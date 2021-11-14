# Louis's git Cheat Sheet for INFO340
Literally all the git commands you ever need to use for INFO340.

## Sanity Check
```git status```: check what files have been changed since the last commit and what branch you are on.

## Pushing to git Trifecta

```git add .```: add **all** files that have been changed since the last commit to the staging area. It tells git that you want to include updates to those files in the next commit. 

> Less common: you can individually add files you want to add to the staging area using:
> ```
> git add filename
>```
```git commit -m "what you did"```: captures a snapshot of the project's currently staged changes (like pressing 'Save' on a word doc). Saves your changes to the _local repository_ (your machine only). Note: the ```-m``` flag takes in a string of what you did / what the commit will update. The message should be short and complete this sentence: If applied, this commit will {your message}.

```git push```:  transfer commits from your local repository to a remote repository (i.e. GitHub). 

## Working with Branches

```git checkout -b your-new-branch-name```: create a new branch in the repo. Note: the ```-b``` flag takes in the name of your new branch.

Whenever you create a branch and push for the first time, you need to set up the upstream. Meaning you only created the branch locally on your machine, not on the remote repository. So you need to push your branch as well. Just follow the command git prompts you to do.
```
fatal: The current branch your-new-branch-name has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin your-new-branch-name 
```

```git checkout existing-branch-name```: switch to an existing branch.

## Merging to main
### Golden rule 1: you always merge onto yourself
### Golden rule 2: all changes come to main already committed, so you just need to push

Let's say you are on a branch called louis-branch (or any branch that is not on main) and want to merge your new changes. 
Follow the pushing to git trifecta:
```bash
git add . # add my changes to staging area
git commit -m "message" # save snapshot of updates locally
git push # upload all of my local changes to the remote repository
```

Then, switch to main to make it up to date with your branch that you just updated.

```bash
git checkout main # switch to main branch 
git merge louis-branch # you merge onto yourself
git push # because you are changing your local version of main, you'll need to push the changes for everyone to see on the repository
```
Note, you can ```checkout``` to another branch (not just main) if you wish to merge changes there instead.

## Merging from main
Let's say you have updates from main that you need locally (your teammate just pushed changes).

```bash
git status # check if you are in the correct branch you want to recieve changes in (i.e. main)
git pull # pull the changes that someone else has pushed
```
Taking this one step furthur, let's say you need to merge those changes from main to another branch/
Assumming you're on a branch called louis-branch (or any branch that is not on main):
```bash
git checkout louis-branch # switch to the branch you want to apply changes to
git merge main # you merge onto yourself
```

## Tips to Avoid Merge Conflicts

1. Always pull before you push
2. More often than not, you will 'Accept Incoming Change' to resolve merge conflicts (in your text editor)
3. Confirm with your teammates on how to resolve the conflicts just in case you lose code (THIS HAS HAPPENED TO ME BEFORE)
4. Use your text editor to help you with merge conflicts (i.e. VSCode has text you can click on)

## "I fked up"

```git stash```: remove all changes to the files you made locally and revert to the old state of since the last commit. Useful when you have been working on code that no longer has a use.

```:wq```: exit vim. Sometimes you'll enter vim, the text editor that git uses. 