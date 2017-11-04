---
anchor_id: mailing-list
title: Sign up to my new mailing list!
layout: blog_post
---

I usually publicise new posts on Twitter, though I also have an [Atom feed](https://www.annashipman.co.uk/atom). However, Twitter relies on people seeing it at the right time, and personally if I wanted to keep up with someone's blog I'd want to get emails, so I've set up a mailing list for new blog posts (and possibly very occasional annoucements).

## Skip the detail and just sign up

<link href="//cdn-images.mailchimp.com/embedcode/classic-10_7.css" rel="stylesheet" type="text/css">
<style type="text/css">
    #mc_embed_signup{background:#fff; clear:left; font:14px Helvetica,Arial,sans-serif; }
    /* Add your own MailChimp form style overrides in your site stylesheet or in this style block.
       We recommend moving this block and the preceding CSS link to the HEAD of your HTML file. */
</style>

<div id="mc_embed_signup">
  <form action="https://annashipman.us17.list-manage.com/subscribe/post?u=c853878c1ba4f3cfef3649e21&amp;id=1d7520de80" method="post" id="mc-embedded-subscribe-form" name="mc-embedded-subscribe-form" class="validate" target="_blank" novalidate>
    <div id="mc_embed_signup_scroll">

      <div class="mc-field-group">
        <label for="mce-EMAIL">Email Address </label>
        <input type="email" value="" name="EMAIL" class="required email" id="mce-EMAIL">
      </div>
      <div class="mc-field-group input-group">
        <strong>Email Format </strong>
          <ul><li><input type="radio" value="html" name="EMAILTYPE" id="mce-EMAILTYPE-0" checked><label for="mce-EMAILTYPE-0">HTML</label></li>
          <li><input type="radio" value="text" name="EMAILTYPE" id="mce-EMAILTYPE-1"><label for="mce-EMAILTYPE-1">Plain text</label></li></ul>
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

Twitter is ephemeral, it relies on you seeing a tweet about a new post to know it's there. It's also [problematic](https://www.theguardian.com/commentisfree/2017/jan/03/ive-left-twitter-unusable-anyone-but-trolls-robots-dictators-lindy-west), and it seems like a good idea [not to rely on it](https://medium.com/the-mission/want-the-ultimate-career-asset-and-most-durable-form-of-power-start-building-your-platform-fb02ea7bdb1e) as my only way of sharing my writing.

## Why you should sign up to my mailing list

I blog about a bunch of interesting topics from [open source in government](https://www.annashipman.co.uk/jfdi/benefits-of-coding-in-the-open.html) through [how to write a good pull request](https://www.annashipman.co.uk/jfdi/good-pull-requests.html) to [tips on conference speaking](https://www.annashipman.co.uk/jfdi/break-into-public-speaking.html), via [more than you ever wanted to know about redirecting URLs](https://www.annashipman.co.uk/jfdi/removing-mediawiki-cool-uris.html), so signing up for the mailing list means you won't miss out on any of that good stuff.

## How I set it up

MailChimp currently have this market sewn up; I checked every newsletter I'm subscribed to (I highly recommend [Sandi Metz's Chainline](https://www.sandimetz.com/subscribe/) and [Benedict Evans' newsletter](http://ben-evans.com/newsletter/), by the way) and they are all powered by MailChimp. The plan is free for the first 2,000 subscribers; after that it becomes relatively pricey and I don't have a business model for this blog. However, you can extract your mailing list and I figured JFDI; it will take some time to get that many subscribers!

However, I had a lot of issues setting it up, and after the amount of time it took me to create the email template I somewhat wished I'd gone a different route. So if anyone has any suggestions of better mailing list software then do let me know.

## A few issues with MailChimp

1. I had a massive shock when I tried to sign up my first test user as it shows your home address. Wow. No way. You have to enter this because of a [US anti-spam act](https://www.ftc.gov/tips-advice/business-center/guidance/can-spam-act-compliance-guide-business) and it's a US company. You also have to include this info in every email, so I have used a PO Box instead.

2. They've [changed their default sign-up to not request confirmation](https://kb.mailchimp.com/lists/signup-forms/single-opt-in-vs.-double-opt-in) and the process for [changing this setting](https://us17.admin.mailchimp.com/lists/opt-in-status/) is somewhat opaque:

    ![Image of an unlabeled checkbox that you have to select for double-opt-in](/img/select_double_opt_in.png)

3. There were some hidden rules about what email addresses are allowed for the mailing list, for example `list@` wasn't allowed. I don't have a catchall for my domain, so I had to set up a new forwarding address and attempt to create an account with no clue about which other addresses wouldn't be allowed.

4. It doesn't seem that you can change the default subscribe options:

    ![Image showing subscription preferences which include 'First Name' and 'Last Name'](/img/subscription_preferences.png)

    I don't want to ask for first name, last name as that is [not good practice for handling names](https://www.w3.org/International/questions/qa-personal-names). I guess that being able to change these settings is one feature of a paid-for plan but it's a shame to have to pay to correct that.

5. The link in the email should you wish to unsubscribe takes you to a form that requires you to write the email address you wish to be removed. This is an infuriating pattern (we know what it is! You just followed a link from the very email we sent!) and was nearly a deal-breaker for me, but time is limited and I will work out how to migrate away/fix that later.

## Sending blog posts automatically

I found the experience of setting up the mailing campaign frustrating; drag and drop editing the design of an HTML email must be annoying even if you're not by default a Vim user. There is also a limit to how many test emails you can send which I didn't find out about until I'd hit it (it's 12 for free accounts) and there doesn't seem to be any way to test a plain-text version of the HTML email — so if you do sign up to receive emails in plain text and it looks rubbish, please do let me know.

However, the automation of emailing when a new blog is published via your RSS (or Atom) feed is great; it's nice not to have to set that up.

## Let me know if you have other good solutions

I think MailChimp has a lot of great functionality if you are selling things, but I really just want a mailing list to keep in touch. There are [some free/open source tools](http://www.thatsjournal.com/email-marketing/list-of-best-free-open-source-email-list-management-software) which I didn't have time to look into, and if anyone has any recommendations I'd love to hear them. I think my requirements are:

- embedded form to allow sign-up
- double opt-in
- one click unsubscribe
- automate sending blog posts as they are published

Also, if you know any MailChimp solutions to my problems above, do let me know.

And do sign up!


TODO:

- polish up this post and go!!
- add a footer to all posts, something about sending the posts but also something else.
If you’d like to be notified when I publish a new post, and possibly receive very occasional announcements, sign up to my mailing list!
- move CSS to stylesheet
- don't forget to actually activate the campaign!
- and delete the other one
