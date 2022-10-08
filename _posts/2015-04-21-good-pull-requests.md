---
anchor_id: pull-requests
title: How to raise a good pull request
tag: Technology
layout: blog_post
---

On our team we always commit code using [pull requests](https://help.github.com/articles/creating-a-pull-request/), for review by someone who hasn't worked on that code.

I was recently pairing with the excellent [Martin Jackson](https://twitter.com/actionjack). He had made a change to use [Librarian-Ansible](https://github.com/bcoe/librarian-ansible) to manage our dependencies; but [the pull request](https://github.com/alphagov/tsuru-ansible/pull/8) was difficult to review because most of the changes were in one commit. I paired with him to help make it easier to review, and he suggested I write up the guidelines I shared.

## Write good commit messages

As an absolute minimum, you should use good commit messages. The [GOV.UK styleguide on commit messages](https://github.com/alphagov/styleguides/blob/master/git.md) is a very good summary of how to do this and why.

Essentially, the diff shows you what has changed, and the commit message should tell you why. Ideally, you should make the explanation of why you made that change as if you were talking to someone who is looking at this code in two years, long after you've moved on to another project. What may seem obvious to you now, when you are head down in that code, probably won't be obvious to you next month, let alone to someone else later on.

## Do one thing in a pull request

The smaller the PR is, the easier it is to review and so the quicker your change will make it onto master. A good way to keep it small and manageable to focus on just doing one thing in a PR. The story you're working on might involve several changes, but if you can, it's worth splitting them into individual pull requests.

A clue as to when a PR might be doing too much comes when you're writing the headline for the PR. If you find yourself saying “and” or “also” or otherwise trying to squeeze in a number of concepts, your PR might be better as two or more.

## Make the pull request tell a story

When someone is reviewing the pull request, it should tell a story. Take the reviewer along with you. Each step should make sense in a story of how you introduced the feature.

For example, with the Librarian-Ansible change we rebased [this commit](https://github.com/alphagov/tsuru-ansible/commit/7547ac0d35a) into [this series of commits](https://github.com/alphagov/tsuru-ansible/compare/d891857...d14bb2f44). Each of those commits is self-contained and comes with a commit message explaining why that step is taken. Taken together, they tell a step-by-step story of how we introduced Librarian-Ansible.

This allows a reviewer to follow along with your process and make it easier for them to think about what you've done and whether the changes you've made are the right ones.

For example a reviewer might get to the point where [we configure Librarian-Ansible to use something other than the default directory](https://github.com/alphagov/tsuru-ansible/commit/d55e7c94) and wonder whether we should instead have changed our Ansible code to refer to the `librarian-roles` directory. Without the separation of steps into a story, it would be difficult to see that step and wonder about the change, so that potential review point is lost.

## Make it a logical story

Ordering the commits so they tell a story can be quite hard to begin with, especially if you're not sure how the piece of work is going to play out. After a while, you will get a feel for the flow of work and you'll have a better idea of what small chunks to commit. Until then (and even then) [git rebase interactive](http://git-scm.com/book/en/v2/Git-Tools-Rewriting-History#Changing-Multiple-Commit-Messages) is your friend.

Apart from making the PR tell a story, it's worth rebasing to keep connected changes together. For example, instead of adding some commits at the end that say “I forgot to add this file” or “Also making the same change here”, it will be clearer for the reviewer if you rebase, and add those changes to the original commit to keep the narrative. I've often reviewed a PR and made a comment like “this change also need to be made in X”, only to find that has been done in a later commit.

The cleaner and more logical the narrative of the commits in the pull request is, the easier it is for the reviewer to retain the whole context in their head and concentrate on the important things to review.

## Provide as much context as possible

Imagine everyone else on the team has no idea what you have been working on. Ideally you want the pull request notification to arrive with a full explanation of what this change is and why you're making it, so that anyone can pick it up and review it. 

Link to the story it relates to (you can also use a [webhook](https://help.github.com/articles/about-webhooks/) so the story or issue is automatically updated). Point to other PRs or issues that are related. Explain what tests you've done, and if relevant, what the reviewer can or should test to confirm your changes.

The more context you can provide, the easier it is to review which makes it more likely to be addressed quickly.

## Make sure the pull request, when merged to master, is non-breaking

Ideally each commit should be an atomic, non-breaking change. This is not always possible. However, a pull request is a request to merge your code onto master, so you must make sure that it is complete, in that it is a non-breaking change. It should work, and the tests should still pass once your pull request is merged.

## Never commit directly to master, no matter how small the change is

This is a rule on my team, for two reasons: communication and review.

When you have a number of people working on a codebase, you want to communicate to everyone what changes you are making. Raising a pull request is a broadcast to everyone [watching that repository](https://help.github.com/articles/watching-repositories/) so even team members who have not been involved in that piece of work can keep an eye on what's going on so that changes do not come as a suprise to them. You also do not know what everyone's experience is, and raising a pull request can sometimes trigger useful input from an unexpected source; committing directly to master would have lost you that opportunity.

As well as making sure the whole team can keep an eye on what changes are happening, raising a pull request also allows the team to maintain a level of quality through code review. Some changes are so tiny that they (probably) don't need a review, but by making a rule that you never commit directly to master, there's no chance that something that should not have done will slip through the cracks.

## An example of a good pull request

Take a look at this [extremely good pull request](https://github.com/alphagov/frontend/pull/784) raised by the excellent [Alice Bartlett](https://twitter.com/alicebartlett).

Alice did the work first, and then pulled out the changes one-by-one to a new branch to make it clear. While doing the work she refactored some code but in the final PR she has put the refactoring up front, to clear the way for the change she wants to make. This makes it much easier to review because the changes don't then clutter up later commits. There is also a lot of detail in the overview.

Raising pull requests like this takes time, but it is really worth doing; it makes it clear for your reviewers, the rest of your team, and for the programmers who will be working on this codebase long after you've forgotten about the changes you made today.
