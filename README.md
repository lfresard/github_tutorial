## 1. Create a local git repository
### 1.1 Open a terminal and move to where you want to place the project on your local machine

```shell
DN52eo2r:Stanford lfresard$ cd 2019_08_workshopweek/
DN52eo2r:2019_08_workshopweek lfresard$ mkdir example_github_repo
```
### 1.2 Initialize a git repository
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
Your `README.md` is tracked but not yet commited. To register the changes you made in your repository you need to add and commit files that were created or modified.

```shell
DN52eo2r:example_github_repo lfresard$ git add README.md 
```

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

From here you have two options:
* either you want to write over existing files in your directory (typically this is your repo and you want to make the changes you intended to do.
* or you don't want to overwrite anything from the master directory for now, and you will create a branch to put your changes on.


## 4. Push to the existing repository
```shell
DN52eo2r:example_github_repo lfresard$ git push -u origin master
Counting objects: 3, done.
Writing objects: 100% (3/3), 266 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/lfresard/github_tutorial.git
   a8496a8..07de7c9  master -> master
Branch master set up to track remote branch master from origin.

```



