# Life Cycle #
### creation ###
new Vue()  
* beforeCreate()  
    *  Initialize Data and Events
* created()
    * Instance created
* beforeMount()
    * compile template or el's templates  
* mounted to DOM
    * replace el with compiled template
    
### updating ###   
* beforeUpdate()
    * before data change 
* updated()
    * before data change 
 
### destroying ###   
* beforeDestroy()
* destroyed()