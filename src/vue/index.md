# VUE #
### Links ###
[https://vuejs.org/v2/guide/](https://vuejs.org/v2/guide/)


### elements ###
data  
methods  

### directives ###
* v-bind
    ```html
    <a v-bind:href="link">Link</a>
    ``` 
* v-once - use only initial value
    ```html
    < v-bind:once>Link</>
    ```
* v-html - adding html template 
    ```html
    <p v-html="htmlWithLink"</p>
    ``` 
* v-on - receiving some events 
    * example 1 - event
        ```html
        <button v-on:click="methodAfterClick"</button>
        ``` 
      ```javascript
      new Vue({
          methods: {
              methodAfterClick(event) {
                  console.log(event);
              }       
          }
      })
      ``` 
  * example 2 - my argument
      ```html
      <button v-on:click="methodAfterClick(2)"</button>
      ``` 
        ```javascript
        new Vue({
            methods: {
                methodAfterClick(myArg) {
                    console.log(myArg);
                }       
            }
        })
        ```
  * example 3 - my argument and event  
      ```html
      <button v-on:click="methodAfterClick(2, $event)"</button>
      ``` 
      ```javascript
      new Vue({
          methods: {
              methodAfterClick(myArg, event) {
                  console.log(myArg);
                  console.log(event);
              }       
          }
      })
      ```
  * example 4 - keyup only for enter key
      ```html
      <input type="text" v-on:keyup.enter="alertMe()"</button>
      ``` 
      ```javascript
      new Vue({
          methods: {
              alertMe(event) {
                  alert(event);
              }       
          }
      })
      ``` 
  * example 5 - adding function directly to html keyup only for enter key
    ```html
    <button v-on:click="increaseBy(2)"</button>
    <button @click="counter++"</button>
    ```  
### computed ###
Similar to data, but for this we can add function
```javascript
new Vue({
  data: {
      value: 0
      },
  computed: {
    result () {
        return this.value == 37 ? 'done' : 'not done yet';
    }             
  }
})
``` 
### watch ###  
Execute code upon data changes/ react to changes
```javascript
new Vue({
  data: {
      counter: 0
      },
  watch: {
    counter (value) {
        var vm = this;
        setTimeout(function() {
            vm.counter = 0; //reset counter every 2 seconds
        }, 2000)  
    }             
  }
})
``` 