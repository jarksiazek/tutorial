# Merging #
### FEATURE -> MASTER ###
```bash
git checkout master #switch to master
git pull #pull remote changes
git merge feature #merge fast-forward feature to master 
git push master #send changes to repo
git branch -d feature #removing branch feature
```
### MASTER -> FEATURE ###
```bash
git checkout feature #switch to feature
git merge master #updating feature
```