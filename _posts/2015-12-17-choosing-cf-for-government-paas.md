---
anchor_id: choosing-cf
title: Choosing Cloud Foundry for the Government Platform as a Service
layout: blog_post
---

We previously wrote about [looking into offering a
platform](https://gds.blog.gov.uk/2015/09/08/building-a-platform-to-host-digital-services/) to host digital
services. This post is about the technology we chose for the beta and how we
made that decision.

![Government PaaS team](/img/Government_PaaS_team.jpg)

## Comparing technologies for the prototype

The first thing we did was look in detail at the various open source and
proprietary options available. I’ve previously written about [how we compared the
open source
options](https://gdstechnology.blog.gov.uk/2015/10/27/looking-at-open-source-paas-technologies/)
and I mentioned that the front-runners were [Cloud
Foundry](https://www.cloudfoundry.org/),
[Deis](http://deis.io/) and [Tsuru](https://tsuru.io/).

Deis was a very good option, but we ruled it out for our prototype for two
reasons: it didn’t have the granularity of user permissions we needed, and it
didn’t have a mature service broker, which would allow us to connect to external
services, eg Postgres. Both of these things are on their
[roadmap](http://docs.deis.io/en/latest/roadmap/roadmap/), but the timing
wasn’t going to work for us. However, we had a very interesting conversation
with the Deis team and this is definitely a technology to keep an eye on.

With the proprietary options, the method of comparison was slightly different
because the source code isn't available to look at, and because it’s not usually
as easy to get a sample platform up and running.

There were four proprietary vendors we were particularly interested in:
[Apcera](https://www.apcera.com/),
[OpenShift Enterprise](https://enterprise.openshift.com/) (Red Hat), [Pivotal
Cloud Foundry](http://pivotal.io/platform) and
[Stackato](https://docs.stackato.com/). Each one of
the vendors answered questions to a similar level of detail as we were able to
learn by [investigating the open source solutions
ourselves](https://gdstechnology.blog.gov.uk/2015/10/27/looking-at-open-source-paas-technologies/). Because of
commercial confidentiality, I can’t share the detail here but it allowed us to
compare the proprietary solutions, and then again with the open source ones.

They all had advantages, but the one that most suited our requirements was
Apcera.

## Comparing Tsuru, Cloud Foundry and Apcera

We wanted to get a prototype up and running quickly so we could start showing it
to our users in government to see if we were on the right lines. So we decided
to start with an open source solution because there are no licensing issues.

We built a prototype using Tsuru, because it's easier to get started with Tsuru
than Cloud Foundry. Then we used that prototype in our user research - we wanted
to make sure we understood which features were most important to our potential
users.

We then built another prototype in Cloud Foundry to compare its features, ease
of use and maintenance requirements to those of Tsuru. Simultaneously, we spent
some time exploring a trial installation of the Apcera platform with our
engineers providing feedback about each of the three different options.

## Why we decided to go for open source rather than proprietary

[Paul Downey](https://twitter.com/psd), the product owner on the
[Registers](https://gds.blog.gov.uk/2015/09/01/registers-authoritative-lists-you-can-trust/) team, has described the work
we're doing on [Government as a
Platform](https://gds.blog.gov.uk/2015/10/07/government-as-a-platform-for-the-rest-of-us/) as fitting into three categories:
product, platform and standard.
![Product, platform and standard sketch by
@psd](/img/productplatformstandard.png)
<p class="photo-credit">Licence: Creative Commons Attribution Paul Downey</p>

This is how we apply those categories:

- product: we would make the code available and you could use it to build your
own PaaS, which you would then run
- platform: we would offer our PaaS as a platform for you to use; this would
incur some costs but would also come with some level of support for the platform
- standard: we would define standards for you to build your own PaaS

If the technology we choose is not open source, the product would be the
proprietary option. So in effect, we'd just be recommending a product to other
departments, and they would then have to build their own platform and incur
costs over and above supporting and developing the platform. But having the code
available for use by other departments as a platform would encourage
collaboration with our colleagues in those departments.

Using an open source solution brings a number of other important benefits. The
chance to contribute code upstream means we can help make the product useful to
us and others in a similar position. Maintaining and building open source
components and the 'glue' (ie the code required to keep it all together) builds
skills and learning in-house. And it also echoes our [tenth design
principle](https://www.gov.uk/design-principles#tenth):
'Make things open: it makes things better'.

## Choosing Cloud Foundry

The three technologies we looked at in more detail had a lot to recommend each
of them.

Tsuru:

- has a very simple architecture and is easy to set up and maintain
- uses commonly understood components like MongoDB and Redis
- it's easy to swap these components for others, eg Dan Carley made a change
to replace the default Hipache router with Vulcand
- the team are extremely responsive and got back to us quickly on all issues
and pull requests, eg Dan’s Vulcand change was merged and published in the next
available release

Cloud Foundry:

- has a mature team management model and an authentication engine that meets
our needs
- handles scaling easily and effortlessly, performing well under a heavy load
- like Tsuru, it has a mature service broker framework, but there are more
services already implemented (e.g. MySQL) for Cloud Foundry, which means less
work for us
- has a very large community with plenty of opportunities for improvement,
sharing tools, recruiting specialists, and sharing knowledge

Apcera:

- has robust multi-tenant support governed by a policy-driven model that
allows granular control of resources, including networks and services, packages,
versions and even regions
- has fine-grained control, which makes detailed auditing easier

While each of the technologies we looked at had advantages, the open source
requirement is important to this project, so we had to rule Apcera out for now.

It was a very close contest between Tsuru and Cloud Foundry. After a lot of
consideration we chose Cloud Foundry for our beta. The maturity of Cloud
Foundry, as well as the size of its community, were the most significant factors
in this decision.

However, all three technologies are very good and if your team’s requirements
are similar to ours then it's definitely worth considering them all.

## Next steps

We hope to share more detail about what we learned about each technology in
future posts, but in the meantime we're now starting the beta build using Cloud
Foundry. We're coding in the open, and aiming to be hosting live services early
next year.


*This post originally appeared on the [GDS Government as a Platform
Blog](https://governmentasaplatform.blog.gov.uk/2015/12/17/choosing-cloudfoundry/)*.
