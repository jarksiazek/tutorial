# VUE RESOURCE #
### Links ###
https://router.vuejs.org/  
https://github.com/vuejs/vue-router
### npm ###
```bash
npm install --save vue-router
```

### setup ### 
* main.js
```javascript
import VueRouter from 'vue-router'
import { routes } from './route'

Vue.use(VueRouter)

const router = new VueRouter({
    routes, //routes : routes
    mode: 'history' //to remove # in url
})

new Vue({
    el: '#app', 
    router, //router: router
    render: h => h(App) 
})
``` 

* route.js
```javascript
import User from './components/User.vue'
import Home from './Home.vue'

export const routes = [
    {path: '/user', component: User },
    {path: '', component: Home }
]
```

* App.vue
```vue
<template>
    <div>
        <router-view></router-view>
    </div>
</template>
```

### router link ###
* Header.vue 
```vue
<template>
    <div>
        <ul>
            <li><router-link to="/">Home</router-link></li>
            <li><router-link to="/User">User</router-link></li>
        </ul>
    </div>
</template>
```

* Header.vue - 2nd approach
```vue
<template>
    <div>
        <ul>
            <router-link to="/" tag="li" active-class="active" exact><a>Home</a></router-link>
            <router-link to="/User" tag="li" active-class="active"><a>User</a></router-link>
        </ul>
    </div>
</template>
```

### redirect by code ###
* User.vue 
```vue
<script>
export default {
    methods: {
        navigateToHome(){
            this.$router.push('/home');
        }
    }
}
</script>
```

### redirect by code with parameters - getting url parameters ###
https://github.com/vuejs/vue-router/tree/dev/examples/route-props
* User.vue 
```vue
<script>
export default {
    data() {
        return {
            usedId: this.$routes.params.id 
        }
    },
    watch: {
        '$route' (to, from) {
            this.id = to.params.id;
        } 
    },   
    methods: {
        navigateToHome(){
            this.$router.push('/home');
        }
    }
}
</script>
```


### children - nested routes  ###
* route.js
```javascript
import User from './components/User.vue'
import Home from './Home.vue'

export const routes = [
    {path: '', component: Home },
    {path: '/user', component: User, children: [
        { path: '', component: UserStart },
        { path: ':id', component: UserDetail },
        { path: ':/edit', component: UserEdit }
    ]}
]
```
* User.vue - remember to repeat "router-view" in parent component
```vue
<template>
    <router-view></router-view>
</template>
```

### adding multi components ###
* route.js
```javascript
export const routes = [
    {path: '', components: {
            default: Home,
            'header-top': Header
        }
    },
    {path: '/user', component: User, children: [
        { path: '', component: UserStart },
        { path: ':id', component: UserDetail },
        { path: ':/edit', component: UserEdit }
    ]}
]
```
* App.vue 
```vue
<template>
    <div>
        <router-view name="header-top"></router-view>
        <router-view></router-view>
    </div>
</template>
```

### redirect on routes ###
* route.js
```javascript
export const routes = [
    {path: '', components: {
            default: Home,
            'header-top': Header
        }
    },
    {path: '/user', component: User, children: [
        { path: '', component: UserStart },
        { path: ':id', component: UserDetail },
        { path: ':/edit', component: UserEdit }
    ]},
    { path: '/redirect-me', redirect: '/user' }
]
```

### redirect catch all not specified - default page ###
* route.js
```javascript
export const routes = [
    {path: '', components: {
            default: Home,
            'header-top': Header
        }
    },
    {path: '/user', component: User, children: [
        { path: '', component: UserStart },
        { path: ':id', component: UserDetail },
        { path: ':/edit', component: UserEdit }
    ]},
    { path: '*', redirect: '/' }
]
```
