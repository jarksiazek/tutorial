# Configuration #
### Saving data in "etc/gitconfig" ###
```bash
git config --global user.name = {yourname}
git config --global user.email = {youremail}
//global config list 
git config --list
```
### Help ###
```bash
git help <verb>
git <verb>  --help
man git-<verb>
```

### Initial local repo ###
```bash
# in project folder
git init
git add .
git commit -m "inital commit"
```
### Git Status  ###
```bash
# basic
git status
# git status short
git status -s 
```

### Git Ignore   ###
```bash
# files ending on ".o" or ".a"
*.[oa]
# files ending on ".a"
*.a
# keep file with "lib.a"ending on ".a"
*.a
# ignore all files in the build/ directory build/
build/
```

### Removing files ###
```bash
# removing file from tracking
# add file to .gitignore
git rm --cached <fileName>
```

### File name changing ###
```bash
git mv originalFileName newFileName
```

### History revision ###
```bash
git log
git log -p #Different between commits
git log -2 #Showing only 2 last commits
git log --stat #Adding statitiscs
git log --pretty=format: "%h - %an, %ar : %s  #Better view of logs options: oneline,short, full, fuller, format
git log --pretty=format:"%h %s" --graph #Format plus graph
git log --since=2.weeks
git log -Sfunction_name #Only show commits adding or removing code matching the string
```

### Removing Commits ###
```bash
git commit --amend

```





