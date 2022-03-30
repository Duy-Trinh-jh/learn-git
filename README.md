# learn-git
## What is Git and Advantages of Git

### Git concept
> Git is the most commonly used Distributed Version Control System to store all files. It helps software developers can work together and maintain a complete history of their work.

### Advantages of Git
- Free and Open Source
- Enable team collaboration
- Easy to try new thing without worrying about affecting the important version
- Manage the history of work
- Recover source code from the other

## Commit 

### What is commit?
> The git commit command captures a snapshot of the project's currently staged changes.

Commit options:
- -m: set the commit's message
```
git add index.html
git commit -m "message"
```
- -a or -all: Commit a snapshot of all changes in the working directory
```
git commit -a -m "message"
```
- -amend: Passing this option will modify the last commit. Instead of creating a new commit, staged changes will be added to the previous commit. 
```
git commit -amend
```
### How to write good commit message:

Syntax:
```
git commit -m "Subject" -m "Description..."
```

How to write good commit message:
- Specify the type of commit:
  - feat: The new feature you're adding to a particular application
  - fix: A bug fix
  - style: Feature and updates related to styling
  - refactor: Refactoring a specific section of the codebase
  - test: Everything related to testing
  - docs: Everything related to documentation
- Use the imperative mood in the subject line
- Use the body to explain what changes you have made and why you made them
- Do not end the subject line with a period
- Capitalize the subject line and each paragraph
- Do not think your code is self-explanatory
- Follow the commit convention defined by your team

### List of posible issues when a commit is broken:
- Wrong commit's message, we can use -amend to retype message:
```
git commit -amend
```
- Commit wrong file but your teammate pulled it and we want to remove this commit:
```
git revert <commit-id>
```
- Commit wrong branch
```
# Create new branch has this commit from wrong branch
$ git branch other-branch
# Reset HEAD, index of branch to previous commit
$ git reset --hard HEAD~
# Check out to new branch
$ git checkout other-branch
```
- Someone accidentally remove a important commit:
```
# View commit history
$ git reflog
# Choose commit that you want to restore
# Ex: git reset --hard HEAD@{2}
$ git reset --hard <commit>
```

## Branch

### Git command for branch
This command lists all the local branches in the current repository
```
git branch or git branch -a
```
This command creates a new branch
```
git branch new-feature
```
This command is used to switch from one branch to another
```
git checkout feature
```
This command will create new branch and move to it:
```
git checkout -b new-feature
```

### List of posible issues when a branch has problems:
- Wrong branch's name, we can fix it with solution:
```
git branch -m <correct-branch-name>
```
- Checkout another branch without save changes in current branch:
```
# Save changes
$ git stash -u
# Checkout new branch and do something
$ git checkout -b other-branch
$ git add <list-of-file>
$ git commit -m "commit message"
# Checkout the previous branch
$ git checkout origin-branch
# Get all changes we did before
$ git stash pop
```
- Someone accidentally remove a branch:
```
# View commit history
$ git reflog
# Choose neccesary commit and create new branch
# Ex: git branch new-branch HEAD@{2}
$ git branch <branch-name> <commit-id>
```

## Basic git command

- Git add: This command adds a file to the staging area
```
git add <filename> or git add .
```
- Git push: This command sends the committed changes of master branch to your remote repository
```
git push <:remote:> <:branch:>
```
- Git pull: This command fetches and merges changes on the remote server to your working directory
```
git pull <:remote:> <:branch:>
```
- Git stack: This command temporarily stores all the modified tracked files
```
Example:
# Save changes
$ git stash -u
# Checkout new branch and do something
$ git checkout -b other-branch
$ git add <list-of-file>
$ git commit -m "commit message"
# Checkout the previous branch
$ git checkout origin-branch
# Get all changes we did before
$ git stash pop
```
- Git merge: this command merges the specified branch’s history into the current branch
```
git merge <branch-name>
```
- Git rebase: this command allows you to rewrite commits from one branch onto another branch
```
git rebase <branch-name>  
```

## Conflict

### What could cause code conflicts:
- Overlapping the scope of teammate's work
- getting git conflicts with yourself is often caused by the repo on your machine not being up to date with the current branch because some changes may have been committed in places you weren’t expecting or you’re switching between too many branches and not merging them

### How to resolve conflict
- Edit conflict files and then add, commit those file
- You should commit regularly: Do not commit a whole file chances, you should break down changes to commit for easily resolving conflict if exist
- You should pull changes from remote before starting work or commiting your changes
- You should create new branch for each feature to avoid conflicting between teammate

## Merge and Rebase

### Compare Merge and Rebase
- Sameness: Using to merge code from 2 branchs
- Difference: 
  - git merge: when this command merge 2 branchs, it sort the order of commit based on its time create. This command will compare content of 3 commit: the commit between 2 branchs and the last commit from 2 branchs. And then it merge into 1 commit has been handled conflict (if exist). Git merge keeps history tree.
  - git rebase: this command will get all commit from the merge branch to setup base. If conflict exist, we will resolve at conflict commit, and then this command will link the remain commit from current branch. Git rebase makes history of commit as the straight line from start to current

### Compose Merge and Rebase
It Based on the your purpose. We can use git rebase to get a much cleaner project historya, easily tracking commit later. Or we can use git merge to sort commit as default.

For example: If we want to keep commit from branch feature on branch master, we can use git rebase branch master on branch feature and then we use git merge to merge branch feature to branch master.

## Exercise
### Description: We have 2 big branch call master (to hold test features for test site) & production. 
### Exercise 1: (Ap & Ev) When we are creating new feature, what branch should we based on and why?
- When we are creating new feature, we should based on branch master because branch master holds test features so we can test carefully the new feature before merge it to other branch.
```
git checkout master
git branch <new-feature>
git checkout <new-feature>
```
- If new feature depend on other feature, we can create new branch base on this branch feature.
```
git checkout <another-branch>
git branch <new-feature>
git checkout <new-feature>
```
- If new feature depend on other features we can create new branch base on one of them and merge the rest of branch.
```
git checkout <first-branch>
git branch <new-feature>
git checkout <new-feature>
git merge <second-feature>
```
- If new feature depend on other feature but new feature only need some code from this, we can create new branch base on this branch and delete other code and commit the changes.
```
git checkout <feature>
git branch <new-feature>
#remove other code
git add .
git commit -m 'only keep the xxx module on new feature'
git push
```
### Exercise 2: (Ap) If we have a feature branch that haven't been merged to production and that branch have bug, what course of action are you going to do with Git to before resolving the bug?
- We checkout branch feature and then create new branch to fix bug. If we need some code from other branch, we checkout this branch and give the paths to the specific files that we want to add to branch fix bug.
```
git checkout feature
git checkout -b "feature/fix-bug"
#if we want to add some code from other branch, we can try this solution for add the specific files:
git checkout <other-branch> <paths>
git commit -m "Get some code from other branch"
#or we add all code from this branch
git merge <other-branch>
```
### Exercise 3: (Ap & Ev) If someone accidentally merge a feature (feature/delete-user) onto production and have a list of commitId ended with (0492978, fc9348c, k101100), then another commit (a1fsas8) is added on top of the production branch. How do we remove that merged feature?
- We checkout branch production and then we use git revert command to revert the commit merge and then we use git push to push this change to branch production. When we want to merge feature again onto production, we revert the revert commit and then merge feature.
```
git checkout production
git revert -m 1 a1fsas8
git push
#when we want to re merge feature onto production
git revert -m 1 <revert-commit-id>
git merge feature/delete-user
git push
```