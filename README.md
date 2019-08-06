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
```shell
DN52eo2r:example_github_repo lfresard$ echo "# github_tutorial" >> README.md
```


```shell
DN52eo2r:example_github_repo lfresard$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)

    README.md

nothing added to commit but untracked files present (use "git add" to track)

```


```shell
DN52eo2r:example_github_repo lfresard$ git add README.md 

DN52eo2r:example_github_repo lfresard$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
 	new file:   README.md

```



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



