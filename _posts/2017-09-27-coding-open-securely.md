---
anchor_id: coding-open-securely
title: Don’t be afraid to code in the open&#58; here’s how to do it securely
tag: Open source
layout: blog_post
---

There are two big concerns government organisations have around <a href="https://www.gov.uk/service-manual/service-standard/make-all-new-source-code-open">making source code open</a>. They want to know which subsets of the code should be kept closed and how to code in the open securely. To address these questions I’ve introduced two pieces of guidance:
<ul>
<li><a href="https://gov.uk/government/publications/open-source-guidance/when-code-should-be-open-or-closed">'When code should be open or closed'</a></li>
<li><a href="https://gov.uk/government/publications/open-source-guidance/security-considerations-when-coding-in-the-open">'Security considerations when coding in the open'</a></li>
</ul>

<p>Both pieces of guidance are based on industry standards and have been reviewed by the GDS security engineering team as well as government colleagues from National Cyber Security Centre, Department for Work and Pensions, Home Office and Ministry of Justice.</p>
<h2>Why we have updated the guidance</h2>
<p>We previously blogged about what code not to open in our post: '<a href="https://gds.blog.gov.uk/2014/10/08/when-is-it-ok-not-to-open-all-source-code/">When is it ok not to open all source code?</a>', but as guidance, it is no longer relevant as our approach to specific areas such as configuration have changed. For example, last year we made <a href="https://gdstechnology.blog.gov.uk/2016/01/19/opening-gov-uks-puppet-repository/">GOV.UK's Puppet repository</a> publically available on GitHub.<p>
<p>We’ve also <a href="https://gdstechnology.blog.gov.uk/2016/07/13/why-security-says-no-wont-cut-it-anymore/">evolved our thinking on security</a>. The previous guidance discouraged people from sharing code that had anything at all to do with security. It didn’t take into account that coding in the open can actually make code more robust as it helps you design with security in mind.</p>
<p>The new guidance addresses why open sourcing code that performs a security-enforcing function is beneficial. In simple terms, we can compare coding in the open to how padlocks work. Everyone knows how padlocks work but they are still secure because you cannot open them without the key. <a href="https://en.wikipedia.org/wiki/RSA_(cryptosystem)">Security enforcing software works in the same way</a>, and good cryptographic algorithms are reviewed by many professional peers. Security is improved through public review.</p>
<p>We still specifically seek peer review on open code and subject our code to penetration testing, as part of following <a href="https://www.ncsc.gov.uk/guidance/security-design-principles-digital-services-main">security design principles</a>.</p>
<h2>What we’re doing at GDS</h2>
<p>Most of the code produced by GDS has been coded in the open from the beginning. Some services started closed source, and to ensure that we are practicing what we preach, we are now opening those: we have recently completed open sourcing <a href="https://govukpay-docs.cloudapps.digital/#contribute">GOV.UK Pay</a> and we are working on opening up more components of <a href="https://github.com/alphagov/verify-frontend/">GOV.UK Verify</a>. </p>
<p>This new guidance will make it easier for your organisation to develop and deploy secure and open services, and should address your concerns around coding in the open securely.</p>
<p><em>This post originally appeared on the <a href="https://gdstechnology.blog.gov.uk/2017/09/27/dont-be-afraid-to-code-in-the-open-heres-how-to-do-it-securely/">GDS technology blog</a></em>.</p>
