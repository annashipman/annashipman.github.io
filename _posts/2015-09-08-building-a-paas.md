---
anchor_id: building-paas
title: Building a platform to host digital services
layout: blog_post
---

 <p>Right now, hosting services is one of the most time-consuming barriers for
new digital services, and usually involves duplicating work done elsewhere. On
the Government Platform as a Service team we’re working on solving that.<span
id="more-19788"></span></p>
<h2>Repetition, repetition, repetition</h2>
<p>Every digital service that government runs needs to have a place to run from;
it <a href="https://en.wikipedia.org/wiki/Web_hosting_service">needs to be
hosted somewhere</a> so that it is accessible to users via the internet. The
service doesn’t ‘just work’; there is a lot of effort involved in setting up all
the components required to host a service.</p>
<p>These components don’t vary much between services. Every service needs an
automated way to let developers know when something is wrong, or to alert them
to something. So, in practice, these groups of components end up looking very
similar across very different services. The picture below shows you an
example:</p>
<p><img src="/img/Separate-projects-image.jpg" alt="image showing three projects with the same technical stack, including alerting, monitoring, logging, each running on a cloud provider" /></p>
<p>As you can tell, there’s a lot of duplication. Teams all over government can
end up duplicating work that’s already been done elsewhere. That means spending
time on areas that aren’t their speciality, such as application monitoring or
log aggregation, which stops teams from focusing on their areas of
expertise.</p>
<p>It also leads to a lot of time searching for people with expertise in this
area to hire. All of this takes time and money and leaves teams less time to
focus on their users’ needs.</p>
<p>One way to address these issues is to provide a <a
href="https://en.wikipedia.org/wiki/Platform_as_a_service">platform as a
service</a> (PaaS) that services could use for their cloud hosting. A shared
PaaS would then change the diagram above into something more like the one
below:</p>
<p><img src="/img/Government-PaaS-Image.jpg" alt="image showing three projects, each running on Government PaaS, which has a technical stack including alerting, monitoring, and logging, and running on three different cloud providers" /></p>
<p>A Government PaaS wouldn’t just solve the issue of duplication, and where to
focus your teams. One thing that takes a lot of time in government is procuring
commercial services and making sure they are accredited. If we could do that
once, for the PaaS, then that could save service teams a great deal of time,
while making sure that those aspects are being handled in the correct way.</p>
<h2>What a Government PaaS needs</h2>
<p>From the user research we’ve been doing it’s clear that it’s important that
<a href="http://whatis.techtarget.com/definition/multi-tenancy">our platform has
a concept of multi-tenancy</a> - applications that run on the platform should be
isolated from each other and not be able to read or change each others’ code,
data or logs. It wouldn’t be appropriate, for example, if the Digital
Marketplace application was able to access the data of the GOV.UK publishing
platform.</p>
<p>We’ve also learned from our experience supporting GOV.UK that a platform
where the <a href="http://www.infoq.com/presentations/gov-uk-devops">people
developing applications also support the application out of hours</a> leads to
better software and a better user experience. We want a platform that supports
this model right from the beginning.</p>
<p>Apart from multi-tenancy and the support model, there are some other things
that we feel are important in a shared PaaS.</p>
<p><strong>It needs to be self-service</strong>. It needs to be easy and quick
for application teams to get started, and the teams using the platform need to
be able to make frequent changes. That means we need to make sure applications
can be deployed and managed by the application teams, but also that they can
make other administrative changes to their applications, for example configuring
DNS. Allowing teams complete control of their applications will remove any
unnecessary delays for them, and means the platform team can focus exclusively
on iterating and improving the platform itself.</p>
<p><strong>It needs to run on multiple public clouds</strong>. This approach
ensures that we avoid being locked into a single provider, so we encourage price
competition, while also removing the risk of a <a
href="https://en.wikipedia.org/wiki/Single_point_of_failure">single point of
failure</a>. Changing infrastructure providers is very difficult to do if you’ve
built to a single provider’s specification so this needs to be built in from the
beginning.</p>
<h2>What we've been doing</h2>
<p>We’ve spent a couple of months exploring what a Government PaaS might look
like and how it could help teams running digital services across government.
We’ve spoken to many potential users, and we’ve worked closely with our
colleagues in other departments who are working to address similar problems, and
we’ve found that no existing departmental solution meets all the needs we’ve
identified.</p>
<p>We’ve evaluated several open source and commercial options, and we’ve built a
prototype and shown it to potential users – developers, web operations engineers
and services managers – both within GDS and in other departments. We’ve tested
our prototype by seeing how it works with real applications (for example, we
tested it using <a href="https://www.digitalmarketplace.service.gov.uk/">Digital
Marketplace</a> and GOV.UK’s <a
href="https://github.com/alphagov/government-frontend">Government
Frontend</a>).</p>
<p>We’ll write about all of this more in later blog posts.</p>
<h2>What we're doing next</h2>
<p>We expect to be in alpha until the end of November, by which time we will
have completed a detailed comparison of two open source PaaS technologies and
addressed issues around performance, security, and scalability, for example. We
are really interested in talking to more potential users, so if you are
interested in getting involved in our user research, or seeing a demo of what
we’ve done so far, please get in touch.</p>

*This post originally appeared on the [GDS
Blog](https://gds.blog.gov.uk/2015/09/08/building-a-platform-to-host-digital-services/)*.
