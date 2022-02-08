


# Projects issues

*Written by Ruijia Yang and last updated on January 30 2022.*

## Introduction
Working through subsequent material in R Markdown documents, possibly using Git and GitHub to track and share your progress, is a great idea and will leave you more prepared for your future data analysis projects.

In this section, you will learn: 

- Develop a few key workflows using GitHub Project that cover your most common tasks.
- Add a github project to your repositories and use it to track github issues using a Kanban style board
- Integrate Git and GitHub into your daily work with R and R Markdown.

Prerequisite:

- Make sure you have a GitHub repository you are ready to work with.

Highlight:

- Working in Github with help of projects, issues and comments.
- Using these GitHub features to plan and track your work, and better managing your projects.

## Project
From last session, you already knew how to create a project in R which is connected to GitHub.However, in this session, the project is a different from the Rstudio Project, and it is a GitHub feature, which helps you organize and prioritize your work. 

A project is a customizable spreadsheet that integrates with your issues and pull requests on GitHub. You can create project boards for specific feature work, comprehensive roadmaps, or even release checklists. With project boards, you have the flexibility to create customized workflows that suit your needs. 

Project boards are made up of issues, pull requests, and notes that are categorized as cards in columns of your choosing. You can drag and drop or use keyboard shortcuts to reorder cards within a column, move cards from column to column, and change the order of columns.

You can create notes within columns to serve as task reminders, references to issues and pull requests from any repository on GitHub.com, or to add information related to the project board. You can create a reference card for another project board by adding a link to a note. 


### Elements in Project 
The activity view shows the project board's recent history, such as cards someone created or moved between columns. To access the activity view, click `Menu` and scroll down.

To find specific cards on a project board or view a subset of the cards, you can filter project board cards. 

To simplify your workflow and keep completed tasks off your project board, you can archive cards. 

If you've completed all of your project board tasks or no longer need to use your project board, you can close the project board. 

### Templates for Project
You can use templates to quickly set up a new project board. When you use a template to create a project board, your new board will include columns as well as cards with tips for using project boards. You can also choose a template with automation already configured.

|    Template   | Description     | 
|------------------------|-----------------|
| Basic kanban    | Track your tasks with To do, In progress, and Done columns|
|Automated kanban | Cards automatically move between To do, In progress, and Done columns |
|Automated kanban with review | Cards automatically move between To do, In progress, and Done columns, with additional triggers for pull request review status |


