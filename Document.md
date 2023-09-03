# Git 

    It is version control system in simple word it tracks all the changes you made in your files where it is initiated by taking snapshot of what is the difference between previous and current states of the file.

## Use Case

    Your are building a website for e-commerce company you done with your coding part and deployed it .After deployed you noticed that you made a spelling mistake in the button.

    To make the mistake you have two method 
    1. You can stop the peoduction server and make changes and again deploy it
    2. If you used git you can go to previout state and host that application while you work in the button changes

    We can make use of the github which git hosting service where we can create an remote repository so team can easily work among themselves by pull and pushing codes, Resolving conflicts and it give tract who changes which file.

## Git Command

- git init : Saying git to track the changes in the repository where we run the command and it will create a ".git" file a hidden file where it store the snapshot,log,configuration,remote link etc.,

```
On Running the above command git start to track the changes on running git status it will so the details of what files in which area

git has three area of tracking the file

working area - it is the area where changes made file are shown

by adding using git add 

The file are move to staging area where it ready for commiting / making a checkpoint / ready for git to take snapshot

by executing git commit

we made a checkpoint/snapshot of the changes made so we can come back to the checkpoint if we needed
```

- git status : shows the untracked, tracked files

- git add *file-name* - to add the file to staging are

- git add . or git add --All : add all the file to staging area which are untracked

- git commit -m "message to make a checkpoint" : t save all the files changes as a snapshot

- git log : show all the checkpoint / commit history
which has the message,commit id, date,Author(who made the commit)

- git log --one-line : show the commit id, message

```
we can create a remote repo in github, bitbucket and reference the git in our local machine to the rempte repo so that we can pull and push the codes

```

- git remote add *user-defined-name* *link-of-remote-repo* : it add the reference of remote repository and mostly the user-defined-name is origin

- git clone *link-of-remote-repo* - it will fetch the repo with entire file including ".git"  it is preferable to use first time for reference when we going to work on a existing project 

> Note : git cloned file will have the user-defined-name for the remote reference as origin by default

- git remote -v : it shows the reference for pull and push operation

> Note : we can have as many reference of remote for a single repository

- git pull origin *branch-name*  or git pull *remote-reference* *branch-name* : to pull the file from the remote repository 

- git pull origin *branch-name*  or git pull *remote-reference* *branch-name* : to push the file to the remote repository

```
As you noticed the command have branch name . The branches are very useful while working as a team to resolve conflict

Git always create a new branch when you make a first commit or when you pull from remote by default branch name is master

As i said earlier git track the file in calculting the difference from previous commits and always have a pointer at the top commit that is head (like a linked list) and each branch have its head pointer

so git enable us to create a branch and track the changes that is we create a another head pointer and keep commit and changes there and we can merge with the older head or branch in later stages

Branches are very useful when you are working as a team . In most software developement process there are three branches main (deployment), develop, feature (developer created branch)

we will pull the develop and create a branch from there or from that head and commit all our changes and push our new branch to remote repo on the remote repo it shows the difference between develop and our branch so now we make Pull request to merge our changes to develop


```

- git branch : to list all the branches and active branch (which branch we are in currently by reen color indication of font)

- git checkout -b *branch-name* : to create a new branch and switch

- git checkout *branch-name* : to switch an existing branch

- git switch -c *branch-name* : to create a new branch and switch

- git switch *branch-name* : to switch an existing branch

> Note both do the same work but checkout is traditional command and switch is modern

- git branch -d *branch-name* : it delete the branch (soft delete ) .it is fully merged with our branch

- git branch -D "branch-name* : it delete the branch forcefully as the branch may have changes that are not fully merged with out branch

> Note: do delete a branch we need to be another branch other than that branch.

- git merge *branch-name* : we can merge the branch mentioned in the command to the current branch

```
There are two types of merging 
1. Fast forward: If the current branch has no extra commit then git will fast forward tha merge which means it will point make the header to move to the head of the branch we are merging.

Note > Fast forward are rare case in real world

2. No fast forward : if the current branch has some commit then git will perfectly merge the branch and 
create another commit as a merge commit.

 if we made changes in the same line in same file while merging it will make a merge conflict that the file which has merge conflicts will have
 >>>>> incoming branch name 
 incoming
 ======
out going
 <<<<< our branch

 we need to remove the character and decide which line to have in the file and commit the changes we made.
```

> When you have no permission / not part of the project to directly contribute to a repo in github we can fork the repo and push changes to the forked  repo and later we can make a pull request
( Fork : Copy of actual repo in your account )
mostly useful in open source contribution



```
Git rebase also used to merge two branches but what the differnce from merge? . in case of rebase we are placing on branch over other that is we are copying commit history from one branch to another branch if you notice the commit id which are hash changes during this process

there we have a linear commit history but when we merge it actually have commit to say when merge happened

it is better to use merge in case working in group so that we can track the changes clearly

```

- git rebase *branch-name* : copy the commit history from mentioned branch to our branch

```
Git interactive rebase help us to edit the commit history suppose we need to combine 4 commits as a single one we can rebase and squash ( merge the commit as single it is one of the option in interactive rebase)
```

- git rebase -i *Head~4* : it will open a window where we specigy which name to preserve and which commits to merge ,drop etc.,

> Note : (pointer) denote the top  commit, 
"~" means reduce/points, "4" denotes : number of commit;
```
Squash used to melt/merge the commit as a single commit 

make the commit which you want to merge as squash
and to which commit you want to merge make it as pick
```

- git cherry-pick *commit-id* : use to coopy a single commit from other branch to our branch with out merging entire branch

```
Reverting and Resetting commit used to remove commit or commit changes from history
```

- git revert *commit-id* - will create a new commit having opposite of that commit if that commit have somethiing added it will delete it.It is useful as it hold undo changes in the history

- git reset --soft *HEAD~1* :  it will go back to the previous commit but still have the changes file there (  using git status we can see that)

- git reset --hard *HEAD~1* :  it will go back to the previous commit but delete the changed files


```
Sometimes we need made some changes in our branch A but there is a urgent work on branch B we try to switch the branch but git says we need to commit the changes to move to the next branch her branch B
so we commit the changes in A and move to B.After completing the work we revert the commit in A and start working on it but there is a wasily way to do it using stash 
```

- git stash *file-name* : help us have the changes stored temporarily in the machine so that we can move to some branches and work and its a LIFO data structure with a id for each stash

- git stash pop or git stash pop *stash-id* - remove the last push file changes from stash and remove from stash or we can pop a particular stash by mentioning its id

- git stash drop *stash_id* : delete that stash and changes 

- git stash apply *stash_id* - get the changes from the stash but not remove from the stash

- git stash list : list of all stash 

- git stash show *stash-id* : it show the changes and the file details

- git diff *commit-1* *commit-1* - it shows the difference between two commits

- git diff *file-1* *file-1* - it shows the difference between two file


- git diff *branch-1* *branch-1* - it shows the difference between two branch

- git diff -staged : it show the difference between staging area and last commit

- git reflog : it store the entire action that it take place in the repository with head pointer position so that if we did any thing by mistake still we can get back to the correct state at the time it will gitv you entire history

> Note : Git reflog is life saver in git.





