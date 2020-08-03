# VUE STATE MANAGER #   

### 2 way binding - 1st approach ### 
* store.js
```javascript
import Vue from 'vue'; 
import Vuex from 'vuex';

Vue.use(Vuex);

export const store = new Vuex.Store({
    state: {
        value: 0                                      
    },
    getters: {
        getValue: state => {
            return state.value;              
        }     
    }, 
    mutations: {
        updateValue: (state,payload)  => { state.value = payload }
    },
    actions: {
        updateValue: ({commit}, payload) => {
            commit('updateValue', payload);
        } 
    }                          
})
```

* App.vue
```vue
<template>
    <input type="text" :value="value" @input="updateValue"/>
</template>
<script>
export default {
    computed: {
        value() {
            return this.$store.getters.value;
        }   
    },
    methods: {
        updateValue(event){
            this.$store.dispatch('updateValue', event.target.value)                 
        }             
    }                               
}
</script>
```

### 2 way binding - 2nd approach  ### 
* store.js
```javascript
import Vue from 'vue'; 
import Vuex from 'vuex';

Vue.use(Vuex);

export const store = new Vuex.Store({
    state: {
        value: 0                                      
    },
    getters: {
        getValue: state => {
            return state.value;              
        }     
    }, 
    mutations: {
        updateValue: (state,payload)  => { state.value = payload }
    },
    actions: {
        updateValue: ({commit}, payload) => {
            commit('updateValue', payload);
        } 
    }                          
})
```

* App.vue
```vue
<template>
    <input type="text" v-model="value"/>
</template>
<script>
export default {
    computed: {
        value: {
            get() {
                return this.$store.getters.value;
            },
            set(value) {
                this.$store.dispatch('updateValue', value)
            }              
        }   
    }                               
}
</script>
```
