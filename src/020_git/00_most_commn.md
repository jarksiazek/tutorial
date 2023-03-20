### GIT LOG

```bash
#one line logs
git log --oneline
git log --graph --all --decorate --oneline
```

### LIST OF MERGED BRANCHES

```bash
git branch -r --merged develop
git branch -r --no-merged develop
git branch -r --merged
```

### REBASE

```bash
#on feature branch to tip of master
git rebase master
```

### CHERRY_PICK

```bash
#one commit
git cherry-pick d4dgd

#one commit and edit commit message
git cherry-pick d4dgd -e

#2 commits or range
git cherry-pick d4dgd..6d62392
```

### CHERRY_PICK WITH CONFLICT

```bash
# 1) get commit
git cherry-pick d4dgd

# 2) resolve conflicts

# 3) add file 
git add fileNameWithConflict

# 4) continue cherry-picking 
git cherry-pick --continue

# 5) or abort 
git cherry-pick --abort
```

### DIFF PATCHES

* share changes via files
  
  ```bash
  #create diff file 
  git diff from-commit to-commit > output.diff
  ```

#apply diff file 
git apply output.diff

```
### DELETE BRANCHES LOCAL ###
```bash
# delete merged branch
git branch -d new_feature

# delete force branch merged or not merged
git branch -D new_feature
```

### DELETE BRANCHES REMOTE

```bash
#1st option - push empty local to remote
git push origin :new_feature

#2nd option
git push --delete origin new_feature
git push -d origin new_feature
```

### PRUNE STALE BRANCHES

* remote all stale remote-tracking branches
* stale branch - actual branch in the remote bas been deleted
  
  ```bash
  git remote prune origin
  git remote prune origin --dry-run
  ```

#prune and fetch
git fetch --prune 
```