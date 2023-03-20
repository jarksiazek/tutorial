### Remove pushed changes

```bash
git log --oneline
git revert <commit-sha> #commit for reverting 
git push #push new commit 
```

### Remove changes from file

```bash
$ git restore filename.txt
```

### Restore deleted file

```
$ git restore deletedFileName.txt
```

### Restore part of changes from file

```
$ git restore -p deletedFileName.txt
```

### Change the last remote commit message

```
git commit --amend -m "<new message>
git push --force
```