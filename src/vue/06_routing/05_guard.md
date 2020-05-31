# VUE ROUTING GUARD #
### Links ###
https://router.vuejs.org/

### beforeEnter - global for all ###
* main.js
```javascript
const router = new VueRouter({
    routes, 
    mode: 'history'  
})

router.beforeEach(
    (to, from, next) => {
        console.log('global beforeEach')
        next(); //possible options false, "/", {}
    }
);
```

### beforeEnter - global for specific path ###
* route.js
```javascript
export const routes = [
    {path: '', components: {
            default: Home,
            'header-top': Header
        }
    },
    { path: '/redirect-me', redirect: '/user', 
            beforeEach: (to, from, next) => {
                console.log('path beforeEach')
                next();
            }}
]
```

### beforeEnter - specific component ###
* App.vue
```vue
<script>
export default {
    beforeRouteEnter(to, from, next) {
            console.log('component beforeEach') // **no access to data!!** 
            next();
    }
}
</script>
```

### beforeEnter - specific component with access to component data ###
* App.vue
```vue
<script>
export default {
    data() {
        return  {
            userName: ''
        }   
    },    
    beforeRouteEnter(to, from, next) {
            next(vm => console.log(vm.userName));// **access to component data!!** 
    }
}
</script>
```

### beforeLeave - specific component ###
* App.vue
```vue
<script>
export default {
    data() {
        return  {
            userName: ''
        }   
    },    
    beforeRouteLeave(to, from, next) {
            if(this.username === "") {
                next(vm => console.log(vm.userName));// **full access to  component data!!** 
            }   
    }
}
</script>
```