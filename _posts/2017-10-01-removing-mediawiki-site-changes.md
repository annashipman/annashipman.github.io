---
anchor_id: mediawiki-spa-site-changes
title: Removing MediaWiki from SPA&#58; Changes to the site
date: 2017-10-01 09:00
tags: ["Technology", "SPA conference"]
layout: blog_post
---

I run the website for [SPA conference](http://www.spaconference.org). This conference has been running for more than 20 years, and I've been the web admin since 2014. This is about one step in updating a 20-year-old legacy PHP site into something more modern: removing the integrated wiki. The story is in two parts, and this part is about why I removed the integrated wiki and the changes I made to the function of the site to accommodate that.

The second part is about [how I made sure the wiki pages were still available](/jfdi/removing-mediawiki-cool-uris.html).

## The site included a 'discussion wiki'

In early years, the conference was residential and had a much smaller, close community, and the wiki was used much more.

The wiki was an installation of [MediaWiki](https://www.mediawiki.org/wiki/MediaWiki), modified so that conference website and the wiki could share a single login. {% comment %} https://github.com/dcleal/spa-conf/blob/e7dd9c7dc17ff617d7402372d8fe525cf356a135/mediawiki/extensions/SPAAuth/SPAAuth.php {% endcomment %}

In recent years, the wiki has been used for two main things: session outputs and user pages.

## Session outputs

The sessions at SPA are mostly interactive, so session outpts can included slides, working code, links to GitHub repos and blog posts, etc.

Session leaders were encouraged to add output from the session to the wiki and you could then [look at all outputs from the conference](http://www.spaconference.org/mediawiki/index.php?title=SpaTwoThousandAndFourteenOutput).

To replace this, I added the ability for conference presenters to update their sessions with the outputs. You can see an example under the heading 'Outputs' for the session [Access control for REST services](http://spaconference.org/spa2017/sessions/session694.html).

{% comment %} As part of this I added functionality to make them clickable https://github.com/dcleal/spa-conf/pull/88 {% endcomment %}

## User pages

If you are submitting a proposal to SPA, you need to [sign up to the conference site](http://www.spaconference.org/scripts/myprofile.php), where you fill in some details and, if you consented, a user page was created on the wiki.

In previous years tickets were also purchased through the site, so this meant all attendees would also sign up to the conference site, and so most attendees would have a wiki page. The wiki (helped by some PHP scripts) showed a 'card index' of these user pages to help with the community feel:

![Page showing a list of all user pages](/img/people_page.png)

However, the conference is now hosted by the [BCS](http://www.bcs.org/), who handle ticketing, so new profiles were only created for session leaders and conference committee members. The 'card index' wasn't at all up to date with who you might meet at the conference.

I moved the user pages to the site itself, rather than the wiki. And we don't need everyone; just speakers. {% comment %} https://github.com/dcleal/spa-conf/pull/70 {% endcomment %}

Before:

![A user page on the wiki](/img/user_page_on_wiki.png)

After:

![The same user page on the site](/img/user_page_on_site.png)

As part of this, I also made a change to the way the site handled images. {% comment %} https://github.com/dcleal/spa-conf/pull/76 {% endcomment %}Previously, when a user uploaded an image, it would be stored by MediaWiki and that would be the image associated with them. A new image would update their user page. Now, user images are uploaded to a directory called mugshots. When a user is a session leader for a particular conference, and they have an image in mugshots their image will be copied over to the current year's images directory and used in their user page.

Two reasons to copy the image over rather than just linking to mugshots:

- Each year's site should be complete in itself and not reply on images from outside of itself
- A user may upload an updated photo for a session in a different year; that should not change the photo used in a previous year.

## Updating profile page

I also made some changes to the profile page at the same time. For example, MediaWiki markup is no longer allowed. It was also collecting a lot of information like address, phone number and fax (!), but now bookings are no longer done through the site, there's no need to collect this information. I also deleted those columns from the database; there's no need to store it for existing users. {% comment %} https://github.com/dcleal/spa-conf/pull/80 {% endcomment %}

![Old profile page showing out of date fields](/img/profile_page_with_consent_options.png)

I also checked whether that information was published on the wiki so I could remove it from there, but even though there were users who had checked the 'publish address' checkbox, no addresses were actually published on the wiki.

In the near future I'll make more changes to the user page so that we actually get consent (or not) for marketing, rather than the implied consent seen here ("By registering with this site you are giving consent for the BCS SPA Specialist group to contact you..."); both in order to comply with [GDPR](https://ico.org.uk/for-organisations/data-protection-reform/overview-of-the-gdpr/), but also because that's a horrible dark pattern.

This was also a good opportunity to change the markup {% comment %} https://github.com/dcleal/spa-conf/pull/80/commits/adfdc8730 {% endcomment %} from a table to more modern mark-up that will allow it to be read on a smaller device.

## Users without details

Many of the sessions at SPA are lead by two or more session leaders, and if their co-presenters are not already registered on the site, naming them in the proposal creates an empty record (i.e. it bypasses all the compulsory fields). This leads to user pages with no content. This is what that looks like:

Before:

![A wiki page showing a user with no details](/img/wiki_empty_user.png)

After:

![A page on the site showing a user with no details](/img/site_empty_user.png)

I think the after looks better. However, one potential addition is a script to let the programme chairs know which speakers need to pad out their bios. There's no need to force this information at the proposal stage, as some proposals will be rejected.

## Getting rid of the wiki

Having made these changes, there was no longer any need for the wiki. However, there are lots of links to it from previous years, both of outputs and user pages, and [Cool URIs don't change](https://www.w3.org/Provider/Style/URI).

This was a lot of work, so I've written it up in a separate post. [Read on for part 2: cool URIs don't change](/jfdi/removing-mediawiki-cool-uris.html).
