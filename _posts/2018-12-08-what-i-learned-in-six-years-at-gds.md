---
anchor_id: high-output
title: What I learned in six years at GDS
layout: blog_post
---
When I joined the Government Digital Service in April 2012, <a href="https://www.gov.uk/">GOV.UK</a> was just going into public beta. GDS was a completely new organisation, part of the Cabinet Office, with a mission to stop wasting government money on over-complicated and underperforming big IT projects and instead deliver simple, useful services for the public.

<p>Lots of people who were experts in their fields were drawn in by this inspiring mission, and I learned loads from working with some true leaders. Here are three of the main things I learned.</p>
<h2>1. What is the user need?</h2>
<p> The main discipline I learned from my time at GDS was to always ask ‘what is the user need?’ It’s very easy to build something that seems like a good idea, but until you’ve identified what problem you are solving for the user, you can’t be sure that you are building something that is going to help solve an actual problem.</p>
<p>A really good example of this is GOV.UK Notify. This service was originally conceived of as a status tracker; a “where’s my stuff” for government services. For example, if you apply for a passport online, it can take up to six weeks to arrive. After a few weeks, you might feel anxious and phone the Home Office to ask what’s happening. The idea of the status tracker was to allow you to get this information online, saving your time and saving government money on call centres.</p>
<p>The project started, as all GDS projects do, with a <a href="https://www.gov.uk/service-manual/agile-delivery/how-the-discovery-phase-works">discovery</a>. The main purpose of a discovery is to identify the users’ needs. At the end of this discovery, the team realised that a status tracker wasn’t the way to address the problem. As they wrote in <a href="https://gds.blog.gov.uk/2015/10/05/status-tracking-making-it-easy-to-keep-users-informed/">this blog post</a>: </p>
<div class="quote">
<p>Status tracking tools are often just ‘channel shift’ for anxiety. They solve the symptom and not the problem. They do make it more convenient for people to reduce their anxiety, but they still require them to get anxious enough to request an update in the first place.</p>
</div>
<p>What would actually address the user need would be to give you the information before you get anxious about where your passport is. For example, when your application is received, email you to let you know when to expect it, and perhaps text you at various points in the process to let you know how it’s going. So instead of a status tracker, the team built <a href="https://www.notifications.service.gov.uk/">GOV.UK Notify</a>, to make it easy for government services to incorporate text, email and even letter notifications into their processes.</p>
<h3>Making sure you know your user</h3>
<p>At GDS user needs were taken very seriously. We had a user research lab on site and everyone was required to spend two hours observing user research every six weeks. Ideally you’d observe users working with things you’d built, but even if they weren’t, it was an incredibly valuable experience, and something you should seek out if you are able to.</p>
<p>Even if we think we understand our users very well, it is very enlightening to see how users actually use your stuff. Partly because in technology we tend to be power users and the average user doesn’t use technology the same way we do. But even if you are building things for other developers, someone who is unfamiliar with it will interact with it in a way that may be very different to what you have envisaged.</p>
<h3>User needs is not just about building things</h3>
<p>Asking the question “what is the user need?” really helps focus on why you are doing what you are doing. It keeps things on track, and helps the team think about what the actual desired end goal is (and should be). </p>
<p>Thinking about user needs has helped me with lots of things, not just building services. For example, you are raising a pull request. What’s the user need? The reviewer needs to be able to easily understand what the change you are proposing is, why you are proposing that change and any areas you need particular help on with the review. </p>
<p>Or you are writing an email to a colleague. What’s the user need? What are you hoping the reader will learn, understand or do as a result of your email?</p>
<h2>2. Make things open: it makes things better</h2>
<p>The second important thing I learned at GDS was ‘make things open: it makes things better’. This works on many levels: being open about your strategy, blogging about what you are doing and what you’ve learned (including mistakes), and – the part that I got most involved in – coding in the open.</p>
<h3>Talking about your work helps clarify it</h3>
<p>One thing we did really well at GDS was blogging – a lot – about what we were working on. Blogging about what you are working on is is really valuable for the writer because it forces you to think logically about what you are doing in order to tell a good story. If you are blogging about upcoming work, it makes you think clearly about why you’re doing it; and it also means that people can comment on the blog post. Often people had really useful suggestions or clarifying questions.</p>
<p>It’s also really valuable to blog about what you’ve learned, especially if you’ve made a mistake. It makes sure you’ve learned the lesson and helps others avoid making the same mistakes. As well as blogging about lessons learned, GOV.UK also publishes <a href="https://insidegovuk.blog.gov.uk/category/incident-reports/">incident reports</a> when there is an outage or service degradation. Being open about things like this really engenders an atmosphere of trust and safe learning; which helps make things better.</p>
<h3>Coding in the open has a lot of benefits</h3>
<p>In my last year at GDS I was the Open Source Lead, and one of the things I focused on was the <a href="https://www.gov.uk/service-manual/service-standard/make-all-new-source-code-open">requirement that all new government source code should be open</a>. From the start, GDS coded in the open (the GitHub organisation still has the non-intuitive name <a href="https://github.com/alphagov/">alphagov</a>, because it was created by the team doing the original Alpha of GOV.UK, before GDS was even formed).</p>
<p>When I first joined GDS I was a little nervous about the fact that anyone could see my code. I worried about people seeing my mistakes, or receiving critical code reviews. (Setting people’s mind at rest about these things is why it’s crucial to have good standards around communication and positive behaviour - even a critical code review should be considerately given). </p>
<p>But I quickly realised there were huge advantages to coding in the open. In the same way as blogging your decisions makes you think carefully about whether they are good ones and what evidence you have, the fact that anyone in the world could see your code (even if, in practice, they probably won’t be looking) makes everyone raise their game slightly. The very fact that you know it’s open, makes you make it a bit better.</p>
<p>It <a href="https://gds.blog.gov.uk/2017/09/04/the-benefits-of-coding-in-the-open/">helps with lots of other things as well</a>, for example it makes it easier to collaborate with people and share your work. And now that I’ve left GDS, it’s so useful to be able to look back at code I worked on to remember how things worked.</p>
<h3>Share what you learn</h3>
<p>It’s sometimes hard to know where to start with being open about things, but it gets easier and becomes more natural as you practice. It helps you clarify your thoughts and follow through on what you’ve decided to do. Working at GDS when this was a very important principle really helped me learn how to do this well.</p>
<h2>3. Do the hard work to make it simple (tech edition)</h2>
<p>‘Start with user needs’ and ‘Make things open: it makes things better’ are two of the excellent <a href="https://www.gov.uk/guidance/government-design-principles">government design principles</a>. They are all good, but the third thing that I want to talk about is number 4: ‘Do the hard work to make it simple’, and specifically, how this manifests itself in the way we build technology.</p>
<p>At GDS, we worked very hard to do the hard work to make the code, systems and technology we built simple for those who came after us. For example, writing good commit messages is taken very seriously. There is <a href="https://github.com/alphagov/styleguides/blob/master/git.md">commit message guidance</a>, and it was not unusual for a pull request review to ask for a commit message to be rewritten to make a commit message clearer.</p>
<p>We worked very hard on <a href="https://www.annashipman.co.uk/jfdi/good-pull-requests.html">making pull requests good</a>, keeping the reviewer in mind and making it clear to the user how best to review it.</p>
<p>Reviewing others’ pull requests is the highest priority so that no-one is blocked, and teams have screens showing the status of open pull requests (using <a href="https://github.com/alphagov/fourth-wall">fourth wall</a>) and we even had a ‘<a href="https://gdstechnology.blog.gov.uk/2015/09/24/reminding-developers-about-code-reviews/">pull request seal</a>’, a bot that publishes pull requests to Slack and gets angry if they are uncommented on for more than two days.</p>
<h3>Making it easier for developers to support the site</h3>
<p>Another example of doing the hard work to make it simple was the opsmanual. I spent two years on the web operations team on GOV.UK, and one of the things I loved about that team was the huge efforts everyone went to to be open and inclusive to developers.</p>
<p>The team had some people who were really expert in web ops, but they were all incredibly helpful when bringing me on board as a developer with no previous experience of web ops, and also patiently explaining things whenever other devs in similar positions came with questions. </p>
<p>The main artefact of this was the opsmanual, which contained write-ups of how to do lots of things. One of the best things was that every alert that might lead to someone being woken up in the middle of the night had a link to documentation on the opsmanual which detailed what the alert meant and some suggested actions that could be taken to address it.</p>
<p>This was important because most of the devs on GOV.UK were on the on-call rota, so if they were woken at 3am by an alert they’d never seen before, the opsmanual information might give them everything they needed to solve it, without the years of web ops training and the deep familiarity with the GOV.UK infrastructure that came with working on it every day.</p>
<h3>Developers are users too</h3>
<p>Doing the hard work to make it simple means that users can do what they need to do, and this applies even when the users are your developer peers. At GDS I really learned how to focus on simplicity for the user, and how much better this makes things work.</p>
<h2>These three principles help us make great things</h2>
<p>I learned so much more in my six years at GDS. For example, the civil service has a <a href="https://www.annashipman.co.uk/jfdi/interviewing-fairly.html">very fair way of interviewing</a>. I learned about the <a href="https://russelldavies.typepad.com/planning/2015/06/doing-the-hard-work-to-make-it-clear.html">importance of good comms</a>, <a href="https://dan.carley.co/blog/2014/05/21/working-late-responsibly/">working late, responsibly</a> and the value of <a href="https://contentdesign.london/book/">content design</a>.</p>
<p>And the real heart of what I learned, the guiding principles that help us deliver great products, is encapsulated by the three things I’ve talked about here: think about the user need, make things open, and do the hard work to make it simple.</p>
<p><em>This post originally appeared on <a href="https://24ways.org/2018/what-i-learned-in-six-years-at-gds/">24ways</a></em>.</p>