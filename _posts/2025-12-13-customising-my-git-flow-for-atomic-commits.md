---
layout: post
title: "Customising My Git Flow For Atomic Commits"
date: "2025-12-13 12:50:40 +0200"
categories: [Git, Debugging]
author: Iain Cambridge
---
I recently learnt about atomic commits after spotting an unusual note on a pull request someone asked me to review. While I'm a bit embarrassed it took me so long to even hear about them, once someone explained atomic commits to me—and showed me the power of bisect when you're using them, plus how much flexibility they give you with Git, was sold.

# Quick Rundown Of Atomic Commits

To be fair, you should read [Atomic commits will help you git legit.](https://dev.to/paulinevos/atomic-commits-will-help-you-git-legit-35i7){:target="_blank"}  with this [git cheatsheet](https://dev.to/paulinevos/git-legit-cheat-sheet-2gf0){:target="_blank"}  which I skimmed to get a grasp of. The concept of single units is clear for most of us. But the benefits of doing it on a commit level were never obvious to me, and that post points out those benefits pretty clearly.

For those who want a super simple breakdown: atomic commits are when you only commit a single logical unit of code that can pass the CI build. In other words, each commit should represent one cohesive change or feature that makes sense on its own. This means that if someone were to review your commit history, they could easily understand what each commit does without needing to look at multiple commits together. The key principle here is that every commit should leave your codebase in a working state - nothing should be broken, all tests should pass, and the code should compile successfully. Think of it like saving your progress in a video game at checkpoints that actually make sense, rather than saving randomly in the middle of a boss fight.

The benefits include:

- Easier code reviews since you can review each commit independently
- Better ability to use bisect since every commit passes tests
- The option to do trunk-based development where everyone pushes directly to the main branch

# The Problem

I currently develop using a pattern where I start with a functional test that I make fail. Then I drill into the entry point in the application and build units of code, doing TDD on those units until I eventually make the functional test pass. This means my working branch always has code that doesn't belong to the logical unit of code that should be contained within atomic commits.

So naturally I asked what atomic commits are actually doing, since this probably wasn't just a me problem. Turns out there are various approaches. One is Stacked Diffs, which I haven't learned yet. Another is reordering commits and pushing for WIP, which sounds like a lot of work. And then there were some truly wild options. So my solutions had these flaws: 'I don't know how to do that yet', 'I'm too lazy for that', or 'I'm not that foolish'.

# The Solution

In true developer fashion, I decided that instead of learning something, I'd just write some scripts to automate it instead.

I needed a solution that:

- Was easy to add to my workflow
- Wouldn't break if it wasn't in the workflow
- Let me switch branches quickly
- Let me commit and push only the logical units I decided on
- Automatically detected what I consider to be the base WIP code
- Didn't commit that base WIP code, but committed everything else

To achieve this, I created three subcommands: `wstash`, `wcommit`, and `wcheckout`.

## Idea

My idea is to use stash to store my WIP base code while I commit everything else. The issue is that manually doing this becomes a pain—it's extra work every time.

- Start a stash session that marks the current files as base WIP
- Each stash session is tied to its branch—only one session can exist per branch
- When committing from a stash session, commit whatever files remain
- When committing without an active stash session, commit normally
- When you check out of a branch with an active stash session, automatically stash your changes
- When you check out to a branch with an existing stash session, automatically restore that stash
- When you check out to a branch without a stash session, don't start one
- Finish a stash session

## wstash

There are three commands \`start\`, \`list\`, \`finish\`.

`start` this command creates a metadata file that shows there is an active stash session currently in progress. It contains the name of the stash that is to be used and references the file where the stash data is stored. Once this metadata file is created, any of the other commands will act differently and automatically use stash instead of their default behavior. This allows you to work within a stash context without having to explicitly specify it each time.

`finish` this command deletes the metadata file that was created by the `start` command and reverts the commands back to their original state so they act like standard commands again. Essentially, it closes out your stash session and returns everything to normal operation mode.

`list` lists out all the branches that currently have active stash sessions enabled. This gives you a quick overview of which branches are operating in stash mode, making it easy to keep track of your work across multiple branches.

### wcommit

This command acts transparently and passes everything through to the `commit` command without any modifications or interference. It essentially serves as a wrapper that maintains all the functionality and arguments you'd normally use with a standard commit operation.

If there is a stash session active at the time you run this command, it intelligently handles the stashing workflow for you. This command automatically stashes the files that are designated to be stashed according to your stash session configuration, then proceeds to commit the remaining changes to your repository, and finally unstashes the code immediately afterward. The end result is that your working directory looks exactly the same as it did before you ran the command - all your uncommitted work-in-progress files are right back where they were. But now you've successfully committed a single logical unit of code to your repository without having to manually juggle the stash and unstash operations yourself.

### wcheckout

This command acts transparently and passes everything through to the `checkout` command without interfering with its normal operation or modifying any of its default behaviour.

If there is a stash session currently active on your current branch, when it switches to the new branc,h it'll automatically stash the code for you. This happens seamlessly in the background. If there's no active stash session, it acts as a standard checkout command would, simply switching branches without any additional stashing behaviour.

Upon switching to the new branch, if there is a stash session active for that specific branch (meaning you had previously stashed work on that branch), it automatically restores the stash for you. This way, you can pick up right where you left off with your work-in-progress changes intact.

## Example

```sh
git wstash start 
git wcommit -am "Add my changes"
git wcheckout -b new-branch
git wcheckout old-branch
git wstash finish
git wcommit -am "Final changes"
```

## Repository

You can find the scripts at https://github.com/that-guy-iain/git-scripts.