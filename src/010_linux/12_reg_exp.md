# REG_EXP #

* ^sam = **sam**uel
* set$ = sun**set**
* c.t = **cut**, exe**cut**e
* let* = le, let, lett, lettttt 
* /.*/ = /user/man, user/share/man
* /0*/ = 12, 101, 1000 # match previous element 0 or more 
* /0+/ =  10, 1000 # match previous element one or more 
* /0{3,}/ =  000, 1000, 10000 # match 3 zeros and more
* /10{,3}/ =  1, 1.00, 10000 # match 0 zeros and max 3 zeros 
* /0{3}/ =  1000, 2000, 300000  # match 3 zeros
* disabled? =  disable, disabled #last letter is optional
* disable|enable =  enable, disable # 2 options 
* c[au]t =  cat, cut # "au" are options 


* grep with regular expression
  * grep -E "0+" == egrep "0+"