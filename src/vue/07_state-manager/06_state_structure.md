# VUE STATE MANAGER #   

### original structure ### 
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

### new structure store and value(state, getters, mutations, actions) ### 
* store.js
```javascript
import Vue from 'vue';
import Vuex from 'vuex';
import value from './value'

Vue.use(Vuex);

export const store = new Vuex.Store({
    modules: {
        value
    }            
})
```

* value.js
```javascript
const state = {
    value: 0                                      
}

const getters = {
    getValue: state => {
        return state.value;              
    }    
}

const mutations = {
        updateValue: (state,payload)  => { state.value = payload }
}

const actions = {
        updateValue: ({commit}, payload) => {
            commit('updateValue', payload);
        } 
    } 

export default {
    state,
    getters,
    mutations,
    actions,
}
```

### new structure store and separate actions ### 
* store.js
```javascript
import Vue from 'vue';
import Vuex from 'vuex';
import value from './value'

Vue.use(Vuex);

export const store = new Vuex.Store({
    modules: {
        value
    }            
})
```

* value.js
```javascript
import * as actions from './action'

const state = {
    value: 0                                      
}

const getters = {
    getValue: state => {
        return state.value;              
    }    
}

const mutations = {
    updateValue: (state,payload)  => { state.value = payload }
}

export default {
    state,
    getters,
    mutations,
    actions
}
```

* action.js
```javascript
export const updateValue = ({commit}, payload) => {
            commit('updateValue', payload);
    } 

export const updateValue2 = ({commit}, payload) => {
            commit('updateValue', payload);
    } 
```

### store rules ###
* the names of methods should be unique in group 