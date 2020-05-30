# VUE ROUTING PARAMS #
### Links ###
https://router.vuejs.org/

### sending uri parameter to link ###
1. Approach 1
    * User.vue - remember to repeat "router-view" in parent component
    ```vue
    <template>
        <router-link tag="button"  
            :to="'/user/' + $router.params.id + '/edit'"
            class="btn btn-primary">Edit user</router-link>
    </template>
    ```  
2. Approach 2
    * route.js
    ```javascript
    import User from './components/User.vue'
    import Home from './Home.vue'
    
    export const routes = [
        {path: '', component: Home },
        {path: '/user', component: User, children: [
            { path: '', component: UserStart },
            { path: ':id', component: UserDetail },
            { path: ':/edit', component: UserEdit, name: 'userEdit' } // use name instead of path
        ]}
    ]
    ```
    * User.vue - remember to repeat "router-view" in parent component
    ```vue
    <template>
        <router-link tag="button"  
            :to="{ name: 'userEdit', params: { id: $routes.parems.id } }"
            class="btn btn-primary">Edit user</router-link>
    </template>
    ```
### query parameters localhost:8080?locale=en&q=100 ###
* User.vue 
```vue
<template>
    <router-link tag="button"  
        :to="{ name: 'userEdit', query: { locale: 'en', q: 100 } }"
        class="btn btn-primary">Edit user</router-link>
</template>
```
* UserEdit.vue 
```vue
<template>
    <div>
        <p>Locale: {{ $route.query.locale }}</p>
        <p>q: {{ $route.query.q }}</p>
    </div>
</template>
```