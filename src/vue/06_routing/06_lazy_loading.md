# VUE LAZY LOADING GUARD #
### Links ###
https://router.vuejs.org/

### lazy loading setup for webpack ###
* router.js
```javascript
import Home from './components/Home.vue'

const User = resolve => {
    require.ensure(['./components/User.vue'], () => {
        resolve(require('./components/User.vue'));
    });
}

export const routes = [
    {path: '', name: Home},
    {path: '/users', name: User}    
] 
```

### lazy loading setup for webpack and grouping ###
* router.js
```javascript
import Home from './components/Home.vue'

const User = resolve => {
    require.ensure(['./components/User.vue'], () => {
        resolve(require('./components/User.vue'));
    }, 'user');

const UserDetail = resolve => {
    require.ensure(['./components/UserDetail.vue'], () => {
        resolve(require('./components/UserDetail.vue'));
    }, 'user');
}

export const routes = [
    {path: '', name: Home},
    {path: '/users', name: User}    
] 
```

