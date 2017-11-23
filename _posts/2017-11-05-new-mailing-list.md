---
anchor_id: mailing-list
title: Sign up to my new mailing list!
layout: blog_post
---

I usually publicise new posts on Twitter, though I also have an [Atom feed](https://www.annashipman.co.uk/atom). However, Twitter relies on people seeing it at the right time, so I've set up a mailing list for new blog posts (and possibly very occasional annoucements).

## Skip the detail and just sign up

<div id="mc_embed_signup">
  <form action="https://annashipman.us17.list-manage.com/subscribe/post?u=c853878c1ba4f3cfef3649e21&amp;id=1d7520de80" method="post" id="mc-embedded-subscribe-form" name="mc-embedded-subscribe-form" class="validate" target="_blank" novalidate>
    <div id="mc_embed_signup_scroll">

      <div class="mc-field-group">
        <label for="mce-EMAIL">Email Address </label>
        <input type="email" value="" name="EMAIL" class="required email" id="mce-EMAIL">
      </div>
      <div class="mc-field-group input-group" style="min-height: 0px;">
        <strong>Email Format </strong>
         <input type="radio" value="html" name="EMAILTYPE" id="mce-EMAILTYPE-0" checked><label for="mce-EMAILTYPE-0">HTML</label>
         <input type="radio" value="text" name="EMAILTYPE" id="mce-EMAILTYPE-1"><label for="mce-EMAILTYPE-1">Plain text</label>
      </div>
      <div id="mce-responses" class="clear">
        <div class="response" id="mce-error-response" style="display:none"></div>
        <div class="response" id="mce-success-response" style="display:none"></div>
      </div>
      <!-- anti-bot signup code-->
      <div style="position: absolute; left: -5000px;" aria-hidden="true"><input type="text" name="b_c853878c1ba4f3cfef3649e21_1d7520de80" tabindex="-1" value=""></div>
      <div class="clear"><input type="submit" value="Subscribe" name="subscribe" id="mc-embedded-subscribe" class="button"></div>
    </div>
  </form>
</div>

## Why I've set up a mailing list

Only publicising posts via Twitter relies on you seeing a tweet to know there's a new post. Twitter is also [problematic](https://www.theguardian.com/commentisfree/2017/jan/03/ive-left-twitter-unusable-anyone-but-trolls-robots-dictators-lindy-west), and it seems like a good idea [not to rely on it](https://medium.com/the-mission/want-the-ultimate-career-asset-and-most-durable-form-of-power-start-building-your-platform-fb02ea7bdb1e) as my only way of sharing my writing.

## Why you should sign up to my mailing list

I blog about a bunch of interesting topics, from [open source in government](https://www.annashipman.co.uk/jfdi/benefits-of-coding-in-the-open.html) through [how to write a good pull request](https://www.annashipman.co.uk/jfdi/good-pull-requests.html) to [tips on conference speaking](https://www.annashipman.co.uk/jfdi/break-into-public-speaking.html), via [more than you ever wanted to know about redirecting URLs](https://www.annashipman.co.uk/jfdi/removing-mediawiki-cool-uris.html), so signing up for the mailing list means you won't miss out on any of that good stuff.

## How I set it up

MailChimp currently have this market sewn up; I checked every newsletter I'm subscribed to (I highly recommend [Sandi Metz's Chainline](https://www.sandimetz.com/subscribe/) and [Benedict Evans's newsletter](http://ben-evans.com/newsletter/), by the way) and they are all powered by MailChimp. The plan is free for the first 2,000 subscribers; after that it becomes relatively pricey and I don't have a business model for this blog. However, you can extract your mailing list and I figured JFDI; it will take some time to get that many subscribers!

However, I had a lot of issues setting it up, and after the amount of time it took me to create the email template I somewhat wished I'd gone a different route. So if anyone has any suggestions of better mailing list software then do let me know.

## A few issues with MailChimp

1. The unsubscribe link in the email takes you to a form that requires you to write the email address you want to remove. This is an annoying pattern (we know what it is! You just followed a link from the very email we sent!) and was nearly a deal-breaker for me, but time is limited and I will work out how to migrate away/fix that later.

1. There were some hidden rules about what email addresses are allowed for the mailing list, for example `list@` wasn't allowed. I don't have a catchall for my domain, so I had to set up a new forwarding address each time without a hint as to which other addresses wouldn't be allowed.

1. I found the experience of setting up the mailing campaign frustrating; drag-and-drop editing the design of an HTML email must be challenging even if you're not by default a Vim user. There is also a limit to how many test emails you can send which I didn't find out about until I'd hit it (it's 12 for free accounts) and there doesn't seem to be any way to test a plain-text version of the HTML email — so if you do sign up to receive emails in plain text and it looks rubbish, please do let me know.

It's also worth noting that they've [changed their default sign-up to not request confirmation](https://kb.mailchimp.com/lists/signup-forms/single-opt-in-vs.-double-opt-in).

## Sending blog posts automatically is easy

Having said that, it is free, and it offers some great advantages. It's very easy to manage subscribers and unsubscribers.

The automation of emailing when a new blog is published via your RSS (or Atom) feed is great and straightforward to set up, it was just designing the email that was taxing. And I'm sure that there are a lot of other advantages to MailChimp that I'll see when I start using it a bit more.

## However, do let me know if you have other good solutions

There are [some free/open source tools](http://www.thatsjournal.com/email-marketing/list-of-best-free-open-source-email-list-management-software) which I didn't have time to look into, and if anyone has any recommendations I'd love to hear them. I think my requirements are:

- double opt-in for sign-ups
- unsubscribe that doesn't require you to type your email address again
- automate sending blog posts as they are published

Also, if you know any MailChimp solutions to my problems above, please let me know.

And do sign up!
