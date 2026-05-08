---
anchor_id: exec-ai-principles
title: "Three AI principles every exec leader needs to understand"
tags: [Leadership, Technology]
layout: blog_post
---

*It's no longer defensible for CEOs and boards to outsource understanding AI to their technology execs. I partnered with [CxAI on a post about the three key principles](https://cxai100.substack.com/p/72221c8f-af37-46e7-a63e-b3c52512edc4) that will enable execs to build that understanding. The post is below.*

This week, we’re shifting gears.

Not to what AI can do for consumers and businesses, but to a more uncomfortable question: as an executive or board member, are you asking the right questions about AI?

Executives are approving budgets, signing vendor contracts, and sitting through AI strategy briefings. Yet in the UK, [only 9% of businesses have actually adopted AI](https://www.gov.uk/government/publications/ai-adoption-research/ai-adoption-research) in any meaningful way (see our [last post](https://cxai100.substack.com/p/spooking-the-markets) for details). And according to [Deloitte](https://www.deloitte.com/global/en/issues/trust/progress-on-ai-in-the-boardroom-but-room-to-accelerate.html), 66% of boards have little to no knowledge of the technology they are asked to fund.

<img src="/img/board_literacy_chart.jpg" alt="" style="max-width: 100%; height: auto; display: block; border: 0;">

There’s a gap between sponsoring AI and understanding it and that gap can be expensive.

Before strategy, before tooling, before any budget is spent, there’s one skill that separates executives who lead AI initiatives from those who just fund them: knowing what to ask.

For this post, we partnered with [Anna Shipman](https://www.linkedin.com/in/annashipman/), a Chief Technology Officer with 20+ years delivering technology strategy, including at the Financial Times, the Government Digital Service, and most recently at Kooth, an AIM-listed Digital Health company. She writes about technology and leadership in her blog so subscribe if you find this interesting.

*(Skip to the end if you want to see Anna’s top questions to ask)*

## What AI literacy actually means at the executive level

It doesn’t mean getting a computer science degree. It doesn’t mean taking classes or tracking every product launch. The pace of AI development makes that impossible, and that’s not your job.

What it does mean is understanding the principles that govern how this technology works, well enough to govern responsibly, challenge assumptions, and ask the questions your organisation can’t afford to skip.

Anna identifies three principles she considers non-negotiable for any executive making AI decisions today:

- **AI is non-deterministic**: you’re managing probabilities, not certainties
- **The economics have flipped**: it’s no longer about what you build, but what you buy and what that costs you long-term
- **Competitive advantage is in integration**: how you embed AI matters far more than which AI you use

## 1. AI is non-deterministic

The AI systems most companies are deploying today operate on statistical representations of language rather than grounded semantics. They don’t truly understand meaning or “know” things the way humans do. They are sophisticated, powerful pattern-matching engines, trained on historical data, that generate plausible outputs based on patterns they’ve seen before. Furthermore, those outputs will differ every time, even with identical inputs, because AI is non-deterministic.

The implications of this are significant:

- **They can’t distinguish between truth and convincing-sounding fiction.** AI systems are prone to hallucination, confidently generating plausible-sounding but inaccurate or fabricated information. Hallucination rates vary significantly by industry and use case. It is possible to improve accuracy by employing checks and including more training data however these all come with significantly increased cost.

<img src="/img/hallucination_rates.png" alt="" style="max-width: 100%; height: auto; display: block; border: 0;">

- **Bias is coded into the system.** Training data reflects historical patterns, including discriminatory ones. AI will reproduce and amplify these patterns with confidence.
- **They don’t predict unprecedented situations.** Models trained on historical fraud data, for example, will miss novel fraud techniques.

This is a feature of how the technology works, not a bug that will eventually be fixed. It is possible to improve accuracy with more training data, better fine-tuning and human review but these improvements come with significantly increased cost. You can’t eliminate AI errors entirely. You can only decide the level of uncertainty your business is prepared to tolerate.

Here’s the mindset shift that matters:

**Traditional software is deterministic**. If your input is X, your output will always be Y. Code quality, testing, and QA aim to eliminate bugs entirely. You release software when it’s “done.”

**AI is probabilistic**. If your input is X, your output will probably be Y, with a confidence level of Z. You release when the error rate is at a level your business can tolerate. A model that’s 95% accurate might transform your fraud detection, be catastrophic for medical diagnosis, or be perfectly acceptable for customer service FAQs, depending entirely on the cost of being wrong.

**Risk tolerance is a strategic decision**. Governance of that risk is essential and regulation is catching up as the EU AI Act and emerging frameworks require demonstrable oversight. Note also that [Article 4 of the EU AI Act](https://digital-strategy.ec.europa.eu/en/faqs/ai-literacy-questions-answers) requires providers and deployers of AI systems to ensure a sufficient level of AI literacy among the people working with those systems on their behalf.

## 2. The economics have flipped

AI costs are now more like running a factory than buying software, continuous operational costs, not a fixed asset that depreciates.

Traditional software is typically modelled as high upfront build costs, low ongoing maintenance, with marginal costs approaching zero as you scale.

AI needs constant tending. While traditional [software degrades](https://en.wikipedia.org/wiki/Software_rot) gradually over time due to technical debt and advances in technology, the maintenance required for AI is far more active:

- **Models drift.** Performance erodes continuously without intervention. The world changes, but your model was trained on old data. Fraud patterns evolve. Customer preferences shift. Language changes.
- **Data drifts.** The data you feed the model in production starts looking different from training data.
- **The underlying concept drifts.** The relationship you’re modelling changes. A pandemic, for example, disrupted all retail forecasting models overnight.

AI models carry ongoing operational costs that scale with usage (compute and tokens), plus active maintenance, plus vendor dependency.

Given these costs, you might think building your own models makes sense. But foundation models have fundamentally changed the build-vs-buy debate. Prior to 2022, companies built proprietary models for competitive advantage. Now we have foundation models such as GPT-4, Claude Opus and Gemini, large-scale AI models trained on massive datasets that provide general-purpose capabilities out of the box. Training a frontier model now typically requires tens to hundreds of millions of dollars in compute, data, and specialised talent. [GPT-4 alone is estimated to have cost over $100M to train](https://aisuperior.com/cost-of-training-llm-from-scratch/); Gemini Ultra approached $200M. By contrast, [adapting existing models through fine-tuning](https://galileo.ai/blog/llm-model-training-cost) can cost from a few hundred to a few thousand dollars for many use cases, often reducing costs by 60–90%.

However, this creates a different problem, namely ongoing operational costs and strategic dependency on model vendors who control pricing. Once you’ve built critical operations around their models, switching becomes prohibitively expensive and vendors know it. The pricing you see today reflects the land-grab phase. This creates a different class of risk with ongoing operational cost exposure and structural dependency on model vendors. CloudZero’s 2025 [State of AI Costs](https://www.cloudzero.com/state-of-ai-costs/) report highlights how organisations are rapidly increasing AI spend yet only around half can confidently measure ROI. Once core workflows are built around external models, switching costs kick in and businesses are exposed to cost volatility, opaque pricing models, and expanding usage-based spend. With spend in some cases rivalling traditional Engineering organisation expenditure, effective governance of AI operating costs is essential.

## 3. Competitive advantage is in integration

GPT-4, Claude, and Gemini are available to everyone. Most AI capabilities are “commoditising” rapidly, improving for all players at roughly the same pace. The technology itself isn’t your moat.

Yet for many organisations, the response looks something like this:

<img src="/img/ceos_ai.jpg" alt="'Who are we?', 'CEOs', 'What do we want?', 'AI!', 'AI to do what?', 'We don't know!', 'When do we want it?', 'Right now!'" style="max-width: 100%; height: auto; display: block; border: 0;">

Competitive advantage will come from where AI is embedded in your organisation and how well you integrate it.

**Data matters, but is unlikely to be your moat on its own.** As we covered in [a previous post on data strategy](https://cxai100.substack.com/p/how-data-unlocks-ai-success), clean, structured, accessible data is a prerequisite for AI to work at all. How intentionally you design your data integration will be a significant driver of competitive advantage. [A compelling example is Walmart](https://www.linkedin.com/feed/update/urn:li:activity:7441536404297449472/), who have invested in building a semantic layer over their own proprietary data creating a more defensible moat rather than simply plugging into ChatGPT.

**Advantage sits at the application and organisational layer.** Which workflows you redesign, which decisions you automate, how you integrate AI into day-to-day operations, how quickly you learn and iterate. This is where the real gains are made. The biggest wins often come from changing your operating model entirely.

**Human-in-the-loop beats full automation for most use cases.** AI [can make individuals 30–50% more productive on certain tasks](https://newsroom.ibm.com/2025-10-28-Two-thirds-of-surveyed-enterprises-in-EMEA-report-significant-productivity-gains-from-AI,-finds-new-IBM-study), but human-AI collaboration consistently outperforms either on their own. Humans can catch AI errors, while AI can scale human expertise combining forces to produce better results in what is termed *diagnostic complementarity* in [this study](https://link.springer.com/article/10.1007/s13347-025-00886-5). It’s worth noting that a decade on from Geoff Hinton’s infamous prediction that AI would eliminate radiologists entirely, [there are more radiologists than ever](https://www.forbes.com/sites/jonmarkman/2026/01/26/the-radiologist-effect-why-ai-creates-more-jobs-not-fewer/).

We’ve heard from many CTOs that even where the speed of coding has been significantly accelerated, overall productivity hasn’t necessarily followed because coding was never the bottleneck. The organisations that will win are [those who understand where their own velocity is actually constrained](https://jellyfish.co/blog/harvard-jellyfish-ai-is-making-developers-faster/), and can align speed, governance, and learning accordingly.

Without intentional integration, AI will simply amplify the organisation you already have. It will not fix structural dysfunction.

## Understanding AI is no longer optional

In the past, CEOs and board members could delegate understanding of these issues to their technology executives. [This is no longer an option](https://www.egonzehnder.com/functions/technology-officers/insights/do-boards-need-a-qualified-tech-expert).

<div class="quote">
“While most directors aren’t expected to be technology experts, they must understand the material issues technology and innovation raise for their companies.”
</div>

Fortunately, it’s now easier than ever to build this basic understanding with literacy by using AI itself to help you learn.

Start with these questions, that Anna has set out below, get real answers and you’ll govern AI investments with the same rigour you apply to everything else.

## The questions to ask by principle

### 1. AI is non-deterministic: you're managing probabilities, not certainties

*Proposed investments* What's the acceptable error rate, and can this system deliver it? What's our fallback when the AI is wrong? What does accuracy improvement cost – is the business case still viable?

*Accuracy claims* How is accuracy being measured, and does it align with business impact? (Overall accuracy can hide catastrophic failures in edge cases)

*Deployment & operations* 
What's our process for monitoring accuracy over time? How often will we retrain the model, and who owns that? Do we have human review in place for high-stakes decisions?

*Bias & fairness* What's in the training data – does it encode historical discrimination? If this system disadvantages a protected group, can we show we took steps to prevent that?

*Accountability* Who owns this system end-to-end — not just deployment, but when it fails? If regulators ask us to explain an AI decision, can we? What's the incident response plan if this fails publicly?

*Vendor relationships* What visibility do we have into how third-party AI works and what biases it contains? What's our recourse if their model produces discriminatory outputs under our brand?

### 2. AI costs are variable and unpredictable – your financial models need to adapt

*Vendor dependency* What happens if our AI vendor increases pricing 3x? Have we modelled that scenario? Are we locked into this vendor, or do we have realistic alternatives?

*Model drift* What’s our process for monitoring when model performance degrades? How often will we need to retrain or update models, and have we budgeted for that?

*Strategic reality* What happens to unit economics if usage grows 50x? In 2–3 years, could AI operational costs rival engineering headcount costs?

*Workforce choices* Have we made a deliberate choice — growth ambition or cost optimisation? Does the people strategy align with our business objectives?

*Team capability* What skills do we need more of, and what skills become less critical? Are we investing in training existing teams, or assuming AI replaces expertise?

### 3. AI doesn't create competitive advantage, your data and execution speed do

*Competitive positioning* Given competitors have the same foundation models, where specifically does this create advantage for us?

*Data as differentiator* Is our data genuinely unique at scale, or table stakes everyone in our industry has? Have we invested in data infrastructure to actually use this data?

*Organisational velocity* Where is our organisation genuinely constrained by legacy systems vs. slowed by bureaucracy? What would it take to create a team that moves at startup speed while maintaining core systems?

*Execution vs. technology* How does our speed of iteration compare to competitors? Can we ship, learn, and improve faster?
