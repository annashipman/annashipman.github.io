---
anchor_id: next-no-next-next
title: What next for No next Next?
tags: Strategy Technology
layout: blog_post
---
Just over three years ago, I wrote about the tech strategy for Customer Products, [No next Next](https://medium.com/ft-product-technology/no-next-next-42c71541ebcc). In this post I talk about how we’ve implemented our strategy, what the outcomes are, and what we are going to do next.

## Next brought a faster, coherent user experience

“Next” replaced our previous FT.com site, which was powered by a monolith, called “Falcon”. Falcon could only be deployed monthly, out of hours, and Next, powered by a microservices architecture, brought huge performance and productivity gains.

Falcon also didn’t have one team in charge of the whole; different parts of the business owned different parts of the site. Next brought all of the website estate under one leadership team, meaning that product, UX and design work together to form a coherent user experience, and the tech is governed in one place making it easier to improve it, maintain it and keep it secure.

## Fighting entropy: No next Next

It cost £10mn and took us two years to build Next. We wanted to make sure we kept that drive and focus on continuous improvement, rather than letting the tech drift so far off track that we had to throw it away and spend another £10mn and two years building another Next: our tech strategy is No next Next.

In any case, there would be no point in throwing it away and building another stack, because entropy is inevitable. The second law of thermodynamics states that everything tends towards entropy. Unless you actively work towards order, over time your system will become messy, more complex, and ultimately unmanageable.

What No next Next means is a focus on sustainability, on supportability and on simplicity. Maintaining a focus on order, continuous improvement, and active replacement of parts of the codebase that have become too complex. And accepting that entropy is inevitable and finding ways to handle it.

![Dots in neat rows on the left leading to dots all over the place on the right, showing things tending towards disorder](/img/disorder.png)

## Giving teams the support to be great

The Customer Products team are an incredibly smart, talented and kind group of people, and all of the ideas and execution for how we move forward on our tech strategy came from the team. Together, we realised we needed to make the space for those ideas and execution to flourish.

One of the early changes we made was moving to a [stable team structure](https://medium.com/ft-product-technology/unlocking-value-with-durable-teams-a70efb435a19), rather than forming teams around initiatives. When teams are long-lasting, it is easier to have a clear strategic vision and work towards it, and it also means teams have a chance to learn how to work together to perform really well and become more than a sum of their parts.

As part of that, we addressed the problem that over 80% of our repos didn’t have a clear technical owner. That didn’t mean that there wasn’t someone who owned each system, but we had no way of knowing which ones were owned and which were not. Unowned tech is an operational risk you don’t know about yet: you don’t want to find out in a production incident that actually, the only people who knew about that system have left the company.

With the move to durable teams, we also moved to full technical ownership. This did have challenges, as some teams found they owned a lot of systems, some of which they knew nothing about, and over time we are working on managing this, including sunsetting some tech, and working out where ownership may actually be in another group.

We also worked on improving our recruitment process, for example [making it fairer for people of colour](https://medium.com/ft-product-technology/making-recruitment-fair-for-people-of-colour-66a3ad907a7d) so that we can continue to build great teams.

## Replacing parts of the codebase that have become too complex

We [rebuilt a critical part of our website](https://medium.com/ft-product-technology/achievement-unlocked-6edbc0b44ddd), called n-ui, on which all of our user-facing apps depended. N-ui did a lot of work, including building and loading client-side code, configuring and loading templates, as well as tracking, ads configuration and a lot more. It was difficult to maintain, not well understood by the current team, and tightly coupled to technical decisions made at the beginning of building the new FT.com. [We replaced it with a set of loosely coupled packages called Page Kit](https://medium.com/ft-product-technology/designing-a-sustainable-front-end-toolset-for-ft-com-f37c59d27eeb) that have been much easier to maintain, and as an additional benefit, replacing n-ui with Page Kit made FT.com faster, halving our Time To Interactive (TTI) metric.

We are now working on [rationalising some of our content APIs](https://medium.com/ft-product-technology/unspaghettiing-ft-coms-content-pipeline-be1421a434cb) which, over time, have grown organically to be a bit like spaghetti.

![Various systems connected by lines denoting APIs that overlap each other and look complex](/img/spaghetti_apis.png)

We’ve also developed [FT.com Tool Kit](https://github.com/Financial-Times/dotcom-tool-kit) to make it easier for teams across FT.com to install the tooling they need, and helps us keep our codebase consistent and maintainable.

As well as working on the less visible parts of the tech estate that slow down performance and developer productivity, we have also worked on simplifying and improving how we deliver features to make it easier for our colleagues elsewhere in the business to work with us. For example, we have recently [rebuilt the newsletter page](https://medium.com/ft-product-technology/read-all-about-it-rebuilding-the-ft-com-newsletters-page-4a63cb16bf43), and we are about to start work on improving the cancellation journey.

## Improving our supportability

When I joined, we only had 5 people on the out of hours rota, and all of those people were people who’d worked on the original build of Next; new people didn’t join the rota. As I mentioned in [my previous post](https://medium.com/ft-product-technology/no-next-next-42c71541ebcc), part of the solution to this involves doing the hard work to make the tech simpler, such as swapping out the complex parts of the codebase.

However, we also did a lot of great work to make it easier to be on the out of hours rota:

- We had a [documentation day](https://medium.com/ft-product-technology/documentation-day-how-the-ft-com-team-improved-our-documentation-to-95-usefulness-in-7-hours-b73d1a7e6f30) to make sure the documentation people look at for support with systems in an incident were up to date.
- We ran [incident workshops](https://medium.com/ft-product-technology/supporting-our-systems-through-incident-workshops-c0d22a4290b9) so people new to incidents could understand what was involved. Before you’ve been involved in support incidents sometimes you feel that you need to know everything about the stack you are supporting in order to sign up, and one of the really great benefits of the incident workshops is that less experienced staff saw more senior staff saying they didn’t know what was happening, and then see what things they’d investigate to figure it out.
- We introduced a shadow rota, where people could sign up to the out of hours rota but as a shadow, meaning they would get called when there was an incident, but they would not be on the hook for solving it; they would observe and learn. We found that people on the shadow rota often make really valuable contributions to handling incidents.
- We’ve also just introduced a slack group called `@incident-watchers` so that people who want to learn about live incidents can be tagged when we’re having one in-hours and watch along.

These changes meant that we went from 5 to 22 people on the out of hours rota, which is much more sustainable.

![A group of people sat round a table with laptops and metrics displayed](/img/incident_workshop.png)

## Achieving operational excellence

Improving the out of hours support process is great, but what is even better is improving the reliability of the site so that there are fewer failures and it is quicker to recover when there are.

When I joined, we had a rotating responsibility for improving reliability called Ops Cops, which teams would take on for a week at a time, We’ve made a few incremental changes to how we do this, each improving our reliability.

Firstly, we [created a dedicated team with a tech lead and delivery manager, that engineers rotated into](https://medium.com/ft-product-technology/why-and-how-we-changed-the-way-we-support-ft-com-7572371f3f36) so there was consistency from week to week.

While this improved things, we found that the rotation meant that the team was not able to focus on larger, more strategic reliability work. The team also didn’t have clear metrics or service level agreements, so we then [created a stable team of three engineers](https://medium.com/ft-product-technology/next-chapter-on-our-journey-to-achieve-and-maintain-operational-excellence-of-ft-com-7dd9c7871347) and a delivery manager, and we added a product manager.

One year on from these changes [the team are doing great things](https://medium.com/ft-product-technology/operational-excellence-one-year-on-f1dccaf2f034); improving observability and reliability, working more proactively rather than reactively, and making recommendations and providing tools that help us achieve operational excellence.

## Improving technical alignment

We have multiple teams working on microservices who are empowered to make technical decisions. However, teams were getting out of alignment with each other. Different teams were making technical decisions that ultimately lead to conflicting or unclear architectural changes.

To address this, we introduced a [technical design document process](https://medium.com/ft-product-technology/thinking-through-our-changes-with-design-documents-35c93bf0938b). When tech leads are making architectural decisions, they share these documents with the other tech leads for discussion. This allows people with relevant experience in a different team to add useful information to a plan, whereas otherwise they might not know it is happening.

As a side benefit it also forms a documentation trail of architectural decisions. We also now use these when other teams would like to make changes to our stack.

## We are part of a larger team

In 2022, we’ve also been able to expand our tech strategy to be much more closely supporting the goals of the business. When we [first started working on the Customer Products tech strategy](https://medium.com/ft-product-technology/no-next-next-42c71541ebcc) in 2018, the vision for FT.com was still around the recent launch of the new site, and our tech strategy was focused on making sure that it remained sustainable. It was about building good tech and not costing the business more money, but it wasn’t about delivering specific products that move us forward.

The best tech strategy could be summarised as “deliver what the business needs”, and now, we have a [subscriptions business strategy](https://medium.com/ft-product-technology/financial-times-subs-and-product-strategy-2021-1bc48a2a337e), and a clear and compelling [product strategy for FT.com & apps](https://medium.com/ft-product-technology/filling-the-product-strategy-gap-22fb6f792139) which helps us really focus our tech strategy on moving towards the most important goals for the business.

In addition, we are now working much more closely with other tech groups across the FT to pull together a tech strategy for all of FT Technology, rather than each group having their own, separate tech strategy.

## What’s next for no next Next

We’ve seen that our tech strategy has really bedded in and allowed people to make decisions based on what helps make our codebase more sustainable, and enabled and supported the great ideas the team have.

Over time, we’ve changed how we work on tech strategy, from setting [quarterly priorities](https://medium.com/ft-product-technology/the-difficult-teenage-years-setting-tech-strategy-after-a-launch-7f42eb94a424), to this year, following a [deeper, more forward-looking process that helped us set priorities for the whole of 2022](/jfdi/tech-strategy-process.html). Our process in 2022 allowed us to really invest more in our tech strategy priorities. For example, building a team to work on API rationalisation for six months, rather than trying to do this work alongside other, competing priorities, and we’ve really seen the benefit of that approach over this year.

I mentioned that Next brought all of the website estate under one leadership team, meaning that product, UX and design work together to form a coherent user experience, and the tech is governed in one place.

As we move towards a multi-product organisation the exciting challenge for Customer Products is how to enable other tech groups to deliver features, some of which will be on FT.com and the apps, without losing the coherent user experience and the strong tech governance.

All this means that the 2023 Customer Products tech strategy will be part of a larger business strategy. So there may be no next for No next Next, but I’m incredibly excited about what we are going to do next!

*This post originally appeared on the [FT Product & Technology blog](https://medium.com/ft-product-technology/what-next-for-no-next-next-adbb02406171)*
