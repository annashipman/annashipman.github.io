---
anchor_id: alphagov-fog-updated
title: How I keep alphagov/fog updated...
layout: blog_post
---

I refer back to this useful email from <a href="https://www.twitter.com/mikepea">Mike Pountney</a> pretty frequently, even though it's easy enough to look up, so thought I'd save it here.

```
git checkout master &&

git pull &&

git fetch upstream &&

git merge upstream/master &&

git push
```
{:.code-sample}

