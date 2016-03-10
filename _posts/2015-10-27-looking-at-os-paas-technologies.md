---
anchor_id: oss-paas-tech
title: Looking at open source PaaS technologies
layout: blog_post
---
<p>I’ve been working on a prototype of what a Platform as a Service (PaaS) for
government might look like, as we wrote about in <a
href="https://gds.blog.gov.uk/2015/09/08/building-a-platform-to-host-digital-services/">a
previous post</a>. <span id="more-1257"></span> One of the first things we did
was look at the open source PaaS options that were available. This post is about
how we did that and what we learned.</p>
<img
src="/img/our_whiteboard_comparison.jpg" alt="Comparison table of PaaS" />
<h2>The open source options we considered</h2>
<p>We looked at a range of proprietary and open source options. In this post, I
am focusing on open source. This is because much of the information we learned
about the proprietary options was shared in commercial confidence. I’ll talk
more about the proprietary options we considered and how we compared them in a
later post.</p>
<h2>Exploring the options</h2>
<p>PaaS is a very fast-moving field at the moment and there are a lot of
options. The first thing we did was take some time individually within the team
to identify which options were worth investigating. We based that on previous
experience, things we’d read about, and further research online. We were around
eight people on the team, so we had a lot to draw on.</p>
<p>It’s not always the case that you are comparing like-for-like with PaaS
technologies. For example, <a href="https://www.cloudfoundry.org/">Cloud
Foundry</a> is a fully-featured PaaS, whereas <a
href="http://mesos.apache.org/">Mesos</a> is a cluster-management system. While
Mesos on its own has a number of PaaS features, it didn’t meet a combination of
the criteria "developer self-service" and "multi-tenancy" (e.g. no
authentication, access control).</p>
<p>I wanted to investigate Mesos as it’s an interesting technology, so we looked
at ways to combine it with other technologies who offer those features. We chose
combinations of technologies based on what we found to be common combinations.
In this example, you can see we looked at both <a
href="http://mesos.apache.org/">Mesos</a> + <a
href="http://aurora.apache.org/">Aurora</a>, and <a
href="http://mesos.apache.org/">Mesos</a> + <a
href="https://mesosphere.github.io/marathon/">Marathon</a> + <a
href="https://mesos.github.io/chronos/">Chronos</a> (Mesosphere). </p>
<p>At this stage, we ruled out things that we didn’t think were worth
investigating further (for example, they were nowhere near production-ready) and
worked out some combinations that made sense to look more into. </p>
<p>The longlist of technologies we investigated is:</p>
<ul>
<li><a href="http://deis.io/">Deis 1.3.1</a></li>
<li><a href="http://kubernetes.io/">Kubernetes</a> + <a
href="https://coreos.com/">CoreOS</a></li>
<li><a href="https://www.cloudfoundry.org/">CloudFoundry 2.0.0</a></li>
<li><a href="https://www.openshift.com/">OpenShift 2.0</a></li>
<li><a href="https://www.openshift.com/">OpenShift 3.0</a> (this came out during
our evaluation period and was very different to version 2.0)</li>
<li><a href="https://mesosphere.com/">Mesosphere</a> (there was no open source
Mesosphere available but we evaluated it using the component technologies it
uses: <a href="http://mesos.apache.org/">Mesos 0.2.1.1</a>, <a
href="https://mesosphere.github.io/marathon/">Marathon 0.8.0</a>, <a
href="https://mesos.github.io/chronos/">Chronos 2.3.2</a>)</li>
<li><a href="http://mesos.apache.org/">Mesos</a> + <a
href="http://aurora.apache.org/">Aurora</a></li>
<li><a href="http://panamax.io/">Panamax</a> + <a
href="https://coreos.com/">CoreOS</a></li>
<li><a href="http://rancher.com/">Rancher</a></li>
<li><a href="https://tsuru.io/">Tsuru</a></li>
</ul>
<h2>Our selection criteria</h2>
<p>In our previous post I outlined the four main criteria we’d identified from
our user research: a PaaS would have to be multi-tenant, self-service, allow
application developer support and be able to run on multiple public clouds. This
had already allowed us to rule out some technologies (for example, a number of
PaaS technologies only run on AWS). We also had some further must-have criteria.
The complete list of our selection criteria is below:</p>
<p><em>Must haves:</em></p>
<ul>
<li>Multi-vendor capabilities</li>
<li>Developer self-service model</li>
<li>Support for scaling application instances with ease (elastic scaling,
manual, self serve)</li>
<li>Support for Linux</li>
<li>Ability to choose application language</li>
<li>Ability to recover from failure of all hosts</li>
<li>Ability to maximise the application availability during underlying host
failure</li>
<li>Zero downtime deploys</li>
<li>Some multi-tenancy capabilities</li>
<li>Access to raw stdout / stderr logs</li>
</ul>
<p><em>Investigation points</em></p>
<ul>
<li>What is involved in deploying applications to this PaaS?</li>
<li>How easy is the maintenance/operation for the team maintaining the
platform?</li>
<li>Is there a hosted option available?</li>
<li>Could the unit of deployment be used without the PaaS?</li>
<li>How well documented is the PaaS? Do they keep their documentation up to
date?</li>
<li>What type of multi-tenancy support is offered?</li>
<li>Is there commercial support/consulting available?</li>
<li>What different levels of access permissions does the PaaS support?</li>
<li>Is it open source?</li>
<li>Does the PaaS provide any database service?</li>
<li>What is the language/tech?</li>
<li>What APIs are available to enable application developers to manage their own
applications?</li>
<li>Is this technology production-ready now?</li>
<li>Is there a cost associated with this and what is it?</li>
<li>How do we get data on which application is using which resources?</li>
<li>Is it possible to back up data from the PaaS itself?</li>
</ul>
<p><a href="https://twitter.com/pbansley">Brett Ansley</a>, our business
analyst, wrote these up very clearly and with acceptance criteria to clarify
what we were looking for. For example, for zero downtime deploys:</p>
<p>Given: an application that is receiving requests<br />
When: a new version of the application is deployed<br />
Then: there is no downtime of the application.</p>
<h2>Comparing against our selection criteria</h2>
<p>We then split into pairs and each pair took a technology in turn to evaluate
it. <a href="https://twitter.com/dancarley">Dan Carley</a>, our tech lead,
outlined some consistent steps to take in each investigation so that we could be
sure each pair was investigating in the same way. For example, to investigate
high availability:</p>
<ul>
<li>High availability (if self-hosted)</li>
<li>Kill one of the hosts (if self-hosted)</li>
<li>Repeat HTTPS requests to application endpoints</li>
<li>Confirm that we have the same number of workers</li>
<li>Restore host</li>
</ul>
<p>Each pair spun up the technology they were using and investigated it. As they
found the answer to each of the selection criteria, they marked it on the
whiteboard (main photograph) so we (and any passers-by) could clearly see how we
were progressing and which technologies had what. If any technology failed a
must-have, the investigation would stop; otherwise it was time-boxed to two
days.</p>
<h2>Multi-tenancy</h2>
<p>The overview of what we learned about each can be seen from the photograph of
the whiteboard above, and is summarised in <a
href="https://gdstechnology.blog.gov.uk/wp-content/uploads/sites/31/2015/10/Consolidated-evalution-of-PaaS-Technologies-Sheet1-1.csv">this
spreadsheet</a>. It’s worth noting that the spreadsheet is slightly more
up-to-date than the photograph of the board; for example Rancher and Tsuru were
late entries, and some answers were updated with more information that we
learned later.</p>
<p>One thing that I found particularly interesting was that multi-tenancy is not
a feature of many of these technologies. For example, Kubernetes and Mesos, two
widely used and interesting technologies, do not support multi-tenancy. There’s
no way to ensure that a team of developers can administer only their application
and not the applications of another team. This meant that they were not suitable
for our purposes.</p>
<h2>The tech that meets our needs</h2>
<p>After going through this process of looking at and comparing a number of open
source PaaS solutions, the clear front-runners were Deis, Tsuru, and Cloud
Foundry. The next stage was to investigate these three technologies more and
choose one to build a prototype. This has helped us with user research, which
we'll share more on later. In the meantime, we hope sharing what we’ve learnt
about these technologies is useful to you, and do let us know your thoughts in
the comments below.</p>

*This post originally appeared on the [GDS Technology
Blog](https://gdstechnology.blog.gov.uk/2015/10/27/looking-at-open-source-paas-technologies/)*.
