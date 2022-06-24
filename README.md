# Git commands
# My Table of content
- [Basic Commands](#basic)
- [Graph representation](#graph)
- [Merging](#merge)
- [Detached HEAD](#detached)
- [Work in progress managment](#stash)
- [Git config file](#gitconfig)
- [Github](#github)



<a name="basic"></a>
## Basic commands 

Initialize
```
git init
```

Retrieve logs
```
git log
```

Retrieve status on the current branch(HEAD)
```
git status
```

Rename local branch from master to main
```
git branch -m master main
```

Add a file to staging
```
git add <filename>
```

Add all files in the folder
```
git add .
```

Commit the changes
```
git commit -m "MESSAGE"
```

Know on what branch we are
```
git branch
```

Create new branch
```
git branch <newbranchname>
```

Move to a branch
```
git checkout <branch>
```

Create and directly checkout a new branch
```
git checkout -b <newbranch>
```

## Graph representation <a name="graph"></a>

```
git log --all --decorate --oneline --graph
```

To create an alias:

```
alias graph="git log --all --decorate --oneline --graph"
```

## Merging <a name="merge"></a>
  Fast forward merge (inheritance path between the 2 branches). If not on same inheritance path then a 3 way merge is applied with a commit and a commit message.
  Get first on the branch you want to merge into (e.g. master).
  ```
  git merge <branch to merge from>
  ```

  Review the merged branches
  ```
  git branch --merged
  ```


  Delete branch
  Can only delete merged branches with -d. If want to delete unmerged branches -D must be used.
  ```
  git branch -d <branch to delete>
  ```

Review the difference between 2 branches
```
git diff <branch1>..<branch2>
```

Aborting a merge
```
git merge --abort
```

When there is a merge conflict one has to open the files shown in red during the merge tentative, review the separation between HEAD and the `branch` we want to merge from. Remove the markers `(<<<<<<<,` `HEAD`, `=======,` `<branch>,` `>>>>>>>>>)` and save the file.

Then we have to stage again and commit the file using git commit without message to open the editor for review.

If one wants to merge different histories we can use:
```
git merge origin/main --allow-unrelated-histories
```

## Detached HEAD <a name="detached"></a>

Checkout on a commit hash instead of a branch. The commit has is the first 7 characters of the 40 characters commit hash.
```
git checkout <xxxxxxx>
```
Create a new branch on the detach head
```
git branch <newbranch>
```

```
git checkout <newbranch>
```

## Work in progress managment <a name="stash"></a>
If one wants to move from branch to branch without staging/commiting file updates we can stash.
```
git stash
```

Several stashes can be created in the same branch, to see the list:
```
git stash list
```

To observe the edits we can add -p
```
git stash list -p
```

Once we want to apply the changes:
```
git stash apply
```

## Git config file <a name="gitconfig"></a>

> It is creating a branch 'master' and that branch I am not able to merge into the 'main' branch. (It show nothing in common so cannot merge)
> Sorry if it is a silly question, but I am trying this thing and stuck since many days. Any help would be much appreciated.

Not a silly question, I struggled until finding out that GitHub is now using `main` by default instead of `master`.
If locally your HEAD is on master then you can rename the branch so:
```
git branch -m master main
```

Now in the init config file you can change the default branch name. Access the global config here:
```
git config --global --edit
```
find 
```
[init]
  defaultBranch = master
```
and replace master by main
```
[init]
  defaultBranch = main
```
save and exit and voila!
This was very helpful for me, hope it was of some use for you too!!

## Github <a name="github"></a>

Rename local branch
```
git branch -m master main
```

Add origin URL
```
git remote add origin URL
```

Initial push
```
git push --set-upstream origin main
```

Force your local repo to github if any problem (this will overwrite your github repo content!!)
```
git push origin main --force
```

It is possible to merge 2 different pieces of code with unrelated commit histories.

> ```
> hint: Updates were rejected because the remote contains work that you do
> hint: not have locally. This is usually caused by another repository pushing
> hint: to the same ref. You may want to first integrate the remote changes
> hint: (e.g., 'git pull ...') before pushing again.
> hint: See the 'Note about fast-forwards' in 'git push --help' for details.
> ```
> 
> 
> Force it:
> ` git push --set-upstream origin master --force`

This might happen if you create a new github repo with a readme file. It could also be totally different code and somehow you feel confident to merge. Then you can do a fetch of the github repo:
```
git fetch
```

Followed by a merge with --allow-unrelated-histories:
```
git merge origin/main --allow-unrelated-histories
```
When the commit file opens just save it or update it.
Then you are ready for the push
```
git push origin main
```
This will sync your local repo with your remote repo (origin on branch main).

Here I used main because github is now using main by default instead of master.
If locally your HEAD is on master then you can rename the branch so:
```
git branch -m master main
```
