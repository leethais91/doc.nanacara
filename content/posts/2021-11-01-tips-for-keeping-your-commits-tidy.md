---
title: "Tips for keeping your commits tidy"
slug: "git-commit-tidy"
description: ""
date: 2020-09-01 11:37:37
author: ThaiLe
tags:
    - Git
cover: "https://about.gitlab.com/images/blogimages/keep-git-commit-history-clean.jpg"
fullscreen: false
---
*These are the techniques I’ll discuss below:*

>
* Frequently run `git pull --rebase origin master`
* Don’t use `git commit --all`
* Amend previous commits with `git commit --amend --no-edit`
* Changing history with interactive rebase `git rebase -i`
* Use git alias
>

I’ll elaborate more on each, and why they’re helpful, below.

## Frequently rebasing from `parent branch`
If you work on feature branches, that are based off a parent branch (e.g. the master branch of the main repository), you want to avoid your branch getting out of sync with the latest work in the parent branch.

As time goes by, your forked branch where you’re working can become significantly out of sync with the latest master branch. This may mean that merging your work when you’ve finished might become very tricky. So you need run `git pull origin master`
`git pull` is shorthand for `git fetch` followed by `git merge`.
But **DON'T DO IT**
That will create a merge commit to your feature branch.
You can avoid this by running:

```bash
git pull --rebase origin master
```
(origin: is the name of the remote pointing to your central repository; master: is your parent branch)

This will grab any new commits from the master branch, and then add all the commits in your feature branch on top of them. This keeps everything in a clear logical order.

If you can, you should also run `git pull --rebase origin master` just before your feature is merged into master. This will help the history in master stay chronological, rather than branching too often.

## Commiting files explicitly
Try to avoid using git commit --all (or git commit -a). 
It can easily lead to errors, because you might easily accidentally include changes you weren’t aware of, and forget to include new files that aren’t currently tracked.

Instead, try to check changing files and then adding files to your commits explicitly:

```bash
git status
git add {file 1} {file 2}
git commit
```

## Add changes to the previous commit
If you’ve created a commit already, but then you do more work that should logically be included in that same commit, you can simply add new work to the previous commit with:
```bash
git add {file}
git commit --amend --no-edit
```
The `--no-edit` command means you don’t want to change the commit message. You can also omit this if you want to change the description of the commit.

## Changing history with interactive rebase `git rebase -i`
Sometime you want to edit messages, remove commits, or combine multiple commits into one on your local branch.
Example, you are implement login feature on your local branch. You create three commits but you want to combine 3 commits into one commit and also edit the edit message before create pull request. Let's see:
```bash
git rebase -i HEAD~3  # Interactively rebase the last 3 commits
```
```bash
pick 239d4c3 Improve user logic
pick adc7c21 Explain user logic better in README
pick fd4f81b ... to be rebased
```

### Ref
 - https://ubuntu.com/blog/tricks-for-keeping-a-tidy-git-commit-history
