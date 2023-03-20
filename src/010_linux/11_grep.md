# GREP #

* grep searching for "train" in all *.txt
    ```bash
    grep train *.txt
    ``` 

* show names of files (-l) where the phase "java" were occurred
  ```bash
  grep -lr "java" /var/log
  ```

* (-i) ignore case sensitivity 
  ```bash
  grep -i "java" /var/log
    ```  

* (-w) searching for work
  ```bash
  grep -w "java" /var/log
    ```  