# VUE ROUTING GUARD #
### Links ###
https://router.vuejs.org/

### beforeEnter ###
* main.js
```javascript
const router = new VueRouter({
    routes, 
    mode: 'history'  
})

router.beforeEach(
    (to, from, next) => {
        
    }
);
```