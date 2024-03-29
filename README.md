# GIT - GITHUB WORKSHOP
This is tutorial for basic working knowledge of GIT/GITHUB.
Created as part of the Montgomery lab workshops week in August 2019. You can also access the slides from this workshop [here](https://docs.google.com/presentation/d/1OuRVkk1c1FjLu0JWE4uUsjk8eqEWilczVa2DsF-n6bg/edit?usp=sharing).
Information here was for the most part retrieved from the resources cited at the end of this document. Those are good reads if you want to go further.

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
* Start a new feature
```shell
DN52eo2r:example_github_repo lfresard$ git checkout -b new_feature master
Switched to a new branch 'new_feature'
```
* Edit some files

```shell
DN52eo2r:example_github_repo lfresard$ touch new_script.sh
DN52eo2r:example_github_repo lfresard$ git add new_script.sh 
DN52eo2r:example_github_repo lfresard$ git commit -m "Start a script for new feature"
[new_feature d1f90ab] Start a script for new feature
 Committer: Laure Fresard <lfresard@DN0a238717.SUNet>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly. Run the
following command and follow the instructions in your editor to edit
your configuration file:

    git config --global --edit

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 new_script.sh
```
* Merge in the new_feature branch
```shell
DN52eo2r:example_github_repo lfresard$ git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 3 commits.
  (use "git push" to publish your local commits)
DN52eo2r:example_github_repo lfresard$ git merge new_feature
Updating 29b2962..d1f90ab
Fast-forward
 new_script.sh | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 new_script.sh
```
* Delete the branch
```shell
DN52eo2r:example_github_repo lfresard$ git branch -d new_feature
Deleted branch new_feature (was d1f90ab).
```

* Push those changes to the remote repository
```shell
DN52eo2r:example_github_repo lfresard$ git push -u origin master
Counting objects: 9, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (9/9), done.
Writing objects: 100% (9/9), 73.89 KiB | 0 bytes/s, done.
Total 9 (delta 4), reused 0 (delta 0)
remote: Resolving deltas: 100% (4/4), completed with 1 local object.
To https://github.com/lfresard/github_tutorial.git
   cdb3e2f..d1f90ab  master -> master
Branch master set up to track remote branch master from origin.
```

You can use this worflow when you are using branches for small changes that are isolated developments rather than organization tool for the development of long lasting features.

#### 5.2.3. 3-way merge
What if you are in a situation where while you a developping a new feature on an independant branch, the master branch keeps changing, or otehr branches are also being created by other developpers?
This is what you will encouter if you have a collaborative project and the fast forward merge cannot work here.

Let's make it an example:
```shell
DN52eo2r:example_github_repo lfresard$ git checkout -b great_feature
DN52eo2r:example_github_repo lfresard$ touch super_cool_scrip_idea.py
DN52eo2r:example_github_repo lfresard$ git add super_cool_scrip_idea.py 
DN52eo2r:example_github_repo lfresard$ git commit -m "develop super cool idea"
DN52eo2r:example_github_repo lfresard$ git merge great_feature
DN52eo2r:example_github_repo lfresard$ git branch -d great_feature
```


#### 5.2.4. Conflict resolution...
There is a conflict when the two branches you're trying to merge changed the **same part** of the **same file**. In those cases Git does not know which version to choose.
When this happens Git stops right before the merge commit so that you can resolve the conflict manually.
Here is what you can do:
* 1. Run `git status` to see which files are causing the problem
```
On branch master
Unmerged paths:
(use "git add/rm ..." as appropriate to mark resolution)
both modified: hello.py
```
* 2. Open your favorite text editor, and navigate to the file that has merge conflicts. To see the beginning of the merge conflict in your file, search the file for the conflict marker `<<<<<<<`. When you open the file in your text editor, you'll see the changes from the HEAD or base branch after the line `<<<<<<< HEAD`. Next, you'll see `=======`, which divides your changes from the changes in the other branch, followed by `>>>>>>> BRANCH-NAME`. 


```
# Print Hello World
<<<<<<< HEAD
print("Hello World")
=======
print("hello world")
>>>>>>> branch-a
```


* 3. Decide if you want to keep only your branch's changes, keep only the other branch's changes, or make a brand new change, which may incorporate changes from both branches. Delete the conflict markers `<<<<<<<, =======, >>>>>>>` and make the changes you want in the final merge.


* 4. Add your changes with `git add hello.py`

* 5. Commit your changes with a comment `git commit -m "Resolved conflict by keeping lower case version"`



### 5.5. Creating a pull request
When you do a pull request you are sending a message to your collaborators basically saying `"Hey am done with the changes on my side of the project can you guys have a look so we can merge it to the main project?"`
In that situation, in case of merging your modification using `git merge` you will file a `pull request`.


Practically you are requesting that the maintainer of the project pulls a branch of your repository to their repository.

* 1. One person creates the feature in a dedicated branch in their local repo.
* 2. He/She pushes the branch to a public Bitbucket/Github repository.
* 3. He/She files a pull request via Bitbucket/Github
* 4. The rest of the team review the cove, discusses it and alters it
* 5. The project maintainer merges the feature into the official repository and closes the pull request.

![Alt text](pull_request1.png?raw=true "Title")

## 6. Undoing mistakes

### Reverting (undoing) a commit

Say we delete a file, and then realize it was important only after committing the change.

```
DN52eo2r:example_github_repo git rm super_cool_scrip_idea.py
rm 'super_cool_scrip_idea.py'
DN52eo2r:example_github_repo git commit -m "deleted important file"
[master 551b2c4] deleted important file
 Committer: mikegloudemans
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 super_cool_scrip_idea.py
```

We use `git log` to view the changes and remember which commit was the one before we made a mistake.
```
DN52eo2r:example_github_repo git log --pretty=oneline
551b2c49847bdb8f62e9293def4b07f967810432 deleted important file
bce12d1a58fd490425f580c0ba094383ab4a5199 Added link to git best practices site
cebc1802c4c91f64a2404b10b1ecabf6ffd0f86d Update README.md
0876a41309ffc288d379b4e3084707d5facbe553 Update README.md
…
```

Then we use git revert to "undo" the last change (the one referenced by the pointer HEAD).
```
DN52eo2r:example_github_repo git revert HEAD
[master 36a6a69] Revert "deleted important file"
 Committer: mikegloudemans
 create mode 100644 super_cool_scrip_idea.py
```

Notice in the output that the operation is not recognized by Git as an undo, but as 
a `create` on the deleted file, the opposite of the `delete` that we reverted.
The git history itself is not changed because git revert doesn’t delete any previous commits. 
It just creates a new commit that is the opposite of the previous commit.

We verify now that we've fixed the issue:

```
DN52eo2r:example_github_repo git log --pretty=oneline
36a6a693ab4f14f484d57c4ec2ad3ddeaab5a85b Revert "deleted important file"
551b2c49847bdb8f62e9293def4b07f967810432 deleted important file
bce12d1a58fd490425f580c0ba094383ab4a5199 Added link to git best practices site
cebc1802c4c91f64a2404b10b1ecabf6ffd0f86d Update README.md
...
```

We can also check with `ls` to see that the file is back.

Like a typical undo operation, `git revert` can be used successively as many times as needed to get 
back to the desired project version. In the above example, if we wanted to continue undoing
changes, we could use `git revert bce12d1a58fd490425f580c0ba094383ab4a5199`, then `git revert cebc1802c4c91f64a2404b10b1ecabf6ffd0f86d`, etc.
It's important here though that we tell it which (older) commit to undo; otherwise it will just go back and forth between
deleting and restoring the deleted file instead of going further back in commit history.

### Recovering deleted files with `git checkout`

Suppose instead that we accidentally deleted the file from our local directory using the standard Linux
`rm` (instead of `git rm`). 

```
DN52eo2r:example_github_repo rm super_cool_scrip_idea.py
```

Since Git is smart and thinks we're smart too, it assumes this change was intentional.
We haven't committed this change yet (and git doesn't know about it at all yet),
so using `git revert` won't help us out. Luckily, we can recover it at any time
by just checking it out from the master branch:

```
DN52eo2r:example_github_repo git checkout HEAD super_cool_scrip_idea.py
```

and a quick `ls` shows that we've restored the deleted file.


## Resources
* Getting Started - [Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [Become a git guru](https://www.atlassian.com/git/tutorials).
* An Intro to Git and GitHub for Beginners ([Tutorial](https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners))
* [Resolving conflicts](https://help.github.com/en/articles/resolving-a-merge-conflict-using-the-command-line)
* [Git best practices](http://sethrobertson.github.io/GitBestPractices/)

