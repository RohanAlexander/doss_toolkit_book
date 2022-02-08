


# What is version control and GitHub?

*Written by Mariam Walaa and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn how to:

- Understand version control
- Understand GitHub and Git

Prerequisite skills include:

- Navigating and working with your local folder directory

Highlights:

- Git behaves for folders similar to how AutoSave behaves for Microsoft Word.
- You can use Git within RStudio or from the command line, like Git Bash.

## Overview

You may use Microsoft Word, PowerPoint, or Excel and turn on AutoSave to track your
progress. Version control works similarly for your folder directory.

You may have a folder directory where you store files that may contain text, code,
etcetera, and you want to track the changes you make to these files. Git helps you do this
by tracking changes the make to your files in a few steps.

Just like turning on AutoSave in a Microsoft Word file, you need to tell Git that you want
a file to be tracked. Using Git, this is a two-step process:

1. First, you need to tell Git that you want to start tracking a file.
2. Next, you need to tell Git that you want the progress made to the file to be captured
at that specific point.

This is a two-step process rather than a single step in order to allow you to make as many
changes as you want before you _commit_ to the point that you would like to have the file
captured at. To be more specific, you can repeat step 1 as many times as you want before
you move on to step 2.

### Visualizing Git

Let's take a closer look at the different aspects of Git.

When using Git, the first thing you want to do is create a repository _within_ a folder
directory on your local computer. This is done using the `git init` command. When you run
this command, Git won't know which files you'd like to track, but it'll at least know that
you want some files in the directory in which you're running the command to be tracked.

<img src="images/64_git-init.PNG" width="640" />

Once you have a local repository as a result of running the previous command, the next
thing you'll want to do is maintain this local repository. In other words, you'll want to
tell Git about the state of your files as you make progress on them. You do this using
these 3 commands: `git add`, `git commit`, and `git push`. The last command, `git push`,
is typically needed when you're working with team mates and you want to push your local
work to the remote repository.

<img src="images/64_add-commit-push.PNG" width="640" />

The last command is `git status`. This is a command that you want to use as you work on
your project and make progress in your directory in order to tell you what you currently
have tracked and what you currently don't have tracked. There are several components to
the output of this command that you'll need to know how to interpret:

<img src="images/64_git-status.PNG" width="640" />

## Next Steps

If you would like to learn more about Git, here are some additional resources you may find
helpful:

- [Pro Git: **Git Basics** Chapter](https://git-scm.com/book/en/v2)
- [Happy Git With R](https://happygitwithr.com/)


## Exercises

### Question 1

### Question 2

### Question 3

### Question 4

### Question 5

### Question 6

### Question 7

### Question 8

### Question 9

### Question 10





