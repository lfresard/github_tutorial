This is a beginner's tutorial for basic working knowledge of github.
Created as part of the Montgomery lab workshops week in August 2019. You can also access the slides from this workshop [here](https://docs.google.com/presentation/d/1OuRVkk1c1FjLu0JWE4uUsjk8eqEWilczVa2DsF-n6bg/edit?usp=sharing).
Information here was for the most part retrieved from the ressources cited at the end of this document. Those are good reads if you want to go further.

## 1. Create a local git repository
### 1.1. Open a terminal and move to where you want to place the project on your local machine

```shell
DN52eo2r:Stanford lfresard$ cd 2019_08_workshopweek/
DN52eo2r:2019_08_workshopweek lfresard$ mkdir example_github_repo
```
### 1.2. Initialize a git repository
```shell
DN52eo2r:example_github_repo lfresard$ git init
Initialized empty Git repository in /Users/lfresard/Documents/Stanford/2019_08_workshopweek/example_github_repo/.git/
```

## 2. Add a new file to the repo

Let's create a README for your repository
```shell
DN52eo2r:example_github_repo lfresard$ echo "# github_tutorial" >> README.md
```

To see the effects of adding this file you can type `git status`

```shell
DN52eo2r:example_github_repo lfresard$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)

    README.md

nothing added to commit but untracked files present (use "git add" to track)

```
Your `README.md` is tracked but not yet commited. To register the changes you made in your repository you need to add and commit files that were created or modified. The `git add` command adds a change in the working directory to the staging area. 

```shell
DN52eo2r:example_github_repo lfresard$ git add README.md 
```
It tells Git that you want to include updates to a particular file in the next commit. However, git add doesn't really affect the repository in any significant way—changes are not actually recorded until you run git commit.
You can check how things changed by running  `git status` again

```shell
DN52eo2r:example_github_repo lfresard$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
 	new file:   README.md
```
Now `README.md` is tracked. But as you can see, changes still need to be committed.

## 3. Commit your file
The `git commit` command captures a snapshot of the project's currently staged changes. Committed snapshots can be thought of as “safe” versions of a project—Git will never change them unless you explicitly ask it to. 



```shell
DN52eo2r:example_github_repo lfresard$ git commit -m "create a readme file"
[master 7ad32bb] create a readme file
 Committer: Laure Fresard <lfresard@DN52eomc.SUNet>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly. Run the
following command and follow the instructions in your editor to edit
your configuration file:
    git config --global --edit
After doing this, you may fix the identity used for this commit with:
    git commit --amend --reset-author
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```


## 4. Push to the existing repository
In addition to `git add` and `git commit`, a third command git push is essential for a complete collaborative Git workflow. `git push` is utilized to send the committed changes to remote repositories for collaboration. This enables other team members to access a set of saved changes.
Here the changes to your files will overwrite the original files in the remote repository.

```shell
DN52eo2r:example_github_repo lfresard$ git push -u origin master
Counting objects: 3, done.
Writing objects: 100% (3/3), 266 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/lfresard/github_tutorial.git
   a8496a8..07de7c9  master -> master
Branch master set up to track remote branch master from origin.
```

## 5. Branches
Git branches are effectively a pointer to a snapshot of your changes. When you want to **add a new feature** or **fix a bug**—no matter how big or how small—you spawn a new branch to encapsulate your changes. This makes it harder for unstable code to get merged into the main code base, and it gives you the chance to clean up your future's history before merging it into the main branch.


![Alt text](branches1.png?raw=true "Title")

A branch represents the tip of a series of commits—it's not a container for commits. 

### 5.1. Create a new branch
The first step is to create a branch on which you will work. For this you can use either `git branch <branch>`, which does not check out the new branch, or `git checkout -b <branch>` which creates the branch and checks out.

```shell
DN52eo2r:example_github_repo lfresard$ git checkout -b new_branch
Switched to a new branch 'new_branch'
```
After that command you are automatically switched to the new_branch and off the master branch.

If you want to confirm your new branch was created you can run `git branch`.

This lists all of the branches in your repository. This is synonymous with `git branch --list`.

```shell
DN52eo2r:example_github_repo lfresard$ git branch
  master
* new_branch
```

The `*` is a pointer to the branch you're at at a given time.

### 5.2 Git merge

Merging is Git's way of putting a forked history back together again. The `git merge` command lets you take the independent lines of development created by git branch and integrate them into a single branch.

The changes are affecting the **current branch**.
 

Merging is Git's way of putting a forked history back together again. The git merge command lets you take the independent lines of development created by git branch and integrate them into a single branch.

Note that all of the commands presented below merge into the current branch. The current branch will be updated to reflect the merge, but the target branch will be completely unaffected. Again, this means that git merge is often used in conjunction with git checkout for selecting the current branch and git branch -d for deleting the obsolete target branch.

How it works
Git merge will combine multiple sequences of commits into one unified history. In the most frequent use cases, git merge is used to combine two branches. The following examples in this document will focus on this branch merging pattern. In these scenarios, git merge takes two commit pointers, usually the branch tips, and will find a common base commit between them. Once Git finds a common base commit it will create a new "merge commit" that combines the changes of each queued merge commit sequence.

Say we have a new branch feature that is based off the master branch. We now want to merge this feature branch into master.
![Alt text](branches2.png?raw=true "Title")

When you use `git merge` you will merge the specified branch feature into the current branch, we'll assume master.
![Alt text](branches3.png?raw=true "Title")

If Git encounters a piece of data that is changed in both histories it will be unable to automatically combine them. This scenario is a version control conflict and Git will need user intervention to continue. 



#### 5.2.1. Preparing to merge
Before merging make sure of a couple of things:
* Confirm that you are currently on the branch you would like to merge the changes to (most likely `master`). If you are not then use `git checkout <receiving-branch>` to change.
* Make sure the receiving branch and the merging branch are up-to-date with the latest remote changes. Execute `git fetch` to pull the latest remote commits. Once the fetch is completed ensure the master branch has the latest updates by executing `git pull`.


#### 5.2.2. Fast forward merge



### 5.2 Push branch to Github

```shell
DN52eo2r:example_github_repo lfresard$ echo "new test" >>README.md 
DN52eo2r:example_github_repo lfresard$ git commit -m "add new step in readme"
On branch new_branch
Changes not staged for commit:
	modified:   README.md

no changes added to commit
DN52eo2r:example_github_repo lfresard$ git push -u origin new_branch
Counting objects: 20, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (13/13), done.
Writing objects: 100% (20/20), 3.40 KiB | 0 bytes/s, done.
Total 20 (delta 5), reused 0 (delta 0)
remote: Resolving deltas: 100% (5/5), done.
remote: 
remote: Create a pull request for 'new_branch' on GitHub by visiting:
remote:      https://github.com/lfresard/github_tutorial/pull/new/new_branch
remote: 
To https://github.com/lfresard/github_tutorial.git
 * [new branch]      new_branch -> new_branch
Branch new_branch set up to track remote branch new_branch from origin.
```

### 5.5. Create a pull request
![Alt text](pull_request1.png?raw=true "Title")

## Ressources
* Getting Started - [Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [Become a git guru](https://www.atlassian.com/git/tutorials).
* An Intro to Git and GitHub for Beginners ([Tutorial](https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners))


