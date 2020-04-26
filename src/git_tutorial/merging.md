# Merging #
### FEATURE -> MASTER ###
```bash
#Before it MASTER -> FEATURE / MASTER -> FEATURE - REBASING
$ git checkout master #switch to master
$ git pull #pull remote changes
$ git merge feature #merge fast-forward feature to master 
$ git push master #send changes to repo
$ git branch -d feature #removing branch feature
```
### MASTER -> FEATURE ###
```bash
$ git checkout feature #switch to feature
$ git merge master #updating feature
```
### MASTER -> FEATURE - REBASING ###
```bash
$ git checkout feature #switch to feature
$ git rebase master
First, rewinding head to replay your work on top of it... 
Applying: added staged command
```