---
anchor_id: benefits-coding-open
title: The benefits of coding in the open
tag: Open source
layout: blog_post
---

<p>For any service to be put in front of the public, it has to meet the Digital Service Standard, a set of 18 criteria.</p>
<p>One of the criteria is that all new source code is <a href="https://www.gov.uk/service-manual/service-standard/make-all-new-source-code-open">made open and published under an open source licence</a>.</p>
<p>This goes hand in hand with our tenth design principle: <a href="https://www.gov.uk/design-principles#tenth">make things open: it makes things better</a>.</p>
<p>In this blog post, I explain why coding in the open makes things better.</p>

<p><img src="/img/coding-in-the-open.jpg" alt="two developers in front of a screen with code on it" /></p>
<h2><b>It encourages good practice</b></h2>
<p>When you know someone is watching, you tend to take greater care. You're more inclined to document your work clearly. You make sure your code is secure by keeping secrets separate from the code. You are polite and constructive in code reviews, and you follow good architectural principles.</p>
<p>In short: when other people can see your work, you tend to raise your game.</p>
<h2><b>It makes collaboration easier</b></h2>
<p>If code is open, it is easier to work on it with others. You don't need to give them special access or make complicated business arrangements. You don't even need to be in the same building.</p>
<p>For example, someone from 18F, the government agency that provides digital services to the government of the United States, was able to <a href="https://gdstechnology.blog.gov.uk/2017/07/18/coding-in-the-open-makes-better-code/">help a colleague from GDS with a code-writing problem</a>.</p>
<p>It worked because both sides coded in the open. We also <a href="https://governmenttechnology.blog.gov.uk/2016/09/06/celebrating-sharing-and-reusing-the-digital-marketplace/">worked with the Australian Government</a> to help them establish their own Digital Marketplace.</p>
<p>Closer to home, it makes it easier to work on the same code between departments.</p>
<h2><b>External users can help make it better</b></h2>
<p>Open code makes it possible for people who don’t work for you to make improvements to your code.</p>
<p>For example, members of the public made improvements to the <a href="https://petition.parliament.uk/">Government Petitions Service.</a> Someone <a href="https://github.com/alphagov/e-petitions/pull/456">added the scheduled date</a> for debates. Someone else made a change to the signature counter to <a href="https://github.com/alphagov/e-petitions/pull/482">make it update in real time</a>.</p>
<p>People can 'scratch their own itches'. They can make the small improvements that aren't at the top of your list of priorities, and they can help make your code more robust.</p>
<h2><b>Others can learn from your work</b></h2>
<p>If your code is open, people can apply what you've learned from doing the work.</p>
<p>Skills Funding Agency used GOV.UK's Smart Answers code to <a href="https://sfadigital.blog.gov.uk/2016/11/17/when-build-a-thing-really-works/">build a tool for their apprenticeships service</a>. It took less than a week.</p>
<p>Without the Smart Answers example to learn from, it would have taken at least two months.</p>
<h2><b>It makes it easier to share standards</b></h2>
<p>Open code makes it easy to follow other teams’ work. This promotes a common culture and way of working when you can see how other teams manage certain issues.</p>
<img src="/img/Anna-Shipman-768x512.jpg" alt="Anna Shipman and another member of GDS staff" />
<p>Quite often, teams will make small improvements to other teams’ work. For example, a developer from GOV.UK <a href="https://github.com/alphagov/verify-frontend/pull/255">made a correction to GOV.UK Verify</a>.</p>
<p>GOV.UK publishes <a href="https://github.com/alphagov/styleguides/">coding style guides.</a> This makes it easy for everyone to find and stick to the same standards.</p>
<h2><b>It improves transparency on government’s work</b></h2>
<p>When code is developed in the open, you can see where public money goes.</p>
<p>It is a catalyst which encourages openness in other things. For example, the <a href="https://insidegovuk.blog.gov.uk/2017/02/13/the-2017-to-2018-gov-uk-roadmap/">GOV.UK roadmap is open</a>, and one of the teams on GOV.UK uses a <a href="https://trello.com/b/7yWk0jhI/govuk-publishing-platform-tap-support-planning">public Trello board</a>.</p>
<p>When there is an occasional outage on GOV.UK we investigate and <a href="https://insidegovuk.blog.gov.uk/category/incident-reports/">publish a report</a>. It’s important to show how we learn from mistakes.</p>
<h2><b>It clarifies ownership</b></h2>
<p>We want government to own and be able to make changes to its services, and lack of clarity on intellectual property (IP) can be a barrier to that.</p>
<p>Open coding from the beginning surfaces copyright and IP issues before work starts.</p>
<p>The Service Standard demands that code is published under an open source licence (<a href="https://github.com/alphagov/styleguides/blob/master/licensing.md">at GDS we use MIT</a>). Additionally, all the work we do as civil servants is Crown copyright.</p>
<p>In the past, government services have wanted to change a project but have been unclear about who owns the IP.</p>
<p>Clarifying the issue upfront is valuable. It means that departments can bring in a supplier to work on their alpha and then switch to another supplier for beta without losing their work.</p>
<p>They can even build up teams from many suppliers who can work on the code seamlessly.</p>
<p>It prevents supplier lock-in. Without clarification, the software created for you can be the thing that will prevent you from switching suppliers.</p>
<p>So resolving this can save a lot of money for government.</p>
<h2><b>It helps make government technology seamless</b></h2>
<p>People who move between departments can continue to work using the same tools as before. It saves time and money. They can share knowledge of projects they were working on, because it’s all open.</p>
<p>After someone moved from GDS to another department, they <a href="https://github.com/alphagov/signon/pull/509">contributed to our single sign-on service</a>.</p>
<p>Over time, it will make government technology seamless as people move towards the most useful tools.</p>
<h2><b>It’s easier to code in the open than to open a closed repository</b></h2>
<p>Coding in the open means you decide whether that code is suitable for publication as part of reviewing each small piece of work.</p>
<p>To open it later means having to go back through a body of work that has built up over time to make sure there is nothing that shouldn’t be made public, which can be significant extra work. </p>
<h2><b>Make your own code open</b></h2>
<p>Many people think that being able to reuse code is the biggest benefit of coding in the open. However, while reuse is a nice-to-have, I hope this blog post illustrates that there’s more to it than that.</p>
<p>Take a look at <a href="https://github.com/alphagov/">our open code</a> and our <a href="https://www.gov.uk/service-manual/technology/making-source-code-open-and-reusable">guidance.</a></p>
<p><em>This post originally appeared on the <a href="https://gds.blog.gov.uk/2017/09/04/the-benefits-of-coding-in-the-open/">GDS blog</a></em>.</p>
