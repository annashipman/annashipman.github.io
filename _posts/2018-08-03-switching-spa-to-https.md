---
anchor_id: https-spa
title: Moving SPA to HTTPS
tags: [Technology, SPA conference]
layout: blog_post
---

I had long been thinking I must move the [SPA site](https://www.spaconference.org/) to HTTPS. However, everything is difficult when using shared hosting and I wasn't sure how to do it. So I was delighted when [Johan Peeters](https://johanpeeters.com/) and [Nelis Boucké](https://hachyderm.io/@nelis) proposed a session for the 2017 SPA conference called [Why SPA should switch to HTTPS and how easy that is](http://spaconference.org/spa2017/sessions/session703.html).

It was a great session. In short, they recommended three approaches:

1. Get the hosting provider to do it. Before the session, Yo and Nelis asked me who the SPA hosting provider was (it isn't discoverable through `dig` as it's resellers all the way down). Once I had told them, they did a bit of investigation, and the hosting provider we use charges £180 per year for HTTPS. A bit much for a non-profit conference run by a registered charity.
1. Use [Let's Encrypt](https://letsencrypt.org/). This is a free certificate authority, provided by the non-profit Internet Security Research Group whose aim is to make a secure and privacy-respecting web. The advantage of this is that you are managing it yourself (though that is also a disadvantage as it's then up to you to make sure that you get the configuration right and keep up to date with changes). If you are using nginx or Apache, it can be a little tricky to configure, though that is addressed if you use [Caddy](https://caddyserver.com/docs/automatic-https). However, Let's Encrypt won't work for SPA, as the shared hosting does not allow us to install anything.
1. Use [Cloudflare's free plan](https://www.cloudflare.com/plans/). You need to point your nameservers at Cloudflare. It means that they terminate your TLS and you are sharing a certificate with many other websites, plus the connection from your server to Cloudflare may still be unencrypted, but it's free, easy and massively reduces the attack vectors and ability for people to sniff your network traffic. ([This is an excellent article](https://www.troyhunt.com/cloudflare-ssl-and-unhealthy-security-absolutism/) about the security aspects of Cloudflare's service).

So it seemed like Cloudflare was the only plausible option for SPA.

## First, I set Cloudflare up for this site

Prior that stage, my blog did not use HTTPS, and I didn't see why it would need to, as all the content is [open anyway](https://github.com/annashipman/annashipman.github.io).

But Yo and Nelis made the excellent point that even static sites with non-private content should be HTTPS, because if only sites that need to be private use TLS then that leaks information just by that fact.

Setting Cloudflare TLS up for my site was easy. I did that in the break after the session, and it had propagated within a few hours.

That went so well I decided to move on to doing the SPA site shortly after lunch. This proved to be significantly more tricky.

## CSS stopped working

After the nameservers had been changed to Cloudflare's nameservers, the CSS was no longer available. The site looked like this:

![SPA homepage with no CSS](/img/no_css.png)

My initial response was to publish the site. Big mistake.

![SPA programme page with no content at all](/img/empty_page.png)


## Frantically trying to get the site back online

Before I go on, I should point out that this was in the afternoon of the last day of the conference. (Thank goodness it wasn't the first day!) So while most presenters and attendees were at the post-conference pub drinks, I was at home frantically trying to get something back where the website had been so that when presenters went to upload their outputs from sessions there was something there for them to upload to.

In fact, the `/scripts` pages were fine, so they could have uploaded their outputs... if they'd known to navigate directly to the page.

## The problem was with how we used the CMS

At that stage, the static content on the website was edited in a staging directory using a CMS (a fairly dated version of [CMS Made Simple](http://www.cmsmadesimple.org/)), and then published using a `publish.php` script which copied the content from staging to production.

It turned out that the issue with the blank pages was with the publish script. Somehow, running the script, instead of copying pages from staging to production, had replaced the production pages with empty strings.

The copying was done with the following code:

```
function getUrlContents($url, $credentials="") {
    if ($credentials == "") {
        return file_get_contents($url, false);
    } else {
        $context = stream_context_create(
            array(
                'http' => array(
                    'header'  => "Authorization: Basic " . base64_encode($credentials)
                )
            )
        );
        return file_get_contents($url, false, $context);
    }
}
```
{:.code-sample}

My intial thought was that the issue was with [`stream_context_create`](http://php.net/manual/en/function.stream-context-create.php), possibly with the `http` on line 7. But reading the documentation for that, and for [`file_get_contents`](http://php.net/manual/en/function.file-get-contents.php) and extensive googling for "stream context create HTTPS" got me nowhere. Eventually, I created a small test file to run this code locally. But it output the full page.

So then I deployed my test file to the server, and it failed there. I then tried `curl` on the server, and got this output:

`curl: (35) error:14077410:SSL routines:SSL23_GET_SERVER_HELLO:sslv3 alert handshake failure`

A [StackOverflow answer](https://stackoverflow.com/questions/34578308/how-to-solve-curl-ssl-v3-alert-handshake-failure) led me to question the version of OpenSSL:
````
OpenSSL> version
OpenSSL 0.9.8e-fips-rhel5 01 Jul 2008
````

Essentially, the version of OpenSSL that `curl` was using doesn't allow copying over HTTPS.

Unfortunately, with shared hosting, there's nothing I can do about that. I can't upgrade OpenSSL, and I certainly can't rebundle `curl` and whatever `file_get_contents` is using.

The only solution to allow publishing using the current method was to allow the site to be served as HTTPS and HTTP.

This meant I had to change the settings on Cloudflare to no longer be "always use HTTPS", which also means that I couldn't use [HSTS](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet). This was very annoying as it meant I then had to rely on the user to try to use HTTPS in order to protect themselves. On the plus side, it did allow me to publish the content again rather than an empty string.

## Fixing the CSS

The issue with the CSS was that in the page source there was a tag `<base href="http://spaconference.org/" />`. I could not see where this was being set. After much investigation and a long time, it turned out that this was a metadata tag set by the CMS.

It turned out that to change this setting, I had to change some code in the template from `{metadata}` to `{metadata showbase="false"}`.

![Documentation about the metadata tag](/img/meta_tag.png)

It was not possible to find this by grepping; it involved understanding how the CMS worked. Not for the first time, I thought that I must remove the CMS.

Fixing this meant that the site was available over HTTPS, with CSS, but only if the user went to `https://` rather than `http://`. Not ideal, but a step in the right direction.

## A series of embarrassing roll-backs

However, when it came to launch the 2018 site, I had to roll back even further.

The first roll-back I mentioned above was almost immediate, switching off HTTPS by default in July 2017, in theory until such time that I could fix the publishing/remove the CMS.

Then, in September 2017, when I was deploying the site for 2018, the whole thing went wrong. Instead of the site, I got a Cloudflare warning page.

![Cloudflare warning](/img/cloudflare_warning.png)

I needed to finish getting the 2018 site out, and didn't have time to investigate and fix (often the way on side projects when the next priority should be going to bed). In order to move foward, I had to switch off HTTP entirely, which would have been an embarrassing full climbdown if anyone paid attention to the site outside of the conference season.

I couldn't remove the CMS immediately, as I was in the middle of an [epic of removing MediaWiki from the site](/jfdi/removing-mediawiki-site-changes.html). While I was writing up that epic, I realised that the session and user pages on the 2017 site didn't have CSS because I'd optimistically updated the links to point to HTTPS. So I then had to [find and replace all those links](https://github.com/spaconference/previous-spa-sites/commit/33c5f1a6).

However, the new site was being published with an HTTPS base tag: `<base href="https://spaconference.org" />` which meant that the CSS could not be retrieved as it was no longer available over HTTPS. I knew that I'd set that somewhere but I couldn't remember where, and I spent a long time trying to figure that out. I eventually found the answer... above, in a draft of this blog post. (A huge benefit of [having a blog when you don't have an amazing memory](/jfdi/how-to-blog.html)!)

Then I realised even my new 404 and 500 error pages, added as part of the [MediaWiki removal](/jfdi/removing-mediawiki-cool-uris.html) had a link to the HTTPS version of the homepage. Even that had to be removed.

It was a series of ever more embarrassing roll-backs until, in October 2017, I was exactly where I had been when the session was proposed.

## A side note

At some point during this process, while looking at the certificate, I saw this.

![Shows I have visited site 1,920 times](/img/depressing.png)

That's depressing.

## Fixing the staging issue

In October, once I'd finished removing MediaWiki, I returned to this problem.

The current status was that I could only deploy from staging to live via HTTP because in order to do this, I had to copy the contents of the staging pages to production which didn't work with the available version of OpenSSL. It seemed to me there were three potential ways to address this:

1. Move staging from `http://spaconference.org/staging/` to `http://staging.spaconference.org`. This would mean I could put `spaconference.org` and `www.spaconference.org` on HTTPS while leaving `staging` HTTP to allow the data to be copied.
1. Find another way to copy from staging to production that doesn't depend on OpenSSL, i.e. defer the problem for now with an interim fix until I'm ready to tackle removing the CMS.
1. Bring forward my plan to sack the CMS from 'someday' to 'now'. 

I dismissed the first idea pretty quickly. It would be a lot of work for what would ultimately be a temporary solution. If I'm going to do a lot of work at this stage, it should be to remove HTTP entirely.

The third idea was clearly the best long term idea – removing the CMS was something I wanted to do anyway, but it would be a lot of work, and I wanted not to go down the rabbithole and just get the HTTPS back. So I looked closely at option 2.

## An interesting diversion

My initial supposition was that the files would be generated on the server so I could just copy them over, but they're not. CMS Made Simple stores the data in separate blobs in the database, and composing them is difficult. However, CMS Made Simple is open source, and because we are on shared hosting, the code was vendored, so I could dig into it and work out how the files were composed.

This was a very interesting diversion and involved a lot of diving into [output buffering in PHP](https://secure.php.net/manual/en/book.outcontrol.php). I spent quite some time down this rabbithole, dealing with issues like wanting my script to call an output buffer but it not working, and this being because there was an unexpected `ob_get_clean()` in the CMS Made Simple PHP; the buffers are not nested so that call clears all buffers for the rest of that process.

I finally managed to generate the [Lead a session](https://spaconference.org/spa2017/lead-a-session.html) page using the following code.

```
<?php
require_once('private_scripts/incl_file_helpers.php');

$alias = 'lead-a-session';

function buffer_callback($buffer_contents) {
    $buffer_contents = preg_replace("/index\\.php\\?page=([^\\\"]*)\\\"/", "\\.html\"", $buffer_contents);
    fileWrite("output.php",$buffer_contents);
    return "$buffer_contents";
}
$_SERVER['REQUEST_URI'] = "/staging/index.php/" . $alias;
ob_start('buffer_callback');
include('index.php');
ob_end_flush();

?>
```
{:.code-sample}

I could then call this by:

```
`if (!isset($_SERVER['REQUEST_URI']) && isset($_SERVER['QUERY_STRING']))`

`QUERY_STRING='page=lead-a-session' php -q -d error_reporting=0 index.php > test.html`
```
{:.code-sample}

So essentially the script recreates the page in the same way the CMS does for display, and then copies that page to production.

And this worked! I could use this as the publish script.

Except... it was missing the menu, which is constructed differently.

And a number of other things:

```
Remaining TODO for generating CMS pages

Needs nav and other sorting
Needs programme
Needs not to output the output of the script!
Needs to suppress header warning
Needs switching to HTTPS
Clear the extra buffer handlers
```
{:.code-sample}

At this point, I gave up. This was, again, turning into a rabbithole for an uncertain and interim outcome. It was time to face facts and  remove the CMS.

This was a huge piece of work that took several months (as this is something I maintain in my not hugely copious spare time), and I've written that up [in a separate post](/jfdi/removing-cms-from-spa.html).

## Finally, having removed the CMS...

I switched HTTPS back on. I had only paused it in Cloudflare, so this wasn't a lot of setting back up again.

This time round, there was no issue with the CSS as it was relative, and the [base tag had been removed](https://github.com/spaconference/spa-website/commit/da71c2a). There was no mixed content for the same reason, all neater.

I turned 'Always use HTTPS' back on. This redirects all HTTP requests to HTTPS, which is an extra hop, so ideally I want to update all links in the [previous sites](https://www.spaconference.org/spa2018/previous-conferences.html) but this is not a high priority.

Some of the previous sites don't look great, but there is a Cloudflare setting 'Automatic HTTPS Rewrites' which helps fix mixed content by changing HTTP to HTTPS for all resources that can be served with HTTPS, which fixes some of them. I'll update the others when I have time.

I changed back my new error pages and all the URLs in the code{% comment %}https://github.com/annashipman/spa-conf/pull/113{% endcomment %}, and then switched HSTS back on.

Moving the site to HTTPS caused the build of the [Jekyll site that replaced the CMS](/jfdi/removing-cms-from-spa.html) to fail in a way I hadn't anticipated, but the amazing advantage of the static pages now being open meant that [someone else identified and fixed this problem](https://github.com/spaconference/spa-website/pull/25) before I was aware of it.

The main issue outstanding is that the local version of the scripts doesn't work over HTTPS. This is annoying, but currently only for me as I'm the only person working on it, so I'll fix it at some point. I also set up the SPA account with Cloudflare under my account rather than a separate one, which will make it harder for me to hand over when I do, but that's also a story for another day.

The great success is I finally managed to switch HTTPS back on in time for this year's conference. 

## I'm not sure it was that easy

So, despite Yo and Nelis's claims, it was not in fact that easy. To be fair, they didn't know the full story of the 20 year old PHP site. And it's a great relief to have done it.

I look forward to the next epic task they set me.
