2026-03-21 23:51

Status: #In-Progress 

Tag: [[Version-control]]

# Git Commands

**INSTALLATION**: [Git download](https://git-scm.com/install/windows)

Below will have frequently needed commands their is more use **git --help** to learn more about it.

### Global commands:
```
git config --global user.name “[firstname lastname]”
//set a name that will seen in commit history

git config --global user.email “[valid-email]”
//set an email that will seen in commit history

```

### Setup 
```
git init
// make the current dir a git repo

git clone url
//clone remote repo into local
```

### Working & Snapshot commands:
```
git status
// Show current branch and changes that are modified for commiting.

git add [file]
// add file for staging to commit

git reset [file]
// unstage the file

git diff 
// diff of what is changed but not staged 

git diff --staged 
// diff of what is staged but not yet committed 

git commit -m “[descriptive message]” 
//commit your staged content as a new commit snapshot
```


### BRANCH & MERGE 
```
git branch 
// list your branches. a * will appear next to the currently active branch

git merge [branch]
// merge the branch

git log
// show commit history of your current branch

git checkout -b [branch-name]
// create a new branch and switch to it (if the branch doesnt exist it will create a new local branch)

git switch [branch-name]
// switch to existing branch if branch doesnt exist

git branch -d [branch-name]
// safe delete (only delete the branch if the feature is merged)

git branch -D [branch-name]
// Force delete the branch.


```

**Note**: If a branch create it will be in local we need to publish it(push it to upstream).

### Main workflow command:
```
git fetch [alias]
// fetch all branches from git remote. normally alias-> origin, if forked alias -> upstream, we can also set alias.

git pull
// update the current branch

git push
// Push the commited changes in local to remote.
```

### Merge & Rebase
```
git rebase [branch-name]


git merge [branch-name]
```

### Cherry pick
```
git cherry-pick [commit-hash]
// Will keep the commit on top of current branch
```
## Reference
