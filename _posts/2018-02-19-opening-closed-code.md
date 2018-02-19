---
anchor_id: open-closed-code
title: How to open up closed code
layout: blog_post
---

Every digital service designed within government has to meet the <a href="https://www.gov.uk/service-manual/service-standard">Digital Service Standard</a>. One of the requirements of the standard is that new source code should be <a href="https://www.gov.uk/service-manual/service-standard/make-all-new-source-code-open">made open and published under an open source licence</a>.

<p>There are a few situations where it’s acceptable to <a href="https://www.gov.uk/government/publications/open-source-guidance/when-code-should-be-open-or-closed">keep code closed</a> but in most cases it will need to be open.</p>
<p>The easiest way to make code public is to write the code in the open from the beginning, and I’ve <a href="https://gds.blog.gov.uk/2017/09/04/the-benefits-of-coding-in-the-open/">previously blogged about the benefits of doing this</a>.</p>
<p>Your team may have old closed code that it needs to open. If there is a lot of closed code, this can be challenging. Here are 3 ways to open it up.</p>
<h2><strong>Option 1: Cycle all credentials then open it</strong></h2>
<p>The commit history is a <a href="https://mislav.net/2014/02/hidden-documentation/">very useful part of a codebase</a> as it explains the reasoning behind changes. If your team wants to maintain the commit history a good approach is to make sure your code contains no secrets and then make it public.</p>
<p>GOV.UK’s infrastructure team did this when it <a href="https://github.com/alphagov/govuk-puppet">opened the GOV.UK Puppet code</a>. The team reviewed the code closely and made sure that any credentials mentioned in the code were no longer in use. They were then able to open up the code. <a href="https://gdstechnology.blog.gov.uk/2016/01/19/opening-gov-uks-puppet-repository/">You can read the infrastructure team’s blog post about it</a> to learn more about what tools and techniques they used to make sure the code was safe to open.</p>
<p>The advantage of this approach is that you maintain the full commit history.</p>
<h2><strong>Option 2: Rewrite history</strong></h2>
<p>If your team feels that the commit history is not suitable for publication, there is an alternative. After reviewing the code to make sure it’s safe to open, you can either rewrite history to remove or improve some commits, or <a href="https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History">squash</a> all previous commits into one. </p>
<p>The MOJ’s Prison Visit Booking team took this approach when it moved from coding privately to coding in the open. The team <a href="https://github.com/ministryofjustice/prison-visits/commit/fc5c908a75cf161b6f3523b5816b76ad3d4adf41">opened the existing code in a snapshot commit</a> (this was the first commit) and then <a href="https://github.com/ministryofjustice/prison-visits">carried on coding in the open</a>.</p>
<p>The advantage of this approach is that you don’t have to touch your infrastructure to do things like change a password or other details. However, the disadvantage is that you lose useful commit history, which can provide context for people working on that codebase. </p>
<h2><strong>Option 3: Move code to a new repo as you use it</strong></h2>
<p>Another way to open closed code is to create a new repository and move code. GOV.UK used this method when <a href="https://gdstechnology.blog.gov.uk/2018/01/05/how-making-our-deployment-code-open-improved-our-workflow/">improving its deployment workflow</a>. This helped the GOV.UK team to spread out the work over a longer time and share the workload out between a larger group of people.</p>
<p>The advantage of this approach is that you can do the work in smaller chunks. And, all the code is examined as you make it open. The disadvantage is that it can take a long time. You’ll also need to make sure your team finishes the job, otherwise you’ll end up maintaining two repos alongside each other.</p>
<h2><strong>After the code is open, work on the open code</strong></h2>
<p>You may be tempted to open code in a snapshot, continue to work in private, and regularly release code to the open version. This is a bad idea because:</p>
<ul>
<li>you need to continue to maintain 2 repos alongside each other, which is extra overhead for your team</li>
<li>you may find it hard to keep up the commitment to open code</li>
<li>you are not coding in the open so you’ll lose the main benefit of <a href="https://gds.blog.gov.uk/2017/09/04/the-benefits-of-coding-in-the-open/">encouraging good practice</a>, as well as other benefits</li>
</ul>
<p>I hope these examples will help you find the method that will work best for your team, so you can enjoy all the benefits of coding in the open.</p>

<p><em>This post originally appeared on the <a href="https://gdstechnology.blog.gov.uk/2018/02/19/how-to-open-up-closed-code/">GDS technology blog</a></em>.</p>
