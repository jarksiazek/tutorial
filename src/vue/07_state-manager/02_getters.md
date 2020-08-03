# VUE STATE MANAGER #   

### getters ### 
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
            this.$store.state.counter++;                         
        }             
    }                               
}
</script>
```

* Result.vue - "computed" reacts on store changes
```vue
<template><div> {{ counter }} </div></template>
<script>
export default {
    computed: {
        counter(){
            this.$store.getters.doubleCounter;                         
        }             
    }                               
}
</script>
```

* Result2.vue - get data directly from store (spread operator could require additional preset stage-2)
```vue
<template><div> {{ doubleCounter }} </div></template>
<script>
import { mapGetters } from 'vuex';
export default {
    computed: {
        ...mapGetters ([
                'doubleCounter', 'anotherGetter'
            ]),
         ownComputedProperty: {
        }                
    }        
}
</script>
```
