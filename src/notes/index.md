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

### Removing Commits --Amend ###
```bash
git commit --amend #Correction of last commit 
git reset HEAD <filename> #To unstage  
```

### Remote Repository ###
Basic info about remote repo
```bash
git remote #Name of servers with repo
git remote -v #Name of servers with repo plus url info
git remote add shortNam http://github.. # git remote add [skrót] [url]:
```
Fetching from remote repo
```bash
git fetch [remote-name]
git pull #fetch + merge
git push origin master #git push [name-remote-repo] [name-branch]
git remote show origin #more info about remote repo
```
Renaming remote repo
```bash
git remote rename #changing remote shot name
```
### Tagging ###
Tag - important versions of project\
Types: 
* soft - pointing to the particular part of code
* description - full object in database Git

Getting tag info
```bash
git tag #showig all project versions
git tag -l 'v1.8.5' #showig all project versions with tag v1.8.5
```
Description tag
```bash
git tag -a v1.4 -m "my version 1.4" #creating descriptive tag 
git show v1.4 #getting info about tagged version
git tag -a v1.2 9fceb02 #adding tag to historic revision
git checkout -b version2 v2.0.0  #Switched to a new branch 'version2' 
```
Soft tag
```bash
git tag v1.4-lw #creating soft tag 
git show v1.4-lw #getting info about tagged version
```
### Aliasing ###
```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.unstage 'reset HEAD --' #Adding 2 'reset HEAD --' to command unstage
git config --global alias.visual "!gitk" #"!" adding alias to external program
```

### HEAD ###
HEAD - place where you are in git tree
```bash
git log --decorate #show where is HEAD
git log --oneline --decorate --graph --all #log graph view
```

### BRANCH MANAGEMENT ###
```bash
$ git branch #current branches,  "*" - HEAD
iss53
* master
testing
```
```bash
$ git branch -v #last commmit for each branch
iss53   93b412c fix javascript issue 
* master  7a98805 Merge branch 'iss53'
testing 782fd34 add scott to the author list in the readmes
```
```bash
$ git branch --merge #list of branches already merged into the branch where you are on / list branches to delete
iss53
* master
```
```bash
$ git branch --no-merge #list of branches not merged yet into the branch where you are on /git branch -d testing -> fail
testing
```
### BRANCHING WORKFLOWS###