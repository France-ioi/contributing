---
layout: page
title: Github Workflows
nav_order: 20
permalink: /github
---

# Github Workflows

## The overall process

1. Make sure you have the last version of master (`git pull origin master` on master branch)
1. Create a new branch from master (`git checkout -b <branchname>` on master) , using a branch name which is relevant to the topic you are working on. (no specific naming convention)
1. Each time you have completed something (every few minutes → 1-2 hours), you commit this part (and push it to GitHub)
1. Once you are done with the implementation and all tests are passing on the CI, you create a pull-request

## Committing to Github

Expected every few minutes (max 2h):
- `git add -p`: and you select with y/n the part you want to include
- `git commit -m "<a relevant commit msg>"`
- `git push origin <yourbranchname>`

Every commit should be on one single piece of work. If you change two independent tasks, e.g. you fix a typo in a translation and you reindent a file, even if they take 30 seconds each, you should create two commits. This makes many commits at the end (especially after a review), but at least we can isolate and undo a commit without effort if needed. It also makes reviewer's work easier.

## Rebasing

A git rebase can be very useful, especially for removing from git history something which should not have committed in the first place, or to fix a commit.

There is no risk in rebasing something which has not been pushed yet but as soon as another developer has used your code locally or has started a review, do not rebase (as it rewrites history). So, for what has been pushed, only rebase at an early stage and just before merging.

In any case, use `git rebase` only if you know what you are doing (this command may really mess up everything).

You can just do rebase at an early stage and just before merging (if you know exactly what you are doing).

## Creating the pull-request

Create on Github a pull-request to merge your branch to master.

Use a **proper description** explaining what you wanted to accomplish and which allows the reviewer to know what he has to focus on. For instance, the goal was to have something working but without considering the HTML/CSS, it should be mentioned so that the review does not do dumb remark and loose time.  If it fixes a GH issue, mention it ("Fixes #123") so that GH auto-closes the issue when PR is merged.

### Appropriate size for a pull-request (PR)

There is not really a minimum size for a PR. If you change a single line in 2 minutes and then switching to something else, it is better to submit this tiny PR.

**A large PR is more problematic.** It implies a lot of work has been done before getting the first feedback. If the direction was wrong, a lot of time may have been wasted.
Also, a long review takes a lot of time to complete and is quite boring and difficult, as a consequence, the developer does not get feedback quickly enough. As a consequence, large PRs tend to have "master" diverges more and more, making the merge more likely to be complex.

In the end, a large PR usually means many remarks. Even for "small features", it is not unusual to have >200 comments over several reviews. Addressing 50 remarks and following them up is quite difficult and time consuming.

Ideally a PR for max 10 hours of work is good size.

### How to split work for a PR?

We can split a piece of work horizontally or vertically.

Horizontally is splitting by layers: the service, the UI, the component in 3 PRs.
Vertically, a subset of the functionalities of the service, of the UI and of the component.

While horizontal splitting is usually more intuitive, vertical one is more convenient for development (more lean/agile), for review (can test the sub-feature) and also may allow to keep a subset of features if the priorities change.


## The review

The goal of the reviewer is to help the developer improve his code to the expected level. The reviewer’s remarks have to be kind and constructive. On the other side, the developer must respect the time spent by the reviewer to help him, especially by handling every remarks, requesting review only when CI has passed and not leaving debug code in the PR (should be prevented by using `git add -p`).

Once the review is published,
- the developer addresses every comment, by either fixing the code and answer "fixed" to the comment, or by explaining why it will not be fixed (the developer does not press "resolve" so that the reviewer can follow up his change requests).
- no comment is left unanswered before requesting a new review (top right button).
- when the reviewer has “accepted” the PR and he has not left some last quick fixes, the developer merges the PR.
- when not required, do not merge the new changes in base branch before merging as this pollutes the history.


## Workflow for working in sub-features while reviews are in progress

A trap, especially when code to review is too big is to develop feature-A, ask for review. Then continue on feature-B,which needs feature-A, so branch for feature-A and create a PR from feature-B with feature-A as base. Then code on feature-A changes after the review, feature-B is ready before feature-A, then feature-C starts, ...

To prevent issues:
- Keep features small
- Don’t re-add new features on a already-reviewed PR
- Address in priority issues on A before continuing B.
- As soon as A is ready to be merged, merge it and make sure PR B is changed from “A ← B” to “master ← B” (automatically done by Github)
- Do not play with git rebase and merge except you know 110% what you do.

