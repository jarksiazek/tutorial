# VUE STATE MANAGER #   

### actions - async mutations ### 
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
    },
    actions: {
        increment: context => {
            context.commit('increment');
        },
        asyncIncrement: ({commit}) => {
            setTimeout(() => {commit('increment');}, 5000)            
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
            this.$store.dispatch('increment')                 
        }             
    }                               
}
</script>
```

* App.vue - map actions
```vue
<template></template>
<script>
import { mapActions } from 'vuex';
 
export default {
    methods: {
        ...mapActions([
            'increment', 'asyncIncrement'
        ])
    }                        
}
</script>
```

* App.vue - map actions with arguments

```javascript
export const store = new Vuex.Store({
    state: {
        counter: 0                                      
    },
    mutations: {
        incrementBy: ( state, payload) => {
            context.state.counter += payload;
        }
    },        
    actions: {
        incrementBy: ( {commit}, payload) => {
            commit('increment', payload);
        },
        asyncIncrementBy: ( {commit}, payload) => {
            setTimeout( () =>{
                commit('increment', payload.by);
            }, payload.delay)
        }
    }                          
})
```

```vue
<template>
    <div>
        <button @click="incrementBy(100)"></button>
        <button @click="asyncIncrement({ by:100, delay:5000})"></button>
    </div>
</template>
<script>
import { mapActions } from 'vuex';
 
export default {
    methods: {
        ...mapActions([
            'incrementBy', 
            'asyncIncrement'
        ])
    }                        
}
</script>
```
