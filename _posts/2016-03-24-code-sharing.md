---
anchor_id: code-sharing
title: Code sharing in large organisations
tags: Technology Leadership
layout: blog_post
---

At [Scale Summit](http://www.scalesummit.org/) last week I led a session on code-sharing in large
organisations. I was particularly interested in how other organisations raise
the visibility of shareable code. This was one of the main themes that came out of the recent [code-sharing unconference at
GDS](https://gdstechnology.blog.gov.uk/2016/03/04/code-sharing-unconference/).

These are the main things I took away from the discussion. For more comprehensive notes, check out [Barrie Bremner's write-up](https://github.com/bazbremner/scalesummit-2016-notes/blob/master/code_sharing.org).

## Some ideas of how to raise visibility of code

People in the session shared the way they publicise code/projects in their organisation. Techniques include writing blogs, either internal or external, presenting at internal meetings and writing things up on internal forums. Facebook have a newsletter called the [Weekly Push](http://blog.newspaperclub.com/2014/04/22/paper-of-the-month-the-weekly-push/) which is used, among other things, to publicise less well known features or new products. In some offices this is pinned up in the toilets!

However, apart from the last one, these are mostly pull methods of communication. You have to know they are there and how to find them. The newsletter is a great idea, but in less joined-up organisations you can't be sure that push communications will get to everyone.

## It's useful to have a community

The discussion kept returning to the value of having a community around areas of interest. If you are regularly talking to other people in your field, you are more likely to find out about similar work other people are doing. There can be a lot of noise, and a community can help you learn what works and what doesn't, and can make it easier to talk to relevant people at the start of a piece of work, rather than when you've gone too far down a certain path. In order to encourage useful sharing of information and discussions taking place at the right time, an organisation could support these kinds of communities.

As well as meetings and distribution lists, people talked about other ways to share information, for example, having a [Slack channel](https://slack.com/) for a particular community. You could drop in and say "I have this problem, does anyone have a solution?".

One person pointed out that we often focus on code-sharing when in fact the real goal should be community. If code is shared or reused as a result of that community, that is good, but having a community is where the real value lies.

For those working in UK government, there are already [some forums for these discussions](https://gdstechnology.blog.gov.uk/join-the-conversation/).

## How to build a community

One useful idea came from [Paul Gillespie](https://twitter.com/bigpg) (quoted with permission). He explained that at Skyscanner, they copy [Spotify's org struture](http://www.scribd.com/doc/113617905/Scaling-Agile-Spotify), and have something called guilds. These are essentially communities of interest. For example, they have one for web dev, one for AWS, one for Python. These guilds have Slack channels, mailing lists and every two weeks they have a guild meeting, which is a one-hour webinar. They use Trello to set the agenda for this meeting, and each guild is run by a core committee.

I later talked to Paul a bit more and he said that in total they have around 6 or 7 guilds. You don't want to have too many, because being involved in a guild is quite labour-intensive.

## Beware of premature optimisation

Early on in the discussion it was pointed out that we should be mindful of what problem we are actually trying to solve before addressing how to share code. Many problems seem superficially similar but turn out not to be, so the same code/product/solution will not be appropriate to both. You may waste time coming to this conclusion or bloat software by trying to make it cover too many different scenarios.

There can also be a lot of pressure to consolidate, and some of this can come from senior management seeing false patterns, for example "too many case management systems". It was noted that spotting actual duplication and finding prior art in this area is part of the role of an architect, but in a large organisation visibility of code is still difficult.

The problem we are trying to solve is to reduce duplication of work, rather than specifically duplication of code. More generally, we do not want teams to waste time reinventing the wheel. We do not necessarily want "the best tool for the job", we want the most cost-effective tool, and that might be copying someone else's code, or the team solving the same, or similar, problem in a different way.

## Code-sharing isn't always the answer

If someone has written code that is perfect for your use case, it can still be hard to share. Even if it is well documented, there is still a ramp up cost to understanding it, and it is unusual that the code can be dropped right in. Several people mentioned that you need to weigh up the cost of these factors against the cost of duplication of code. Arrayed against these factors, building it yourself might not turn out to be that expensive.

## It's important to weigh up the costs

The general feeling was that forming a community is very useful to prevent duplication of work or code, but it was also pointed out that there are costs. For example the time cost of communication and staying in touch, keeping documentation up to date etc. Again, these may outweigh the costs of duplicating work.

There are other advantages to being involved in communities of interest, but it is worth considering the cost of the time and effort. For example, while the idea of a Slack channel for a community, mentioned above, can be very useful, [Slack can also be a drain on productivity](http://m.signalvnoise.com/is-group-chat-making-you-sweat-744659addf7d#.3dhurm2vu).

We also returned a few times to the topic of sharing services, or platforms, rather than the code itself. Instead of writing code to be shared, build a service or platform that provides functionality. However, the question of cost came up again: building and operating a service is expensive and takes skilled people, as well as maintenance costs.

## My take-home message

The main thing I took away from this discussion is that you need to be clear about what problem you're trying to solve and what the costs of the solutions are. Sometimes an increased awareness of code that has already been written will solve your problem, but sometimes what you need might be access to a service, or it might be to share knowledge across a community.

Thanks very much to all who took part in the discussion.
