---
title: Everything I Know About Git
description: Personal Notes
author: Patricia Aas
layout: post
icon: fa-pencil
image: "/assets/images/grafitty-4500971_640.jpg"
---

Ok, fine, I probably know more, and yes, you will probably disagree with some of this, but we both know I wrote this more for me than for you, so you're welcome :)

## Setup and config
### Make aliases
`git config --global alias.st status`

### Make pull rebase
`git config --global pull.rebase true`

### Then make pull auto stash
`git config --global rebase.autoStash true`

## See state
### Commit log
`git log`
### Status of the current tree
`git status`

## Basics
### Get changes from remote
`git pull`

### Commit changes locally
`git add <filename>`

`git commit -m "Commit message"`

### Push local changes to remote
`git push`

### Put my changes safely / temporarily away
`git stash`

### Get them back
`git stash pop`

## Branches
### List all branches
`git branch -a`

### Create a remote branch and track it
`git checkout -b <branch name>`

`git push -u origin <branch name>`

### Delete remote branch and tracking branch
`git branch -d <branch name>`

`git push -d origin <branch name>`

## Commit massaging
### Commit this into the previous (unpushed) commit (other usecase: fix commit message)
`git commit --amend`

### Pick bits of changes to a file
`git add -p <filename>`

### Reorder or squash commits
`git rebase -i HEAD~<number of commits>`

### Pick a specific commit into this branch
`git cherry-pick <SHA>`

## Fix state of tree
### Reset to some known SHA - but keep the changes in staging
`git reset <SHA>`

### Remove everything that happened after this
`git reset --hard <SHA>`

## Misc
### Get state of remote without changing the state of my tree
`git fetch`

### Create a git repo
`git init .`
