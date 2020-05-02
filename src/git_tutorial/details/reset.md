# RESET #
### Move HEAD ###
- reset to move a HEAD
    * git reset --soft HEAD~ //move HEAD to previous commit
    
- updating the index (-mixed)
    * git reset --mixed HEAD~ //default option, undid last commit, unstaged everything

- updating the working directory (--hard)
    * git reset --hard HEAD~
    * git reset --hard [SHA-1] 
