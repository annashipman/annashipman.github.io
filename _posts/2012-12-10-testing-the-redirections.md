---
anchor_id: testing-the-redirections
title: Testing the redirections
tag: Technology
layout: blog_post
---

Now that [GOV.UK](https://www.gov.uk/) has replaced Directgov and BusinessLink, and departments are
moving to [Inside
Government](http://digital.cabinetoffice.gov.uk/2012/11/15/a-quick-tour-of-inside-government/), we want to make sure that people visiting links to
the old sites get where they need to be. We want them to be redirected to the
correct page on GOV.UK, with [no link left
behind](https://gds.blog.gov.uk/2012/10/11/no-link-left-behind/).

This post is about the tools we built to make that possible.

## Finding the links

The first thing we needed was a list of everything we wanted to redirect: all
the Directgov and BusinessLink URLs (links and Web addresses). This proved to be
a fairly significant task - both sites had long histories and various different
providers, so a comprehensive list of these URLs did not exist.

Instead, we collected our own lists from a variety of sources, including
[traffic](http://en.wikipedia.org/wiki/Web_traffic)
logs, records of friendly URLs (shorter, more memorable links that redirect to
longer URLs), and the results of
[spidering](http://en.wikipedia.org/wiki/Web_crawler) the sites.

This gave us a total of about 8,000 Directgov URLs and about 40,000 BusinessLink
URLs.

## Wrangling the URLs

Many of the lists of URLs existed in various spreadsheets, maintained by
different people. We needed a canonical source of truth. So we built the
[Migratorator](https://github.com/alphagov/migratorator).

The Migratorator is a [Rails](http://rubyonrails.org/) app, backed by a
[MongoDB](http://www.mongodb.org/) database. It allows
multiple users to create one-to-one mappings for each URL, where the mapping
consists of the source URL, status (whether it will be redirected or whether, no
longer representing a user need, it is now gone) and, if applicable, the page to
which it will be redirected.

![Migratorator image](/img/migratorator_mapping.png)


As well as the mapping information, the Migratorator allows us to capture other
useful information such as who has edited a mapping, tags showing information
about the type of mapping, and a status bar showing how far through the task we
are.

![Migratorator detail](/img/migratorator_filter.png)

## Checking the mappings

We needed to confirm that the mappings were actually correct. We wanted several
people to check each mapping, so we created the
[Review-O-Matic](https://github.com/alphagov/review-o-matic).

The Review-O-Matic is also a Rails app and uses the Migratorator API to display
the source URL and the mapped URL in a side-by-side browser, with voting
buttons.

![Review-O-Matic](/img/review-o-matic.png)

We asked everyone in GDS to help us by checking mappings when they had some
spare time. However, clicking through mappings can be dull, so we ran a
competition with a prominently displayed leader board. The winner, who checked
over 1,000 mappings, won cake.

## Confirmation from departments

The Review-O-Matic presents the mappings in a random order, and the way it's set
up means that links within pages cannot be clicked. This is good for getting as
many mappings as possible confirmed, but our colleagues in departments needed to
check content relevant to them in a more methodical and interactive way. Enter
the [Side-by-side Browser](https://github.com/alphagov/review-o-matic-explore).

The Side-by-side Browser displays the old and the new websites next to each
other. Clicking a link on the left hand side displays what this will redirect to
on the right hand side.

![Side-by-side browser image](/img/sidebyside.png)

The Side-by-side browser is a [Node.js](http://nodejs.org/) proxy that serves itself and the site
being reviewed on the same domain, so that it's 'live' and not blocked by the
[Same-Origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy). We joked that, in essence, the side-by-side browser was a
phishing attack for the good!

Initially it used the Migratorator API for the mappings. However, once we'd
built and deployed the Redirector, we could use that instead to populate the
right hand side. As well as simplifying the code, this meant we could now see
what the Redirector would actually return.

At this point, we distributed it to our colleagues in departments to check the
mappings and raise any concerns before the sites were switched over.

## Bookmarklet

We used another trick to test Directgov mappings while the site was still live.
We created a domain called aka.direct.gov.uk, which was handled by the
Redirector, and a [bookmarklet](http://whatfettle.com/2012/09/aka.html). By replacing the 'www' with 'aka' the bookmarklet
allowed us to see what an individual Directgov page would be replaced with.

## The Redirector itself

For the actual redirection, we use the open-source Web server
[Nginx](http://wiki.nginx.org/Main). The
[Redirector project](https://github.com/alphagov/redirector/) is just the process for generating the Nginx configuration.
It's written mainly in [Perl](http://www.perl.org/) with some
[PHP](http://php.net/).

Generating the Nginx config requires logic to determine from the old URL what
kind of configuration should be used.

For example, the important part of a Directgov URL is the
[path](http://en.wikipedia.org/wiki/URI_scheme#Generic_syntax), e.g.
[www.direct.gov.uk/en/Diol1/DoItOnline/Doitonlinemotoring/DG_196463](http://www.direct.gov.uk/en/Diol1/DoItOnline/Doitonlinemotoring/DG_196463), while for
BusinessLink the essential information is contained in the query string, e.g
[http://www.businesslink.gov.uk/bdotg/action/detail?itemId=1096992890&type=RESOURCES](http://www.businesslink.gov.uk/bdotg/action/detail?itemId=1096992890&type=RESOURCES).
Redirecting these two types of URL requires different types of Nginx config.

This logic, plus the mappings we gathered, make up much of the Redirector
project.

## The joy of tests

In addition, the project contains a suite of unit and integration tests,
including one that runs every night at 5am. This test checks that every single
URL in our source data returns a [status
code](http://en.wikipedia.org/wiki/List_of_HTTP_status_codes) that is either a 410 'Gone' or a
301 redirect to a 200 'OK'.

For a few weeks before the launch we also ran the daily Directgov and
BusinessLink logs against the Redirector to see if there were any valid URLs or
behaviour we'd missed. By doing this we found that, for example, even though
URLs are case-sensitive, Directgov URLs were not, and users would therefore
expect [www.direct.gov.uk/sorn](http://www.direct.gov.uk/sorn) to work in the
same way as [www.direct.gov.uk/SORN](http://www.direct.gov.uk/SORN).

## Going live!

The final task was to point the
[DNS](http://en.wikipedia.org/wiki/Domain_Name_System) for the sites we're now hosting at the
Redirector. Now users following previously bookmarked links or links from old
printed publications will still end up on the right place on GOV.UK.

![redirector post-it gets lots of votes at retrospective](/img/redirects.jpeg)

The configuration now has over 83,000 URLs that we've saved from [link
rot](http://en.wikipedia.org/wiki/Link_rot), but
if you find an old BusinessLink or Directgov link that's broken then let us
know.

Traffic through the Redirector is easing off as GOV.UK pages are consistently
higher in the Google search results, but it's been really exciting making sure
that we do our best not to break the strands of the Web.

*This post originally appeared on the [GDS Blog](https://gds.blog.gov.uk/2012/12/10/testing-the-redirections/).*