Click [here](https://youtu.be/YQbbZlcb5mI) to view a video demo of creating a project


### Adding issues and pull requests to a project
You can add issues and pull requests (PR) to a project board in the form of cards and triage them into columns. 
You can add issue or pull request cards to your project board by:

- Typing the issue or pull request URL in a card.

- Searching for issues or pull requests using search qualifiers in the project board search sidebar. 

In the project board, click`+ Add Cards`. From the filtered list of issues and pull requests, drag the card you'd like to add to your project board and drop it in the correct column.

### Adding issues and pull requests to a project board from the sidebar
On the right side of an issue or pull request, click `Project` and choose from different tabs for the project board you would like to add to. Type the name of the name of the project in `Filter projects` field.

### Add Automation for project boards
You can configure automatic workflows to keep the status of project board cards in sync with the associated issues and pull requests.
To set up automatic workflows for a repository project board, you must have write access to the repository. 

You can automate actions based on triggering events for project board columns. This eliminates some of the manual tasks in managing a project board. For example, you can configure a "To do" column, where any new issues or pull requests you add to a project board are automatically moved to the configured column. And to edit columns that already have configured automation, click `Manage` at the bottom of the column. 

You can read more [here](https://docs.github.com/en/issues/organizing-your-work-with-project-boards/managing-project-boards/configuring-automation-for-project-boards)



## Issues
You can use GitHub Issues to track ideas, feedback, tasks, or bugs for work on GitHub. 

Create issues:

Issues can be created in a variety of ways, you can create an issue from a repository, an item in a task list, a note in a project, a comment in an issue or pull request, a specific line of code, or a URL query.

Track work:

You can organize and prioritize issues with projects. To track issues as part of a larger issue, you can use task lists. (You can read more [here](https://docs.github.com/en/issues/tracking-your-work-with-issues/about-task-lists).) To categorize related issues, you can use labels and milestones. To stay updated on the most recent comments in an issue, you can subscribe to an issue to receive notifications about the latest comments. To help contributors open meaningful issues that provide the information that you need, you can use issue forms and issue templates. (You can read more [here](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests).)


## Comments
Adding line comments is a great way to discuss questions about implementation or provide feedback to the author.

You can comment on a pull request's Conversation tab to leave general comments, questions, or props. You can also suggest changes that the author of the pull request can apply directly from your comment.

How to add line comments to a pull request:

-In the list of pull requests in your repository, click the pull request where you would like to leave line comments. 
-On the pull request, click `Files Changed`. 
-Hover over the line of code where you'd like to add a comment, and click the `blue plus icon` for comment. To add a comment on multiple lines, click and drag to select the range of lines, then click the `blue plus icon`. 
-Leave your comment in the comment box. Click `Add single comment` when you are done.

How to resolve conversations:

You can resolve a conversation in a pull request if you opened the pull request or if you have write access to the repository where the pull request was opened. To indicate that a conversation on the Files changed tab is complete, click `Resolve conversation`. The entire conversation will be collapsed and marked as resolved, making it easier to find conversations that still need to be addressed.

## Exercise
### Question1
1. GitHub Project is the same with the project in RStudio.

    a.  False
    b. True
    
### Question2    
2. What will you do in GitHub if you want to make your project more organized and efficient?

    a.  Create a project board in Github to track the progress
    b. Manually write down some updates in the excel sheet
    
### Question3
3. It is efficient to use GitHub Project in teamwork, and people can custom fields to track metadata.

    a. False
    b.  True
    
### Question4    
4. what should you do to keeo your project staying up-to -date with the information on GitHub?

    a.  Don't need to do anything and GitHub will help me do everything
    b. Manually update the information in project board
    
### Question5    
5. A public project board is visible to anyone with the project board's URL. So everyone who can view the project can edit the project.

    a.  False, only who has write access to the repository can edit it.
    b. True
    
### Question6
6. After adding a crad as a note to a project board and you find that it isn't sufficientr for you needs, you can still convert it to an issue.

    a. False
    b.  True
    
### Question7   
7.  You can filter cards using the following search qualifiers in any combination.

    a. Filter cards by author using `author:USERNAME`
    b. Filter cards by assignee using `assignee:USERNAME` or `no:assignee`
    c. Filter cards by label using `label:LABEL`, `label:"MULTI-WORD LABEL NAME"`, or no:label
    d. Type some text you'd like to search for
    e.  All above is correct
  
### Question8
8. You can manage your work on GitHub by creating labels to categorize issues, pull requests, and discussions. Once a label exists, you can use the label on any issue, pull request, or discussion within that repository.

    a. False
    b.  True
    
### Question9
9. You can copy a project board to quickly create a new project and reuse a project board's title, description, and automation configuration. 

    a. False
    b.  True
    
### Question10
10. One project can only be used with one repositories.

    a.  False, I can link up to twenty-five repositories to my organization or user-owned project board. 
    b. True
    
## Common Errors
1. If you get a message about git not being found, it means installation was unsuccessful or that it is not being found, i.e. it is not on your PATH. RStudio can only act as a GUI front-end for Git if Git has been successfully installed AND RStudio can find it. 

A basic test for successful installation of git is to simply enter git in the shell. 

You may be able to find Git after the fact with these commands in the shell :

-`which git` (Mac, Linux, or anything running a bash shell)

-`where git` (Windows, when not in a bash shell)

2. Be intentional about where you create this Project.

Click “Create Project” to create a new directory, which will be all of these things:

- a directory or “folder” on your computer
- a Git repository, linked to a remote GitHub repository
- an RStudio Project

Tips: Suggest you “Open in new session” in R.


## Next Step
You can take advantages of these GitHub project management features, such as GitHub repositories, issues, and project boards, to plan and track your work, whether working on an individual project or cross-functional team. You can read more [here](https://docs.github.com/en/issues)

## Reference

GitHub Docs. https://docs.github.com/en


