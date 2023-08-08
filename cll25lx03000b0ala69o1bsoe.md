---
title: "Day 5 = Source Code Management - Git & Github Advanced"
datePublished: Tue Aug 08 2023 10:23:48 GMT+0000 (Coordinated Universal Time)
cuid: cll25lx03000b0ala69o1bsoe
slug: day-5-source-code-management-git-github-advanced
tags: linux, github, git, devops90days

---

### 🌿 **Branching Strategies in 2018:**

Back in 2018, there were three essential branching strategies commonly used in software development:

1. **Master Branch**: This branch represented the stable and production-ready code. Changes from other branches, such as the staging and development branches, were merged into the master branch once thoroughly tested and approved.
    
2. **Staging Branch**: The staging branch served as a pre-production environment where further testing of features and bug fixes occurred. This step allowed developers to ensure a higher level of code quality before merging into the master branch for release.
    
3. **Develop Branch**: The develop branch acted as the central codebase for ongoing development work. Developers created individual feature branches from the develop branch to work on specific tasks and features.
    

* *Feature Branches*: Within the develop branch, developers worked on separate tasks in dedicated feature branches. For example, Feature 1, Feature 2, and Feature 3 were created as separate branches to develop different functionalities.
    

### 🛠️ **Handling Errors with Git Revert and Git Reset:**

In the development process, errors or bugs are inevitable. When an issue arises in the develop branch, developers have a couple of powerful tools at their disposal to address them: `git revert` and `git reset`.

1. **Git Revert**: When a mistake is made in the develop branch, developers can use `git revert` to undo specific commits while keeping the commit history intact. This means that the erroneous changes are reversed, and a new commit is created to record the reversal. This approach ensures that the changes are safely removed without affecting the branch's history.
    
2. **Git Reset**: On the other hand, `git reset` allows developers to move the branch pointer backward to an earlier commit, effectively "rewinding" the branch's history. This approach is useful when developers need to completely undo the changes and discard any commits after the reset point. However, it's important to note that using `git reset` can result in the loss of commit history, making it a more drastic operation compared to `git revert`.
    

### 📝 **Real-World Example in 2023:**

Fast forward to 2023, the company's branching strategy has evolved, and they have embraced a more detailed approach to manage their development process.

* [**Prd.app.com**](http://Prd.app.com): Represents the production environment where the stable and thoroughly tested code is deployed.
    
* [**Stg.app.com**](http://Stg.app.com): The staging environment serves as a pre-production testing ground, enabling rigorous evaluation of new features before they are promoted to production.
    
* [**Dev.app.com**](http://Dev.app.com): The development environment is where developers work on various tasks assigned through Jira, a popular issue and project tracking tool.
    
    * *Jira Task Branches*: For better organization, each task assigned via Jira is tackled in its own dedicated branch, such as Jira Task 1, Jira Task 2, and Jira Task 3. This approach allows for efficient collaboration among team members and better tracking of progress.
        

### 🌿 **Git Cherry-Pick**:

`git cherry-pick` is a useful command in Git that allows you to apply a specific commit from one branch to another. It is handy when you want to pick specific changes from one branch and apply them to another without merging the entire branch.

### 🌿 **Git Stash**:

`git stash` is a command that temporarily stores your uncommitted changes in a "stash" so that you can switch to another branch without committing them. It is useful when you need to switch branches but don't want to commit your changes yet.

### 🌿 **Git Branch - Delete**:

`git branch -d <branch-name>` is used to delete a local branch in Git. It removes the specified branch from your repository. If the branch contains unmerged changes, you need to use the `-D` flag to force the deletion.

### 🌿 **Git Conflict**:

Git conflicts occur when two or more branches have made conflicting changes to the same file or code. Git displays these conflicts as markers in the affected file, and you need to manually resolve them before committing the changes.

### 🌿 **Git Merge**:

`git merge` is used to combine changes from one branch into another. It integrates the changes from the specified branch into the current branch. Conflicts may arise during the merge, which requires manual resolution.

### 🌿 **Git Merge Dev --squash**:

`git merge <branch-name> --squash` is a merge option that combines the changes from the specified branch into the current branch as a single, squashed commit. This means that instead of a full merge with all commit history, it appears as a single commit with the combined changes from the other branch.

In summary, Git provides a variety of powerful commands to manage branches, handle conflicts, and merge changes between branches. Git cherry-pick allows for selective application of commits, git stash helps in temporarily storing uncommitted changes, git branch - delete deletes local branches, and git merge combines changes between branches. Conflicts may arise during merges, which require manual resolution, and git merge dev --squash enables squashing changes from one branch into a single commit. Mastering these commands is essential for effective version control and collaboration in Git-based projects.

With this advanced branching strategy and the use of Git revert and reset when necessary, the company has significantly improved its development process, resulting in smoother collaboration, more reliable code, and faster issue resolution.