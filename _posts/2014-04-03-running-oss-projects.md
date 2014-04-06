---
anchor_id: oss
title: Running OSS projects
layout: blog_post
---

At [ScaleSummit](http://www.scalesummit.org/) last week, I proposed a session on running Open Source projects. I am hoping to move the project I'm working on, [vCloud Tools](https://github.com/alphagov/vcloud-tools), from being [coded in the open](https://gds.blog.gov.uk/2012/10/12/coding-in-the-open/) to being Open Source and wanted to get the benefit of the accumulated wisdom. It was an excellent session and I really got a lot out of it.

The executive summary is that if you are trying to build a community, you need to optimise for bringing people into the community, and a lot of the discussion focused around that. Here are some of the main things that I took away from it.

### Good documentation is crucial

Optimise documentation for bringing people into your community. It’s unlikely to already be good for that, as you are so familiar with the code and the project that you don’t realise what someone new to it doesn’t know.

One way to do this is to make it clear that you are happy to answer people’s questions -- even hundreds of questions -- as long as they follow up by submitting a patch to clarify the documentation. Encourage people to raise bugs against the documentation.

### Make it easy to get involved

Make it clear how people can contact you for clarification or with ideas. An IRC channel is a great, if you can make it work, but you need to be aware of certain drawbacks. For example, people tend to expect a quicker response than by email, so you need to make sure people are in it. It will be very quiet at night in the UK.

In a later discussion back at GDS we decided not to do that for this project because there would be a lot of effort to make it work and it would be an added distraction. We definitely don’t want to say “Come to our vCloud Tools IRC channel” if there’s no-one there.

As well as (or instead of) an IRC channel, you should have a mailing list.  You can either make it open or make it so that only a subset of people can reply. Someone advised that it wasn’t a good idea to have lots of mailing lists, (\*announce\*, \*discussion\* etc). It was also pointed out that even if you’re not writing code, managing the community can easily become a full-time job.

The Perl community does communication well, and the example of [Catalyst](http://www.catalystframework.org/) was given -- this project has 450 committers and the maintainer has changed 5+ times. Also mentioned was this blog post about communication with newcomers to the project: [Love your idiots](http://shadow.cat/blog/matt-s-trout/love-your-idiots/).


### Respond quickly to external contributions

One of the things that I especially wanted to know about was how quickly you should aim to respond to pull requests. This is particularly an issue in that we are going to be managing this in work time and there will be competing priorities. The general consensus was you need to respond within 24 hours, and it’s acceptable for this not to include weekends if you are clear in your documentation that this is the case. It’s important to note that the response doesn’t have to be a review or a merge, it can be as simple as a note saying “Thanks for this, I am going to review it in a couple of days”.

The most important PRs to pay attention to are the ones from new contributors. Again, optimise for bringing people into your community.

It’s a good idea to have CI run tests on PRs so you can see failures before merging -- [Travis](https://travis-ci.org/) is good for this as it integrates well with GitHub. However, it was stressed that it is important to review the contribution as well, even if it passes all the tests!

### Communicate your vision

Something else I was particularly interested in is what do you do if you feel a well-meaning PR is pulling the project in the wrong direction? It was suggested that a lot of this comes back to documenting your original vision and being very explicit about what this software is aiming to do.

You need one person or a group of people to be responsible for maintenance, and they are the ones responsible for the vision. Someone gave the example of [Mozilla](http://www.mozilla.org/) in the early days who just accepted everything, and eventually had to rewrite the core offering.

But also, take it as it comes. If you as the maintainer don’t think a direction is correct, it’s completely fine for someone to fork the software, and you may later find that the fork is doing the job better. The example of [GCC](http://gcc.gnu.org/) was given, where a separate fork existed for about 5 years, and the GCC maintainers eventually realised that the fork was what everyone was using and merged it back in.

Modularity also makes the process easier -- having a common core that everyone can agree on is relatively easy, and divergence can be supported with plugins.

It is very important that if you close a PR, you do so with a clear explanation, whether this is due to poor quality or incompatible direction. 

### Don’t be too hardline

One thing we talked about was not being too strict with external contributors. Sometimes people might not have the experience to know how to write tests, either in general or in your particular test framework, so insisting that a PR must have tests before it can be merged is going to put people off who could have really valuable contributions. Some people said they are very happy to write tests for newbies. Talk to the contributor to find out why they wanted to make those changes and then show them the tests you've written, maybe asking them whether it looks like the test cases cover the functionality they wanted to add.

However, changes in functionality should definitely include updated documentation and it is more reasonable to reject a PR for lack of that.

### Assume people have the best intentions

This is great advice for life in general. Even if what they are suggesting looks completely wrong and it’s hard to understand how they could have thought it was the right approach, assume they have the best intentions and proceed accordingly.

### Issue tracking

We currently manage work on the project internally using [PivotalTracker](http://www.pivotaltracker.com/). My plan was, once we’re ready to make it OSS, we move remaining features and bugs to GitHub issues, and work from that. This was seen as a good idea -- it makes it clear to people what we are planning to work on and (ideally!) prevents them from raising issues we already know about. It also has a major benefit -- you can Google for the issue.

### It must be an active project

You need to be using the software yourself, otherwise it’s a recipe for abandonware. And it’s good to make this activity clear -- related to the above point about issue tracking, if all your activity is on your internal tracker and mailing list and private IRC channel, then it won’t be clear to potential users and contributors that the project is still active. 

### Contributing Guidelines

It is important to have contributing guidelines. This wasn’t discussed extensively in the session, but in an extremely helpful follow-up email from [Tom Doran](https://twitter.com/bobtfish) he pointed me at a number of great resources which included the [Catalyst development guidelines](https://metacpan.org/pod/distribution/Catalyst-Manual/lib/Catalyst/Manual/DevelopmentProcess.pod). I also heard from [George Brocklehurst](https://twitter.com/georgebrock) who pointed me at the [contributing guidelines for gitsh](https://github.com/thoughtbot/gitsh/blob/master/CONTRIBUTING.md) and also a really useful page that [thoughtbot](http://thoughtbot.com/) have on [code review](https://github.com/thoughtbot/guides/tree/master/code-review).

### Legal issues

Something that was raised as we finished up the session and were leaving was that, especially as Government, we need to be very careful about who owns the code. For example, some people may be working for companies where their contract states that the company owns all OSS contributions.

### What next for vCloud Tools?

These considerations and some others mean it will be a little while before we move vCloud Tools from coding in the open to OSS, but it was really useful to have this input which covered a lot of things I hadn’t thought about.

Many other things were discussed, including when you need a standalone website, and what tools are good for versioning documentation, but these were the things I found most useful and relevant. Thanks a lot to everyone who took part in the session, it was very valuable and constructive.

#### Notes

Note that ScaleSummit operates under the [Chatham House Rule](http://en.wikipedia.org/wiki/Chatham_House_Rule) so none of the comments made in the session have been attributed, and thanks to [Matt Bostock](https://twitter.com/mattbostock) and [Phil Potter](https://twitter.com/philandstuff) whose write-ups ([Matt's](http://tech.mattbostock.com/2014/03/23/scale-summit/), [Phil's](https://gist.github.com/philandstuff/9684513)), were a very useful addition to my own notes.
