
# GIT OFFICIAL DOC

https://git-scm.com/doc

# GIT BASICS AND CONCEPTS

Git is a control version system. Just a tool to manage, and organize file versions. It is a fundamental knowledge for any software developer (writers and others too), because it is the most common way to share your code with others or just with yourself in case you move to another computer.

## Basically you can do things like:

- Save your code remotely as a backup
- Have a log of your versions of every file of the project.
- Control the software development flow when you are in team. Several users can work in the same project, so it is easy to know who and when did anything else.
- Go back to an old version if needed
- Share code with teammates 
- And so much more...


# GIT GLOSSARY

Working directory &rarr; root folder. Where .git is. Local repository

Staging area &rarr; files add/prepared to be commited

Index &rarr; = staging area

Origin &rarr; default remote repository name. Also called as upstream by default

HEAD &rarr; Current branch pointer. HEAD points to actual branch and branch points to a commit (usually last commit) 

Detached HEAD &rarr; When HEAD points to an old commit of the current branch

# GIT COMMANDS

git init &rarr; inititate git repository on that folder

git status &rarr; show status of the actual local git repository

git log &rarr; repository log info

git log --oneline &rarr; repository log info abbreviated to one line per commit

## COMMIT

git add . &rarr; add to staging all files with changes

git add "file" &rarr; add file to staging

git commit &rarr; open default text editor and wait until save and exit to commit

git commit -m "commit description starting with imperative verb prefered" &rarr; most common use of commit

git commit --amend &rarr; recommit previous commit. It opens default text editor

git commit -a -m "commit message" &rarr; add all modified files and commit in one step

## IGNORE 

official doc &rarr; https://www.git-scm.com/docs/gitignore

tool for default gitignore files &rarr; https://www.toptal.com/developers/gitignore/

create .gitignore on root folder git repository to avoid git to track specificied files or folders

## BRANCH

git branch &rarr; list branches from the repository

git branch "new branch name" &rarr; create a branch from the current HEAD

git switch "branch name to switch" &rarr; switch to that branch. If you have not that branch locally, but you do remotely, it will connect to remote branch and create same locally

git switch -c "new branch name" &rarr; create a new branch and switch

git checkout "branch name" &rarr; same function as switch. It is the older way. Still common though

git checkout remotename/branchname &rarr; point to that remote branch

git branch -d "branch name" &rarr; Delete branch. You cant do it if your are in this branch

git branch -m "branch name to rename" "branch new name"&rarr; rename name of a branch

git branch -r &rarr; show remote branches

## MERGE

git merge "branch to merge from" &rarr; merges the commits from a branch to actual HEAD
if your feature branch just has commits that master doesnt and master does not have any new commit, i will be a Fast Forwards merge. I will just move master to feature branch HEAD.

My  feature branche has two commits, master, where i am going to merge, has one new commits. Master commit affects to a file that is not in conflict with anu of my commit files. When git merge, git will do a merge commit, will merge both branches, but will add a commit with a comment of "Merge branch 'branch name'" at head of master.

If master has a commit that involves a file that is in my feature branch commit, when merge, there will be a conflict. Git will ask me to choose a version. Every file with conflcit will have some tags to refer the conflict. 

        Tags are <<<<< HEAD
        changes of my HEAD
        =================
        changes from the other branch
        <<<< branch name 

## REBASE

Is another way to merge branches but with difference es with merge command 
It can be nice to uso for cleanup commit history 

### Rebase vs Merge
When we use git merge in a large team or a concurrent project, we have to update our feature branch often. That makes commit log to get dirty. It is not really smooth.

With rebase, if master changed we can use it to re base out branch commits just after the new commits coming from master. Not in the middle with merge. It is like if you created your feature branch with that last master version.

### The GOLDEN RULE:

DO NOT REBASE THE MASTER BRANCH FROM ANOTHER BRANCH because that history is sharted with other persons and then can be difficult to restore.

Just rebase from master when you are in your feature branch

git rebase branchname &rarr; bring new commits from branchname and rewrite them before my feature branch commits

if conflicts, i have to choose a version as we do with merge. After that, git add that files and 

git rebase --continue &rarr; continue with rebase when were conflicts
git rebase --abort &rarr; abort rebase operation

