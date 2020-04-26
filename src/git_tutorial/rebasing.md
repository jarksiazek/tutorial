# Rebasing #
### MASTER / SERVER / CLIENT ###
Git baseline
![](.rebasing_images/5f4f8e16.png)

1. CLIENT -> main line 
    ```bash
    $ git rebase --onto master server client
    $ git merge master #updating feature
    ```
    CLIENT was added to main line  
    ![](.rebasing_images/7a7005c5.png)\

2. CLIENT -> MASTER
    ```bash
    $ git checkout master
    $ git merge client
    ```  
    CLIENT was merged to MASTER
    ![](.rebasing_images/946e6a03.png)

3. SERVER -> main line 
    ```bash
    $ git rebase master server #git rebase [basebranch] [topicbranch]
    $ git merge client
    ```   
    SERVER was added to main line  
    ![](.rebasing_images/eee5a794.png)

4. SERVER -> MASTER
    ```bash
    $ git checkout master
    $ git merge server
    ```  