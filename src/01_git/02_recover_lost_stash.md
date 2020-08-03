# Lost stash #
http://inlehmansterms.net/2015/09/19/recover-a-dropped-git-stash/
### gui to see all recent lost changes ###
```bash
gitk --all $(git fsck --no-reflogs | awk '/dangling commit/ {print $3}')
```

### apply stash ###
```bash
git stash apply 121212121
```