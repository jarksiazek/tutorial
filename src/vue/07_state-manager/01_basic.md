# VUE STATE MANAGER #
### Links ###
Vuex Github Page: https://github.com/vuejs/vuex  
Vuex Documenation: https://vuex.vuejs.org/en/
### Flow ###

fetching = state -> getters -> component  
updating = component (dispatch - async)-> actions (commit)-> mutations (sync)-> state 

### npm ###
```bash
npm install vuex --save
```
### setup ### 
* store.js
```javascript
import Vue from 'vue'; 
import Vuex from 'vuex';

Vue.use(Vuex);

export const store = new Vuex.Store({
    state: {
        counter: 0                                      
    }                
})
```

* main.js
```javascript
import { store } from '/store/store.js'

new Vue({
    el: '#app', 
    store,     
    render: h => h(App) 
})
```

* App.vue
```vue
<template></template>
<script>
export default {
    methods: {
        increment(){
            this.$store.state.counter++;                         
        }             
    }                               
}
</script>
```
