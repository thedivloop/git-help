# Git commands

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

## Graph representation

```
git log --all --decorate --oneline --graph
```

To create an alias:

```
alias graph="git log --all --decorate --oneline --graph"
```

## Merging

Review the difference between 2 branches
```
git diff <branch1>..<branch2>
```

Aborting a merge
```
git git merge --abort
```

When there is a merge conflict one has to open the files shown in red during the merge tentative, review the separation between HEAD and the <branch we want to merge from>. Remove the markers (<<<<<<<, HEAD, =======, <branch>, >>>>>>>>>) and save the file.

Then we have to stage again and commit the file using git commit without message to open the editor for review.

## Detached HEAD

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

## Work in progress managment
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

## Github

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
