---
anchor_id: durable-teams
title: Unlocking value with durable teams
tags: Strategy
layout: blog_post
---

Over the past six months, my group at the Financial Times has moved from project-based teams to durable teams. In this post I’ll explain why we made that move and how this is helping us deliver bigger and better things for our customers.

## We want to be able to deliver as much value as possible

Our goal on Customer Products is to make FT.com and the iOS and Android apps be as good as they can be for our customers, and increase the lifetime value of each customer or corporate licence. As with any tech organisation, we have a tech estate that we need to keep [sustainable, supportable and operationally reliable](https://medium.com/ft-product-technology/no-next-next-42c71541ebcc), while also freeing up as much time as possible to deliver value to our customers and the business.

We use everything we already know about good software development to allow us to focus on where we can really add value. We already do continuous integration, automated testing, effective code review, and many more standard development practices that eliminate wasted time and low value work, and we also experiment, release early and iterate so we don’t spend too much time on work before we know it’s valuable.

However, we realised there was something we could do around the actual organisation of the group itself to help us become a really high-performing team.

## We used to have initiative-based teams

When I first started working at the Financial Times, my group — which builds the ft.com website and the iOS and Android apps — was made up of around 11 teams. Teams were formed around projects, usually with a product focus. For example, we had a Conversion team, whose focus was on converting casual readers into subscribers. When we had new initiatives, for example launching FT podcasts, we formed a new team.

Over the past year, we’ve changed to a new team structure: durable teams. This means our group is made up of nine teams, that each own a product area and the associated tech estate, plus our [ops cops team](https://medium.com/ft-product-technology/why-and-how-we-changed-the-way-we-support-ft-com-7572371f3f36), who handle in-hours support.

![A diagram showing the nine durable teams and how they overlap, along with our small ops cops team](/img/nine_teams.png)

## Initiative-based teams have some advantages

The main advantage of our previous structure is that each team is focused on one product goal, which is good from the perspective of working together to deliver value.

It also allows the group to quickly swarm on problems, and by not having to care about legacy code or bugs, the team are free to work as fast as they can on new features. It was a good approach for the early stages of building the new FT.com, where there was no legacy code to worry about.

It also makes budgeting easy — if we get investment to do an initiative, then we put a team together to do that initiative.

However, there are downsides to this approach, and over time they get worse.

## Forming, storming, norming, perf-

One big disadvantage of changing teams quite frequently, is that it often does not give the team a chance to form into a really high performing unit.

All teams go through a process of team building. One way to represent the stages a team goes through is [forming, storming, norming, performing](https://hr.mit.edu/learning-topics/teams/articles/stages-development), as they figure out how to work together in order to achieve the best outcomes.

If you build teams around projects, this means that there is a ramp-up period while the team go through the early stages, and if the team is not together for long enough, it’s possible they won’t spend very long (if any time at all) in the performing stage. This happens if new initiatives come in and the team is disbanded to form other, new teams.

This is frustrating for the people on the team, and also means the business does not get the best value out of the highly skilled people working for it.

## Orphaned technology is an operational risk that you don’t know about yet

If the team is disbanded to move onto other projects, the technology they have built often does not move with members of the team to the new project. For example when the podcasts team disbands to work on other initiatives, none of the work they’ve done may fit into the new teams.

This is a problem waiting to happen; it is a security and operational risk. Without ownership of tech, if any future development or maintenance is needed, it may be hard to find someone who has time to do it. In some cases, everyone who worked on a project may have left the company.

Even if no security risks arise, it slows things down. If an unowned piece of tech has outlived its usefulness, there won’t be anyone to take care of decommissioning it, meaning that over time your tech stack gets clogged up with code that is not adding value but is adding complexity and slowing everything down.

## Project-based teams remove agency from the team (and add administrative cost)

It takes a lot of effort to form a team; you need to find the right balance of skills, someone to tech lead, delivery manage and be the product owner; you need to find engineers, customer researchers, product designers and possibly business analysts and you need to make sure that the work they are currently doing can be finished or stopped.

It also means the initiative ideas are coming from outside the team. The idea for the project comes about before the team is formed, so by the time the team has formed, it’s already been decided what they are working on, even though that might not represent the biggest opportunity for the business or [even be a feasible idea](https://svpg.com/four-big-risks/).

When you bring a team together to deliver a project that has already been decided, this can lead to the team feeling like a [feature factory](https://medium.com/hackernoon/12-signs-youre-working-in-a-feature-factory-44a5b938d6a2), which is demotivating, and also doesn’t allow people to use their best skills to help solve business or customer problems.

## We decided to move to durable teams

While we were some way from being a feature factory (for example, we have a really strong culture around [measuring the outcomes of our work](https://vimeo.com/273987309), and [A/B testing features](https://2018.continuouslifecycle.london/sessions/how-we-ab-test-at-the-financial-times-and-what-happened-when-we-started-testing-headlines-too/) to see if they are useful) some of the issues highlighted in the feature factory blog post were a little close to the bone, for example, “Team Tetris”.

We realised that one way to address a lot of the issues we had was to move to a durable team structure. This would allow us not just to solve some of the problems we currently had, but also it would allow us to really grow and unlock the potential of our teams.

- We can create teams that between them own our entire estate. Each team can take responsibility for the strategic direction of that area and kill things that no longer add value. We will no longer have unowned tech, which leads to security and operational risk.
- Durable teams mean we do not waste effort stopping and starting teams every quarter.
- Durable teams help people build domain knowledge, mastery and vision, help build organisational memory and fine tune effective ways of working.
- When a team reaches peak productivity, ideas and execution are consistently better. From meaningful work we get motivated people and a better quality product.
- Durable teams help us be clear about what our strategy is, what is in scope and what our capacity is.
- Durable teams make it easier for those outside our group to know who to talk to about a particular part of the product.

## A long-lived team can work on bigger opportunities

A durable team is in a good position to think strategically about the part of the domain they own. When the team knows they are going to be around to experiment, iterate and see the outcomes from changes they make, then they can take bigger bets.

This works from both a product and a technical perspective. A long lived team can take a big bet on changing how we show you relevant news because they will be around to make the changes and keep iterating until they get it right. They can also take a big bet on moving database platform to unlock potential, because they will still be around to reap the benefits of the move.

When a team is just there for a short, or uncertain, length of time, then in order to make any impact, they have to stick to small, incremental improvements. Working on the big bets which might reap huge rewards is too risky — the team may be disbanded before they’ve had a chance to show the benefit. If they have a longer lifespan they are free to try some things that are higher risk. Some will fail, but some will lead to the big changes that lead to exponential growth.

## Stable teams can be empowered teams

What we really want is [empowered teams](https://svpg.com/empowered-product-teams/), coming up with and trying out the ideas that can really deliver value to our customers and help the business grow.

Each of our durable teams has a tech lead, a product manager and a delivery manager. Together, they are responsible for setting the direction for the team, working out what opportunities to focus on, and weighing up priorities within the team. This includes when to focus on adding product features and when it’s more crucial to focus on improving the tech.

As a leadership team, we can step back from making sure we know the detail of exactly what each team will do and concentrate on setting the higher level strategy and objectives. Then we can trust the team to use their huge skills and experience in the domain to identify for themselves what is the most valuable work they could be doing.

## Technical ownership of our estate has already started to save the business money

Our tech strategy on Customer Products is [No next Next](https://medium.com/ft-product-technology/no-next-next-42c71541ebcc). We don’t want our tech to drift so far off track we have to spend £10m and another two years rebuilding it. Making sure all our tech is owned is part of that strategy. When all tech is owned by a currently active team, the team that owns that part of the estate can make longer-term decisions about it.

When we started the move to durable teams, we had 332 systems or repositories, of which 272 were not assigned to a specific team. This didn’t mean that no-one knew about any of them, but we didn’t know which ones people knew about and which were orphaned — we didn’t know the scale of the problem.

Now, all of our systems or packages are owned by a currently active team. As teams started taking ownership, they quickly identified systems that were no longer needed or no longer used. By the time we finished tech ownership, we had removed 47 systems and packages, and more consolidation is planned.

This saves the business money directly in ongoing infrastructure costs, and indirectly, both through engineers no longer needing to maintain these systems, and through making [operational support easier](https://medium.com/ft-product-technology/why-and-how-we-changed-the-way-we-support-ft-com-7572371f3f36https://medium.com/ft-product-technology/why-and-how-we-changed-the-way-we-support-ft-com-7572371f3f36).

## Handling work that falls across teams

There are two main risks in having a durable team set up like this. One is that some work naturally falls across two or more teams. Previously we would have formed a team to work on that thing, but now we need to coordinate between the existing teams to get that done.

The way we address that is as well as Delivery Managers co-ordinating as they usually do, the Principal Engineers — who work across the whole of Customer Products — make sure they have technical oversight and input into those projects. In addition, as far as possible, we try to architect the work so it can be done asynchronously, perhaps released behind a feature flag, and linked together when work in all teams is complete.

## Making sure splitting the domain doesn’t limit opportunities

The other risk is that splitting the domain up into set teams has the potential for limiting thinking. Where you might have previously looked for the biggest opportunity across the whole estate, you might now only look for the biggest opportunity in your domain.

The current situation is still better than it was, in that there is much more potential for teams to make those strategic decisions even within their own domain, as they own everything around that domain. But it is an important part of my leadership role, as Tech Director, alongside the Product Director and Delivery Director, to make sure that this opportunity for bigger picture thinking is not lost.

It’s also worth noting that the current durable teams are not set in stone. It may be that as the product strategy develops over the coming years the actual teams change. However, we will approach any future changes with the same principles: empowerment, total tech ownership and allowing teams to stay together for the long term.

## We got it done just in time

We had the last handover durable team meeting on the 24th February and the FT started working from home on Monday 16th March.

We are so lucky that we got the durable teams work finished in time. Having a durable team is really valuable at a time like this. It would be extremely difficult to manage if we were still trying to put teams together to work on initiatives, while all working from home in difficult and stressful circumstances, and those teams had to bond, figure out how to work together and perform in these circumstances.

## It’s already adding value

We’ve already seen how durable teams helps us go faster. We’ve eliminated some waste in our technical estate and teams are looking for ways to reduce it further. We recently had to take on a piece of work that we hadn’t planned for, and we were able to distribute it among the relevant teams and get started on it, without waiting to hire people for the extra work, and we know when it’s finished it will continue to be owned by those teams. And we’ve seen great ideas emerging from teams, including some excellent discovery work that’s leading to teams taking much bigger bets.

Like many others the FT has been [hit by the coronavirus crisis](https://www.ft.com/content/0069d422-da44-4d06-ae5b-766836bfda6e). Having durable teams and a strategy of a [sustainable, flexible codebase](https://medium.com/ft-product-technology/no-next-next-42c71541ebcc) gives us the foundation to accelerate fast and have greater flexibility to support whatever the business needs, through this crisis and beyond.

_This post originally appeared on the [FT Product & Technology blog](https://medium.com/ft-product-technology/unlocking-value-with-durable-teams-a70efb435a19)_.
