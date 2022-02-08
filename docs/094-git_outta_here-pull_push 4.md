


# Git: pull, status, add, commit, push

*Written by Mariam Walaa and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn how to:

- Create a local repository in a folder
- Make changes to a remote repository
- Maintain a local repository

Prerequisites include:

- Creating a [GitHub account](https://github.com/join)
- Downloading [Git Bash](https://git-scm.com/downloads)

Highlights:

- You can start tracking a folder of your work locally using Git.
- You can share a local repository with team mates using GitHub.

## Overview

There are two common scenarios for getting you and your team mates set up to use Git and
GitHub:

1. Your team hasn't started the project yet, so one of your team mates needs to create a
Git repository which you can clone and start pushing files to and pulling files from.
2. You've already started working on the project locally and want to share it with your
team mates so they can add their own work.

Both of these scenarios are described in great detail by Jenny Bryan from RStudio. You can
find and follow those instructions here:

- Scenario #1: [Happy Git With R: Chapter 15 - New project, GitHub
first](https://happygitwithr.com/new-github-first.html#new-github-first)
- Scenario #2: [Happy Git With R: Chapter 17 - Existing project, GitHub
last](https://happygitwithr.com/existing-github-last.html#existing-github-last)

## Videos

![](https://youtu.be/aX5BqMkyt3s)

![](https://youtu.be/Afn1zzo0Uis)

## Exercises

In this section, we'll go through exercises that help you understand the process of
tracking and committing files within a local repository using Git.

We will begin by opening Git Bash, creating a new folder directory, and creating a new
file as follows:

1. Create a new folder directory: ``mkdir DoSS-Toolkit-Git-Demo``
2. Go to the folder directory: ``cd DoSS-Toolkit-Git-Demo``
3. Create a new file: ``touch README.md``

We now have a folder directory with a README file.

### Exercise 1

<!-- ```{r git-exercise-1, echo = FALSE} -->
<!-- question("We want to initialize the local repository. Which is the correct command?", -->
<!--          answer("git init", correct = TRUE), -->
<!--          answer("init"), -->
<!--          allow_retry = TRUE, -->
<!--          random_answer_order = TRUE) -->
<!-- ``` -->

If you've done this correctly, you should now have a local repository in your folder.

### Exercise 2

<!-- ```{r git-exercise-2, echo = FALSE} -->
<!-- question("We want to start tracking this file. Which is the correct command?", -->
<!--          answer("git add README.md", correct = TRUE), -->
<!--          answer("add README.md"), -->
<!--          answer("git add README"), -->
<!--          allow_retry = TRUE, -->
<!--          random_answer_order = TRUE) -->
<!-- ``` -->

If you've done this correctly, you should now have started tracking README.md. You can
check the status using `git status`.

### Exercise 3

<!-- ```{r git-exercise-3, echo = FALSE} -->
<!-- question(paste("We started tracking README.md and want to commit this file. ", -->
<!--                "Which is the correct command?"), -->
<!--          answer("git commit -m 'Add README.md to the local repository'", -->
<!--                 correct = TRUE), -->
<!--          answer("git commit 'Add README.md to the local repository' -m"), -->
<!--          answer("git 'Add README.md to the local repository' -m commit"), -->
<!--          allow_retry = TRUE, -->
<!--          random_answer_order = TRUE) -->
<!-- ``` -->

If you've done this correctly, you should now have a committed README.md file in your
folder (i.e., Git knows about this file and has stored a version of it that you've decided
to commit).

If you want to share this folder with your team mates, you would have to create a remote
repository on GitHub. To do this, you can follow [these
instructions](https://happygitwithr.com/existing-github-last.html#existing-github-last)
from Happy With Git R.

### Exercise 4

<!-- ```{r git-exercise-4, echo = FALSE} -->
<!-- order <- c("git add README.md", -->
<!--            "git commit -m 'add updated README.md'", -->
<!--            "git push") -->

<!-- question_rank(paste("We made changes to README.md _locally_ and we want to push ", -->
<!--                     "these changes. In which order should we run the commands?"), -->
<!--               answer(order, correct = TRUE), -->
<!--               answer(rev(order), correct = FALSE), -->
<!--               allow_retry = TRUE) -->
<!-- ``` -->

### Exercise 5

<!-- ```{r git-exercise-5, echo = FALSE} -->
<!-- question(paste("Someone made changes to README.me in the _remote_ repository and we ", -->
<!--                "want to pull those changes. Which is the correct command?"), -->
<!--          answer("git pull", correct = TRUE), -->
<!--          answer("git push"), -->
<!--          answer("git status")) -->
<!-- ``` -->

### Exercise 6

<!-- ```{r git-true-statements, echo = FALSE} -->
<!-- question("Which of these are true? Check all true statements.", -->
<!--           answer(paste("You can run `git status` before you run `git init` to see ", -->
<!--           "which files are already being tracked."),  -->
<!--           message = paste("Running `git status` before initializing the local Git ", -->
<!--           "repository will give you an error. A Git repository needs to be ", -->
<!--           "initialized first in order to check the status of it.")), -->
<!--           answer(paste("Once you initialize a Git repository within a folder, ", -->
<!--           "all files in that folder automatically become tracked."), -->
<!--           message = paste("Initializing a Git repository within a folder does ", -->
<!--                           "not tell Git which files in that folder to track.")), -->
<!--           answer(paste("When a file is committed, the file becomes shared", -->
<!--                        "with everyone who has access to the remote repository."), -->
<!--                  message = paste("A file is committed to the _local_ Git repository ", -->
<!--                                  "and not the remote Git repository.")), -->
<!--           answer(paste("Running `git push` pushes all committed files to the ", -->
<!--                        "remote repository which can be accessed by others."), -->
<!--                  correct = TRUE), -->
<!--           answer(paste("Running `git pull` pulls all new files from the remote ", -->
<!--                        "repository to your local repository."), correct = TRUE), -->
<!--           allow_retry = TRUE, -->
<!--           random_answer_order = TRUE) -->
<!-- ``` -->

## Common Mistakes & Errors

Below are some common mistakes and errors that you may come across while using Git:

- You try to run `git commit` after making changes to a file but you aren't currently
tracking that file, so you need run `git add` first.

- You run `git status` and see that a file is listed under both `Changes to be committed` 
and `Changes not staged for commit`. This happens when you start tracking a file and make
more changes to it before you commit it. Now, the initial version is tracked and the most 
recently updated version is still untracked, so they appear under both sections.

- You try to run `git push` to push your updates to the remote repository while there are
some new updates in the remote repository, likely from another team mate, that you don't
already have. The error you get will likely be something like:
  + `error: Your local changes to the following files would be overwritten by merge: ...
  Please commit your changes or stash them before you merge.`.
  
  This is an issue for Git because Git has your team mate's new updates, and now you're
  telling Git to add your own updates without your team mate's updates, so Git doesn't
  know what to do. The best way to avoid this issue is to always run `git pull` before you
  start working on your files locally. However, there's a better explanation on what to do
  if you run into this issue by Jenny Bryan from RStudio in [this
  section](https://happygitwithr.com/pull-tricky.html) from Happy Git With R.

## Next Steps

If you would like to learn more about Git, here are some additional resources you may find
helpful:

- [Pro Git: **Git Basics** Chapter](https://git-scm.com/book/en/v2)
- [Happy Git With R](https://happygitwithr.com/)

If you've completed this tutorial successfully and would like to learn how to use Git
within RStudio, there is a helpful
[section](https://happygitwithr.com/rstudio-git-github.html) in Happy Git With R about
connecting RStudio to Git and GitHub.



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