### interactive rebase
entering this mode ables us to edit commits, add files, drop commit..etc from our HEAD to a specific commit
git rebase -i 7dcd78a &rarr; Enters in interactive rebase mode, and shows all commits from specified to HEAD. For every commit, we can do an action. All actions are listed down. Every commit since specified will change its hash


## DIFF

shows the difference between two spots of the repository. it could be between working directory, HEAD, staged files, commits, branches...etc.

git diff &rarr; showsw difference between working directiory and staged files

git diff HEAD &rarr; shows difference between working directory and HEAD (last commit of actual branch)

git diff HEAD filename.txt &rarr; shows difference between staged file and same file in HEAD

git diff --staged &rarr; shows difference between staged files and HEAD
    

## STASH

You can stash changes of working directory working + stage area and change to another branch if needed.
it is like to save a version on a memory, and if we want to recover those changes back, we just use unstash

git stash &rarr; save changes and rollback to previous commit. Now you can change to another branch of commit without problemas.
git stash pop &rarr; apply stashed changes to current version and remove stash
git stash apply &rarr; apply stashed changes to current version and dont remove stash
git stash list &rarr; list the stashes. You can stash several changes in distinct stashes


### UNDO changes and time travel 

We can checkout to a previous version. To a previous commit in order to see how the code was at that point. Or we could even create a new branch based on a previous commit. For that, we checkout to that commit, pointing HEAD to that branch &rarr; commit.

git checkout "commit-hash" &rarr; set HEAD to point to that branch commit

git checkout HEAD~n &rarr; same as before but you can checkout by HEAD number. Being HEAD the last, 1 previous and so forth

git switch "branch name" &rarr; to recover the real HEAD of that branch where we checkedout to previous commit

git checkout HEAD &rarr; discard changes from working directory and reset to HEAD version

git restore "file name" &rarr; reset file to HEAD version 

git restore --staged "filename" &rarr; unstage file that was staged. It doesnt restore the content of the file, just removes it from staged area

git reset "commit-hash" &rarr; it will remove commits between actual HEAD and that commit. Then it points HEAD to that commit.

Dont use git reset if you are working with other people, because it will be hard to concile 

git reset --hard "commit-hash" &rarr; same as before, but, it also revert working directory to state of the commit. WARNING! you will lose your files and changes.

git revert "commit-hash" &rarr; it will also undo changes, but instead of remove any commit from branch, it will create a new commit with reverted version. Use revert instead of reset if you ever pushed to an origin repo that other people may be using.

## REMOTE 

It is used to connect a local repo to a remote repo. Usually to github , bitbucket, gitlab...etc

git remote add "name" "url remote repo" &rarr; connect local repo to a remote one. Usually name param is origin. Usually git push origin master

git remote rename "oldname" "newname" &rarr; just rename de remote repo

## PUSH 

git push "remotename" "branchname" &rarr; update the branch in remote with commits in your local + 

You dont really have to be on the branch you want to push

## FETCH

It will update the local repository from the remote, but wont touch my working directory. It update my local origin/master (for example)

We could for example, fetch and then work with the last version of remote if we dont have internet and of course, no one pushed any commit to remote repo

git fetch remotename &rarr; bring remote changes to local repo

git fetch remotename brachname &rarr; bring specific branch changes from remote


## PULL

It will bring changes from remote, but also, will merge them into out working directory. Into our HEAD.
pulling can provoke conflicts between your working directory and remote changes. You will need to resolve then to choose a final version for your working directory

git pull remotename branchname &rarr; it actually will fetch to local repo + merge to our working directory

git pull &rarr; it will do the same, just bringing changes from the remote default tracking branch.


## GIT WORKFLOWS

### Centralized - only one branch (master)

Not ideal for teams where you want to share code, because u have to pull and push to master for that.

as it is constantly commited by others, devs have to resolve conflicts frequently
Not the best option for experiments

### Feature branches. Create a branch per feature/fix/anychange

Most common flow. 
- You can share code just by switching to a branch
- master wont have broken or experimental code
- master will have a real history commits

### Fork & Clone

Used mainly for big open source projects when we dont have permisions to push. 

So we can fork a repo, creating then an own copy of the repo. There, we can push without problems and create pull requests to the original project. Owners of it can accept and merge our changes. 

That is the way of collaborating with open source projects, for example.

