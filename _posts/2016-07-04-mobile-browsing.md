---
anchor_id: mobile-browsing
title: Making my site look better on small screens
tag: Technology
layout: blog_post
---

I've had this blog for five years, but I've only recently started using my phone to browse the internet, at which point I realised it displayed terribly on a small screen. It's a wonder anyone ever read my posts.

<img class="half-width" src="/img/before_responsive.png" alt="Screenshot of site on an iPhone before redesign" />

As a predominantly back-end developer, it wasn't immediately clear to me what I needed to do to improve matters, so I thought it was worth making a note here once I figured it out.

## Responsive design

You want the site to respond to information about the client accessing it to display in the best way for that client. In this case, I wanted the site to respond to browsers with a smaller screen and display differently, rather than just show everything as per a desktop browser but just much, much smaller.

The [media query](http://www.w3schools.com/cssref/css3_pr_mediaquery.asp) allows the site to get the capability of the device.

## Redesign required

The first thing I needed to do was work out how I wanted the site to look on a mobile device, which actually took a bit of thinking about. I realised that the current layout wasn't going to work well and, as is often the way of these things, probably already wasn't working well.

I was using a [three column layout](http://matthewjamestaylor.com/blog/perfect-3-column.htm). However, on some pages the right column was left blank, and on one page I was instead using a two column layout. Only one page was making full use of the three columns. It was time to let it go.

<img class="half-width" src="/img/only_page_using_3_columns.png" alt="Only page using 3 columns" /> <img class="half-width" src="/img/page_using_2_columns.png" alt="Page using 2 columns" />

## Redirecting a URL

I took that opportunity to also rename the Games page. I used to spend more time developing little games; now I do a more diverse range of side projects so I can showcase more of that here. Because my site is hosted on GitHub pages I could not do a [301 redirect](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes), but I set up a [meta refresh tag](https://en.wikipedia.org/wiki/Meta_refresh) to redirect to the new page. A 200 to a 200 is not ideal, but is [better than a 404](https://www.w3.org/Provider/Style/URI.html).

You can see the redesign changes I made [on GitHub](https://github.com/annashipman/annashipman.github.io/pull/5).

## Use Jekyll for the whole site

When I originally started this blog I handcrafted the HTML for each post, and the rest of the site was also handcrafted HTML. My principle was just to get started rather than waiting until I'd figured out the best way to do it.

When I [started using Jekyll](https://github.com/annashipman/annashipman.github.io/commit/b3452315d7ce7a468cb81b590fb131dec412aafb), I only used the Jekyll features for the blog. However the redesign from the inconsistently applied three column layout made it much easier to [Jekyllise the whole site](https://github.com/annashipman/annashipman.github.io/pull/7) and allowed me to [remove a lot of the duplication and handcrafting](https://github.com/annashipman/annashipman.github.io/pull/6).

These initial changes actually made the site worse on mobile because there was more padding on the right.

<img class="half-width" src="/img/in_progress_responsive.png" alt="Screenshot of site even narrower on iPhone screen" />

## Set viewport

The first change after the redesign was [to add the viewport meta tag](https://github.com/annashipman/annashipman.github.io/pull/9/commits/b144e8effe4919d18857685e1ff8cccdb9f467c3) with an initial scale of 1. This sets the zoom level at 1:1 so the page is rendered at the width appropriate to the device width rather than zooming out to fit the whole page onto the screen.

## Make embedded video responsive

After setting the viewport initial scale, most individual posts looked good on mobile. However the JDFI page has all the posts on it, and it looked very wrong. All the content was squished to the left.

<img class="half-width" src="/img/unresponsive_images.png" alt="JFDI page with all content squished to left" />

It turns out that the code provided by YouTube and SlideShare to embed videos/slides into your site is not responsive; it has a fixed width. This means that the site renders the text correctly for the size of the device, but when it gets to the fixed width video it then zooms out to allow space for it.

<img class="half-width" src="/img/fixed_width_video.png" alt="An embedded video pushing the page size out" />

These [two](https://www.abeautifulsite.net/how-to-embed-youtubevimeo-videos-responsively) [articles](https://coolestguidesontheplanet.com/videodrome/youtube/) were useful in working out how to fix this. I changed the HTML to not have the fixed sizes and [added some CSS](https://github.com/annashipman/annashipman.github.io/commit/a66e09868d39c8d2ff6101bcbb2326075feeeffe).

It also turned out that on Safari (and hence on the iPhone) long lines of code were not broken, leading to the same effect as the fixed-width video, which I fixed with an [addition to the viewport tag](https://github.com/annashipman/annashipman.github.io/commit/bc2e73a10a144dff2806914eeadd78b77e954f2b).

## Only have two horizontal columns if device is large enough

Once I'd done all this set up I was at the point I needed to be, where I could change the layout based on the size of the device.

To do this, I looked through the CSS for anything that changes the horizontal structure of any of the elements, e.g. width, float etc, and [put that inside a @media query block](https://github.com/annashipman/annashipman.github.io/commit/251b806141669593e2722432dc91f8168df35354). Initially this was just the two columns but I later [added the Twitter link](https://github.com/annashipman/annashipman.github.io/commit/f2fccec50a5b24d72b5aaa7b99b2646f2b5ddcee).

## Move columns into preferred order

After all these changes, I then [changed the HTML](https://github.com/annashipman/annashipman.github.io/commit/24f94b2589805e697d4f788c00fdcf9ed84a594b) to make the columns appear in the order I would like if they cannot be side by side.

There are many other improvements to make to this site but hopefully if you are reading on mobile it's much easier. Do let me know!
