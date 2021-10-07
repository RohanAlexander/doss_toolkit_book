


# Putting (G)it All together in RStudio

*Written by Matthew Wankiewicz and last updated on 7 October 2021.*

## Introduction

Now that you have learned about the different GitHub operations and processes that you will need for future projects, we can now look at how to use these commands in RStudio. Using the commands in RStudio is a much better alternative because you will have all of your work located in one place. This lesson will look at how to push, pull, fork and do other GitHub operations using RStudio.

Before beginning, make sure you have Git downloaded onto your computer or else these commands will not work.

## Bringing the Repo into R

Before working with a GitHub repository in RStudio, make sure you have a GitHub repository you are ready to work with.  

Now that you have created the repo, you can click the green button to get a link which will help you clone the repository. To open this in R, open up R then click on the cube with a plus over it to create a new project, click version control and then Git. Now, paste in the url you copied earlier and create the project. Now you have a project in R which is connected to GitHub. Now you can create new files and upload them to GitHub so others can see. 

## Explaining the buttons/commands

Looking in the top right pane (depending on how your RStudio is configured) you will have tabs that say "Environment", "History"..., select the one that says "Git" to take a look at the Git commands. In this panel, you can decide which files to upload/delete, commit any changes, pull from the main repo, push to the main repo, review any changes that you've made and lastly create/switch between branches. We will now look at what each command/button does.

- **Diff:** Clicking on Diff will open up a new window in R. The window will show all of the files which have been changed (relative to what the main repo looks like) and will also show you the changes you have made. You can also use this window to commit changes you have made and push/pull from the main repo. 

- **Commit:** Using commit in the smaller window is similar to using it in the "Diff" window, you just need to select files you want to send to the repo and then commit your changes.

- **Pull:** Pull is fairly self-explanatory, it will pull files from your GitHub repo. It's important to pull files before pushing, to make sure you avoid any possible conflicts with files overlapping. 

- **Push:** Push will push your files to the GitHub repo. This will be used when you have finished making changes with your file(s) and are ready to have it uploaded so other people can look at the new files. The order for uploading these files would be to commit your changes, pull from the repo and then push to the repo.

- **History:** The next icon is a small clock which represents the history of your work. It shows you past commits including what was changed in each commit.

- **Revert, Ignore and Shell:** These commands are located in a dropdown menu after you click on the gear beside the clock. Revert allows you to undo any changes you have made, Ignore allows you to set up a gitignore (useful for blocking any files you don't want to be uploaded) and Shell will open up your terminal allowing you to use git commands there. 

- **Branching:** The next symbol represent branches. When you click on this symbol, it will ask if you want to create a new branch. As you learned in the branches module of the toolkit, branches are useful for testing out changes you want to make without impacting your main branch, in case an error occurs. You can use the dropdown menu to the right of the branches symbol to move between your branches.

- **Terminal (Optional):** While you can use the RStudio commands to conduct these GitHub commands, you can also use the terminal in R to do the same thing. All of the GitHub commands will be in the form of "git _____" and you can find them by typing "git" into your terminal, this will return a list of git commands. This does the same thing as the R panel does but if you are more familiar with writing git commands in terminal this may work better for you. 

### Making an R project into a GitHub repo

Sometimes you may be working on a project in R and you forgot to make a GitHub repo for it. If this happens, the `usethis` package can help you create a repo from RStudio. The function `usethis::use_git` will let you turn your current project into a GitHub repo so you can upload your files. 
  - If you run this function for the first time it will likely encounter an error because you need to get a token from GitHub to do this. After running `usethis::browse_github_token` a new window will open asking you to log into your GitHub account. Once you log in you can set permissions from the token and then you can copy it. Once you copy it call `usethis::edit_r_environ()` and store your token as "GITHUB_PAT=token". 

Once your token is set and your R is reset you can use `use_git` and it will ask you if it's okay to commit your files so they can go to GitHub. Once you say yes, it will ask you to restart your RStudio window to bring in the Git pane, to upload your files. Once your RStudio is restarted use the "Diff" button to commit your changed files (if any). Now, use the `usethis::use_github` to send your files to a GitHub repository. 
  - `use_github` will ask if you have ssh keys set up, you probably will not so select "https". It will then ask if your title and description are acceptable, if they are, you can say yes and upload it to GitHub!

## Live Demonstration 

- A video explaining the basics of GitHub in RStudio:

<iframe width="560" height="315" src="https://www.youtube.com/embed/lCWu3aL1WQ0" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Test Your Understanding

<!-- ```{r github-rstudio-mc1, echo=F} -->
<!-- question("True or False, you can use the terminal OR the git pane in RStudio to use git commands?", -->
<!--          answer("True", correct = T), -->
<!--          answer("False"), -->
<!--          allow_retry = T) -->
<!-- ``` -->

<!-- ```{r github-rstudio-mc2, echo=F} -->
<!-- question("Which package allows you to create GitHub repositories from R projects?", -->
<!--          answer("`usethis`", correct = T), -->
<!--          answer("`githubcreate`"), -->
<!--          answer("`tidyverse`"), -->
<!--          answer("`dplyr`"), -->
<!--          random_answer_order = T, -->
<!--          allow_retry = T) -->
<!-- ``` -->

<!-- ```{r github-rstudio-mc3, echo=F} -->
<!-- question("How do you avoid GitHub conflicts in R (this was also asked in a previous lesson)?", -->
<!--          answer("Conflicts don't happen in R"), -->
<!--          answer("Push then Pull"), -->
<!--          answer("Pull then Push", correct = T), -->
<!--          answer("What's a conflict?"), -->
<!--          allow_retry = T) -->
<!-- ``` -->

<!-- ```{r github-rstudio-mc4, echo=F} -->
<!-- question("Which does the pull command do?", -->
<!--          answer("Updates your local files from your repository", correct = T), -->
<!--          answer("Updates your repository from your local files"), -->
<!--          answer("Creates a new branch"), -->
<!--          answer("Opens up the terminal"), -->
<!--          random_answer_order = T, -->
<!--          allow_retry = T) -->
<!-- ``` -->

<!-- ```{r github-rstudio-mc5, echo=F} -->
<!-- question("Which does the push command do?", -->
<!--          answer("Updates your local files from your repository"), -->
<!--          answer("Updates your repository from your local files", correct = T), -->
<!--          answer("Creates a new branch"), -->
<!--          answer("Opens up the terminal"), -->
<!--          random_answer_order = T, -->
<!--          allow_retry = T) -->
<!-- ``` -->


<!-- ```{r github-rstudio-rank, echo=F} -->
<!-- order <- c("Make changes in file", "commit changes", -->
<!--            "pull from the main repo", "push to the repo") -->

<!-- question_rank("What is the workflow for uploading a file to a GitHub repo from R? (SORT first -> last)", -->
<!--               answer(order, correct = T), -->
<!--               answer(rev(order), message = "Other way!"), -->
<!--          allow_retry = T) -->
<!-- ``` -->

## Common Mistakes and Errors

The most common error that will occur when working with GitHub in R are conflicts. Conflicts occur when you attempt to make a change on a file and when you upload the file to GitHub it doesn't match its records. The previous module called "Dealing with Conflicts" explains what to do when these errors occur.
  
## Next Steps

For more information about using GitHub in RStudio, check out the following links:

  - This blog post shows how to use git in RStudio and highlights the terminal commands: https://resources.github.com/whitepapers/github-and-rstudio/


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

