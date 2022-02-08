


# Dealing with conflicts

*Written by Matthew Wankiewicz and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn how to:

- Deal with conflicts that arise when working with GitHub.
- Deal with merge conflicts in GitHub.

Prerequisite skills include:

- Familiarity with GitHub.
- Git installed on your computer.
- Having a GitHub account.

Highlights:

- Merge conflicts occur when a user with a non-updated branch attempts to make a change to the main repository, causing there to be two different versions of the same repository.
- When merge conflicts occur, the owner of the repository must review the error and make a proper change to the main branch.
- **Always** pull before you push.

## The content

When you begin to work with GitHub, whether it is on personal projects or group assignments for school, you must always be careful of conflicts with GitHub. Conflicts usually arise when different version of the same file are being pushed into the main repository and GitHub does not know which one to use. 

The two main conflicts that can arise when using GitHub are conflicts with updating your personal GitHub repo (not pulling for pushing) or having multiple people change the same file in their pull requests when working in groups.

### Conflicts from Pushing before Pulling

If you decide to change something quickly on the GitHub website while you're also working on the project using R, you run the risk of creating a conflict. This conflict could be as simple as changing a typo in your README and you forgot to update that change in your R project. This is where pulling before pushing comes in handy because if you pull, your R project will be updated with the changes present on the website and if you don't, GitHub will have record of two different changes and will be unsure of which one to use.

### Conflicts from Having an Issue with a Pull Request

Sometimes, you may make a change on the main repository that someone else may have made in their branch/forked repository and when they make a pull request, GitHub will notice that there is an issue. Again, this could be something as simple as two people updating the README in different ways, causing GitHub to flag that there is an issue. When these conflicts occur, the owner of the GitHub repo will have to decide how to fix the conflict.

### Solving Conflicts

Sometimes, the easiest thing to do when there is a conflict is just delete the file (or even the repo) but save all of the important information. Then, you can create a new repo and add back in all of the files. Obviously you don't want to do this because it is time consuming and fairly simple to fix. These fixes will be described below.

**Pushing before pulling**

When you make a change on your GitHub repo and there is a conflict, when you commit your change, R will tell you that your version is ahead of the main repository. When you see this, it means that there is a difference between the files. If you attempt to pull and there is an issue, GitHub will tell you something along the lines of "**Updates were rejected because the remote contains work that you do not have locally. This is usually caused by another repository pushing to the same ref**". If that message appears, GitHub will recommend that you pull from your main repo to find the error. When you pull, GitHub will give an error saying "**CONFLICT (content): Merge conflict in [File]. Automatic merge failed; fix conflicts and then commit the result**. 

The file with the issue will then be opened up on you RStudio and will show you the error that it found. It will show you what the change you made is and what the difference is on the main branch (your changes will be shown under "<<<<<<< HEAD", the main branch's content will be shown below). What you will have to do is fix the error between the two versions, either keep what GitHub has already or make the change to fit what you wanted to do. Once you are satisfied with your change, go to the Terminal (this is located in R, a tab over from the console). In the terminal type "git add [filename]", press enter and then head back over to the Git tab on the top right of your RStudio window. Select the file that had the error and then commit and push and your error will be fixed. There will be a video explaining this on the next page.

**Merge conflicts**

If you have multiple people working on the same GitHub repo or you are just using a branch, there is the possibility that a merge conflict will occur. Merge conflicts occur when there are changes made to the main repo and a branch which do not match. Once a pull request is made, the owner of the repo will have to manually look over the issue instead of automatically merging the changes. When using branches, before the pull request is made, GitHub will say that it "Can't automatically merge" but it will still allow you to send the pull request (giving the option for you or the repo owner to do more work). If you decide to send the pull request, the owner of the repo won't be able to press the green button saying merge, instead they will see something saying "This branch has conflicts that must be resolved". To the right of that message there is a button saying "Resolve conflicts". 

Once you click on the "Resolve conflicts" button, it brings you to a page which looks similar to when you have an error with Pushing and Pulling. It will show the proposed changes from the branch and what that change looks like in the main repo. At this point, the owner can make their changes and then click on "Mark as resolved" and then "commit merge". Finally, you the owner will have to click "Merge pull request" and then "commit merge" to solidify the change into the main repo.

## Questions

Link to video explaining how to fix pull/push issues: https://youtu.be/hNmZ81poNkQ

Link to video explaining how to fix merge conflicts: https://youtu.be/SjjqBnmRP64

## Exercises

<!-- ```{r q1Conflicts, echo=FALSE} -->
<!-- question("What should you do to first to avoid conflicts in R?", -->
<!--          answer("Pull then Push", correct = T), -->
<!--          answer("Push then Pull")) -->
<!-- ``` -->

<!-- ```{r q2Conflicts, echo=FALSE} -->
<!-- order <- c("Make changes in R", "Stage the changes", "Commit the changes",  -->
<!--            "Pull from your main branch", "Push the changes to your main branch") -->
<!-- question_rank("What is the proper order to change your GitHub repo from R", -->
<!--               answer(order, correct = TRUE), -->
<!--               answer(rev(order), correct = FALSE, message = "Wrong direction!"), -->
<!--               allow_retry = TRUE) -->
<!-- ``` -->

<!-- ```{r q3Conflicts, echo=FALSE} -->
<!-- question( -->
<!--   "What is the command you should write in Terminal when you encounter a conflict?", -->
<!--   answer("git add [filename]", correct = TRUE), -->
<!--   answer("git remove [filename]"), -->
<!--   answer("git replace [filename]"), -->
<!--   answer("git rid of [filename]") -->
<!-- ) -->
<!-- ``` -->

<!-- ```{r q4Conflicts, echo=FALSE} -->
<!-- error <- c("After error message, pull from the main repo", "Open up the file with the issue", -->
<!--            "Edit the error", "Use the 'git add' command", "Commit the change",  -->
<!--            "Pull from the main repo", "Push the changes to the main repo") -->
<!-- question_rank( -->
<!--   "When you encounter a conflict, what should you do?",  -->
<!--   answer(error, correct = TRUE), -->
<!--   answer(rev(error), correct = FALSE, message = "Wrong direction!"), -->
<!--   allow_retry = TRUE) -->
<!-- ``` -->

<!-- ```{r q5Conflicts, echo=FALSE} -->
<!-- question( -->
<!--   "True or false, merge conflicts occur when there are different commits for the same file?", -->
<!--   answer("TRUE", -->
<!--          correct = TRUE), -->
<!--   answer("FALSE") -->
<!-- ) -->
<!-- ``` -->


## Next Steps

For further information on how to deal with conflicts in GitHub, check out:

- GitHub documents about merge conflicts: https://docs.github.com/en/free-pro-team@latest/github/collaborating-with-issues-and-pull-requests/addressing-merge-conflicts



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
