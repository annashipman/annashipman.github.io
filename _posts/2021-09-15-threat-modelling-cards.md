---
anchor_id: threat-modelling-cards
title: Threat modelling cards
tag: Technology
layout: blog_post
---

Threat modelling is a way to identify the potential security flaws in your system, and prioritise mitigations. On Monday I attended a session comparing some card games you can use to help you, at [SPA conference](https://www.spaconference.org/). This is a brief write-up.

## The purpose of threat modelling cards is to provoke discussion

There are various ways to do threat modelling, for example the [National Cyber Security Centre (NCSC) recommends attack trees](https://www.ncsc.gov.uk/collection/cyber-security-design-principles/establish-the-context-before-designing-a-system).

Security cards are a way to help a group think laterally about the problem, and bring up ideas and discussion of potential security flaws that might not have come up on first thinking about it. They can also be a way to engage everyone in the team with the problem.

The idea of this conference session was to compare three such card decks to see what kinds of insights they generated.

## The session was really well put together

The session was run by [Charles Weir](https://charlesweir.com/), [Lucy Hunt](https://www.lancaster.ac.uk/scc/about-us/people/lucy-hunt) and [Shamal Faily](https://www.shamalfaily.com/). They had documented a basic banking application with a simple architecture diagram. We then used one of the three card decks to generate potential security issues with the application. After ten minutes we swapped to another card deck, and then the third. The three groups each used the three decks of cards in a different order.

At the end of the three games we spent a few minutes dot voting on the issues we'd identified – black dots for the most important, red dots for the most interesting.

## We used three very different decks of cards

The card games we used in this session were [Elevation of Privilege](https://www.usenix.org/conference/3gse14/summit-program/presentation/shostack) (you can download a [very useful presentation](https://adam.shostack.org/Elevation-of-Privilege-BlackHat2010ShostackFinal.pptx) on it), [Adversary Personas](https://daylight.berkeley.edu/adversary-personas/) and [Security and Privacy Threat Discovery](http://securitycards.cs.washington.edu/index.html).

Each of these decks were quite different with different activities involved.

## Elevation of Privilege

The Elevation of Privilege cards are very technical. They outline something that might happen, divided into the six areas in the [STRIDE framework](https://en.wikipedia.org/wiki/STRIDE_(security)). For example, one card is titled "Spoofing" and reads "An attacker could squat on the random port or socket that the server normally uses".

The actual game involves placing cards on the diagram to indicate where in the architecture the situation described on the card could be a problem, but for our shortened version of the game we were to indicate what situation was present for this to be a problem.

All the cards were more or less that level of technicality, requiring a fairly high base level of architectural knowledge and understanding of security terms. It would be hard to imagine playing this game with the product owner or even junior engineers.

It did however prompt some advanced thoughts and useful discussion about what security flaws there might be in our system.

## Adversary Personas

This was the second game our group played and was very different. It had cards about human impacts (e.g. "Societal wellbeing"), cards about Adversary Motivations (e.g. "They are incompetent", "They need to influence politics"), cards about Adversary Resources (e.g. "They live in tomorrow's world").

You play this game by first understanding what you are protecting (the impact) and then getting into character as one of the adversaries, and then using the resources to see if that affects how you think about that persona. The end goal is to identify the top three personas who are most likely for your organisation and then identify what and how they might attack your system.

As for all the games, we didn't play the full version in the session. Instead, we talked about the personas and impacts and used that discussion to identify some potential issues.

This one generated some really interesting discussion, and people with less technical or security experience were able to get fully involved.

## Security and Privacy Threat Discovery

This was the third game we played, and after the other two it was very odd. Each card in this game has A LOT of information and suggestions. For example, a card headed "Technological Attack: Adversary's Methods" reads:

<div class="quote">
<p>What kinds of technical attacks might the adversary perform over an analog or digital link? How would this enable or amplify an attack on confidentiality, integrity, or availability?</p>
<p>Example Related Concepts:</p>
<ul>
<li>Example Attacks: denial-of-service · spoofing · repudiation · elevation of privilege · replay attacks · relay attacks · jamming</li>
<li>Example Outcomes: acquire password files · eavesdrop on confidential exchanges · install bot software</li>
</ul>
</div>

Coming straight after Adversary Personas, which had really encouraged unbounded thinking, it was hard to engage with these cards at first. With the above one, for example, it lists quite a lot of the potential answers, which doesn't feel very motivating to come up with more.

The [activities](http://securitycards.cs.washington.edu/activities.html) for these cards are different to the other two sets and they can also be used for education rather than for securing a particular system. It seemed like they might prompt good ideas for a group less familiar with security concepts, and we did generate quite a few potential issues from them.

## Which cards generated more insights?

When coming together and looking across the three groups at the end of the session, the interesting thing was that each deck of cards, regandless of the group or the order, had generated roughly the same number of black dots, i.e. important security issues to address.

However, in all groups, the Adversary Personas had generated the most red dots, i.e interesting issues raised.

## I would definitely want to use a deck of cards

I found this exercise really interesting. All of the decks of cards prompted the group to think outside our default ways of thinking, so I would advocate using a deck of cards as a supplement to any threat modelling session I was doing.

Which deck I would want to use would depend on the context, e.g. the technical understanding of those taking part, what other methods we were using, whether the priority of the session was to identify new risks or gain a collective understanding, etc.

Other security cards are available, for example [protection poker](https://opensource.com/article/19/3/protection-poker-agile-security-game).

And other threat modelling methods are also available! This [a useful summary](https://insights.sei.cmu.edu/blog/threat-modeling-12-available-methods/).

Charles, Lucy and Shamal plan to write up a more detailed blog post with the outcome of the session, which I look forward to reading.

## Go to SPA!

And [SPA conference](https://www.spaconference.org/) is still going on, until Friday this week, with lots of great sessions still to come. You can [get a free ticket here](https://www.eventbrite.co.uk/e/spa-conference-2021-tickets-155925821329?discount=SCHOLARSHIP2021).
