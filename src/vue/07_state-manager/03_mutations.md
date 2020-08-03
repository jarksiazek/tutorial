# VUE STATE MANAGER #   

### mutations - only sync ### 
* store.js
```javascript
import Vue from 'vue'; 
import Vuex from 'vuex';

Vue.use(Vuex);

export const store = new Vuex.Store({
    state: {
        counter: 0                                      
    },
    getters: {
        doubleCounter: state => {
            return state.conter * 2;              
        }     
    }, 
    mutations: {
        increment: state => state.counter++
    }                          
})
```

* App.vue
```vue
<template></template>
<script>
export default {
    methods: {
        increment(){
            this.$store.commit('increment')                 
        }             
    }                               
}
</script>
```

* App.vue - map mutations
```vue
<template></template>
<script>
import { mapMutations } from 'vuex';
 
export default {
    methods: {
        ...mapMutations([
            'increment'
        ])
    }                        
}
</script>
```
