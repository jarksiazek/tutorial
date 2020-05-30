# VUE ROUTING ANCHOR #
### Links ###
https://router.vuejs.org/

### Route to specif id localhost:8080/#data ###

* main.js
```javascript
const router = new VueRouter({
    routes, 
    mode: 'history',
    scrollBehavior(to, from, savedPosition) {
        // return { x:0, y:0 }; //scroll to 0,0
        if (to.hash) {
            return { selector: to.hash }; //scroll to hash selector
        }   
    }   
})
```

* User.vue 
```vue
<template>
    <div>
        <p id="data"></p>     
    </div>
</template>
```
* App.vue 
```vue
<template>
    <div>
        <router-link
            tag="button"
            :to="link"
            class="btn btn-primary">Edit user</router-link>   
    </div>
</template>

<script>
    export default {
        data() {
            return  {
                link: { 
                    name: 'user', 
                    params: { id: this.$router.params.id },
                    query: { locale: 'en' },
                    hash: '#data'
                }
            }       
        }   
    }
</script>
```