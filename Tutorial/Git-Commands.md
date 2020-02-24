# Purpose
This page serves as a mini cheat sheet / knowledge base for useful Git commands that we have used. 

If you encounter something weird, please still do google or consult the group.\
Everyone is encouraged to add commands / correct the knowledge here, alongside with a *concise* description.





# Common commands with options
### Getting remote files from Git
| Description | Command |
|---|---|
| Clone this repository. | `git clone git@gitlab.com:teem10/team10.git` |
| Pull all the updates in the **current** branch. Note this does **NOT** overwrite your local changes. | `git pull` or `git pull origin [branch_name]` |
| **Please** do this before you start any work. |  |



### Branching
| Description | Command |
|---|---|
| Create a new branch [branch_name]. | `git checkout [branch_name]` |
*(Before you do this, make sure to do `git pull origin master` while you're on the `master` branch)* |  |
| Switch to [branch_name]. | `git branch [branch_name]` |
| Create a new branch [branch_name], then checkout (switch) to that branch. | `git checkout -b [branch_name]` |
*(Before you do this, make sure to do `git pull origin master` while you're on the `master` branch)* |  |
| This is equivalent to `git branch [branch_name]` followed by `git checkout [branch_name]`. |  |



### Before/While adding files for a commit
There are some tricks in cmd for your to add/remove files precisely and quickly:
*  `[folder_name]/.` Adds all the (not-ignored) files under [folder_name].
*  `*.[extension]` Wildcard. For example, `*.pyc` refers to all files that has the extension `.pyc`.

| Description | Command |
|---|---|
| Check which files are staged & unstaged. | `git status` |
| Run this as many times as you can to confirm you have done the right thing **before** committing. |  |
| Add [filename] for your next commit. | `git add [filename]` |
| Add **all** files under your current directory. | `git add .` |
| Unstage (undo the "add") [filename] for your next commit. | `git reset HEAD [filename]` |
| Unstage (undo the "add") **all** files under your current directory. | `git reset HEAD .` |



### Committing
Commit [messages](https://chris.beams.io/posts/git-commit/) should be:
* Atomic
* Conclusive
* In imperative mood (e.g. "Create customer homepage" rather than "Create**d** customer homepage")

| Description | Command |
|---|---|
| Ah, our favourite command | `git commit -m "[message]"` |
| Push local committed changes onto the repository. At the bare minimum, do this every time you get off work. | `git push` or `git push origin [branch_you_are_in] |





# Less common commands
### Viewing history
| Description | Command |
|---|---|
| Display the full history of this branch. | `git log` |
| Display the history of this branch, showing only the titles. | `git log --oneline` |
| Display the history of this branch, showing only the titles, and grouped by users. | `git shortlog` |



### Branching
| Description | Command |
|---|---|
| Display available branches in this repository. | `git branch` |
| Delete the **not-yet-pushed** local branch [local_branch_name]. | `git branch -d [local_branch_name]` |



### Pushing
| Description | Command |
|---|---|
| Push all


# To be documented/tested
* Force git pull: https://itsyndicate.org/blog/how-to-use-git-force-pull-properly/
* `git revert ...`
* For commits, there is some way to write a body. Check [this](https://chris.beams.io/posts/git-commit/) out if you want more knowledge.