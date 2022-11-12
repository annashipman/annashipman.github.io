---
anchor_id: difficult-teenage-years
title: "The difficult teenage years: Setting tech strategy after a launch"
tags: Strategy Technology
layout: blog_post
---

When you are launching a new product to replace an existing one, it’s easy to rally behind the mission and make the right technical decisions that will get you over the line. But after the launch, it’s very common for things to lose focus: the vision is no longer so clear, corners you cut to get the product live come back to bite, and the tech can start to feel like it’s drifting off track.

This is the difficult teenage years.

## Setting a strategy to get back on track

We experienced this with the [launch of the new FT.com site in 2016](https://www.niemanlab.org/2016/10/the-financial-times-flips-the-switch-on-its-new-website-after-months-of-beta-testing-in-the-open/). The new site is much faster, responsive on different devices and uses modern technology. It has a microservices architecture and ships hundreds of times a week. The launch of the site led to a measurable increase in how often our subscribers visited the site and the number of articles they read while there, and it also led to a big increase in subscribers.

When I joined the FT in 2018 I found an excellent, smart and motivated team, good tech and a great culture. However, some things were drifting off track. This post is about how we created our tech strategy for getting out of the difficult teenage years, and how you could too.

## Strategy is diagnosis, vision and a plan

It’s worth talking about [what strategy is](https://www.annashipman.co.uk/jfdi/good-strategy-bad-strategy.html). A strategy consists of three parts:

1. Diagnosis: What’s the current situation?
1. Vision: What is your desired end state? Where are you trying to get to? What does ‘good’ look like?
1. The plan to get there: What are the highest impact steps you can take to get to your desired end state?

## The vision for the launch of “Next”

The [previous FT.com website](https://web.archive.org/web/20151231154747/http://www.ft.com/home/uk) was a monolith that could only be released once a month, outside of working hours. The site itself was slow and it was also not [responsive](https://en.wikipedia.org/wiki/Responsive_web_design), so on mobile devices it looked like a tiny version of the desktop site. There also wasn’t one team responsible for the overall look, feel, and technical coherence of the site: different parts of the business owned different parts of the website.

Initially, a small team worked on a prototype of a new FT.com website, which they called “Next”. Next has a microservices architecture and is built in Node.js. The Next team focused on building a fast, responsive site, with an emphasis on shipping and measurement. Users were given the opportunity to opt in to the Beta, and 5% did, allowing the team to develop the site in the open with real users.

In October 2016 it was rolled out to all users, and “Next” became the current FT.com site.

## Diagnosis: The difficult teenage years

When I joined the FT in 2018, the site was still good — fast, still using modern technology, still shipping hundreds of times a week, with a focus on measurement and A/B testing everything. The team were focused, smart and really friendly and inclusive.

However, there were some cracks starting to appear. Some of the types of comments I heard were:

- Engineers weren’t sure of the value of the work
- There were areas of code people didn’t want to touch
- There was duplication of code
- A couple of services required deploying microservices in a certain order to make a change (which contradicts the point of microservices, as independently deployable units)
- Feature changes felt too bitty
- Some of the people who set technical direction had moved to other projects
- Someone said, and this was echoed by different people in similar ways, “It doesn’t feel like we are owning or guiding a system, we are just jamming bits in”.
- Finally, something I heard from different teams and different disciplines, a red flag that indicates a lack of focus: “We need more developers”.

These kinds of comments show the main themes of the difficult teenage years:

- Lack of clear vision
- The tech can start to feel like it’s drifting
- Things aren’t communicated as well as they used to be

This is very common after a launch.

## The vision after the launch needs to be different

You need a vision so you know what you are working towards, and to help communicate with others what you are working towards. When you are launching a new site to replace an existing site the vision is easy to communicate, because the new site will be better than the old one in a number of ways. You are replacing something that everyone can see the flaws with, as with the old FT.com site.

It is also easier to have conversations about what is in scope and out of scope before launch because there is usually a date in mind or some kind of milestone, so conversations about whether we have time to get something done before the deadline are much more focused.

After the launch, you no longer have the old site for comparison. So you need to be clear about what ‘good’ looks like.

## Vision: No next Next

The vision for our technology is that we make our tech sustainable.

Good is a healthy codebase that is simple enough for new starters to understand and for us to maintain, that is supportable and operationally reliable, delivers a good user experience and allows us to maintain and increase our ability to add value to the customer and the business.

Bad would be the tech drifting so far off track that we end up in a position where we have no choice but to do another rebuild; another “Next” project again in a few years, with all the costs associated with that.

So our vision is _No next ‘Next’_.

## The plan to get there: The highest impact steps

Once you have the diagnosis and the vision, you need to work out what to do to get from where you are to where you want to be. What are the activities with the highest leverage? What are the things we should do now that will make other things easier later? What are the things that if we don’t do them now, other things we need to do later will be impossible?

## How we worked out what to do

Sometimes, once you are clear on the vision, it’s obvious what the next steps are. Often, however, you need to do some work to get there. Here are some things you can do to help:

- Listen to the patterns in what people say. When I joined the team, I had a one-to-one conversation with each of the engineers, to ask them what was going well, what was going badly (or was about to go badly) and whether there was anything they thought I should know. Some clear patterns emerged from those incredibly useful conversations.
- If you have a specific questions, surveys can help. For example, we wanted to find out what areas of code people were most afraid of, so we sent out a survey to ask that question, and why.
- For general patterns, the [Spotify healthcheck](https://labs.spotify.com/2014/09/16/squad-health-check-model/) is very useful. We send this out every three months, and can see clear patterns which help us prioritise.
- Early on, I gathered the senior engineers together and we had a session where you lay out cards on the floor to identify priorities. ([I explain a bit more about how to run that session here](https://www.annashipman.co.uk/jfdi/russells-strategy-advice.html)). This is a really useful exercise for surfacing things you haven’t thought of, understanding dependencies, and making sure that you are all on the same page.
![People laying out cards to identify priorities](/img/card_workshop.png)
 - Look for artefacts, for example technical principles, dashboards, architecture diagrams and runbooks. These are high leverage things that help make sure everyone has a shared understanding. If they are missing, getting some of those in place is likely to be an early priority. If they are in place, how frequently are they updated and are you sure they are current?
- Finally, a live site is different from a site in development. There are areas that won’t have been a priority before the launch that are for a site in production. For example, how does out of hours support work? How do you handle critical security vulnerabilities? And how do you act on — or even get — customer feedback?

## It’s all about communication

The most important part of a strategy is making sure people know what you’re doing and where you are going. You can have the best vision and best strategy but if no-one knows about it, it’s worthless.

Everyone in the team needs to understand where we are heading so they can make decisions about what they work on so we all get there.

People outside the team need to know our strategy so they can see how it helps the whole FT with our goals as a company, and so they can influence it if they have information that we need.

## Communication takes a lot of effort

Communicating the vision and strategy involves communicating your message in lots of different ways: emails, presentations, small group discussions, posters, etc.
You have to say the same things over and over again, until you are bored of the sound of your own voice saying them, and then even more; because every time you say it, it will be new to someone. Perhaps they missed the last meeting, or weren’t listening, or are new. But if you want people to know what the strategy is, you need to keep talking about it.

Communication is harder after the launch because the vision may not be as clear, and some of the people involved in the launch will have moved on to other projects. So it’s important to put even more effort into how you communicate your vision and strategy.

## It isn’t too late to get back on track

If some of this sounds familiar to you it’s worth letting you know that it might feel like it’s too late for you to get out of the difficult teenage years, but it isn’t. FT.com had been live for 18 months when I joined and we are doing well in getting back into a good shape. I hope that some of these techniques will help you, and I’d love to hear your stories about how you got your tech strategy back on track.

## More detail about our tech strategy is on its way!

In my next post, I’ll talk in more detail about our _No next Next_ tech strategy and how we are doing.

This is a blog post version of a talk I did at [Continuous Lifecycle Conference London](https://2019.continuouslifecycle.london/sessions/launch-difficult-teenage-years/). You can [watch the video here](https://youtu.be/EkfqgQXfEv8), or [see the slides here](https://www.slideshare.net/annashipman/after-the-launch-the-difficult-teenage-years).

And if you are interested in joining us on this journey, [we are hiring](https://roles.ft.com/)!

_This post originally appeared on the [FT Product & Technology blog](https://medium.com/ft-product-technology/the-difficult-teenage-years-setting-tech-strategy-after-a-launch-7f42eb94a424)_.
