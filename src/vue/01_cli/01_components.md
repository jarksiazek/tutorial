# Components #
http://vuejs.org/guide/components.html  
https://vuejs.org/v2/guide/components-registration.html
### Register Globally ###
```javascript
Vue.component('my-cmp', {})
``` 
### Register Component in App.vue ###
```vue
// Home.vue
<template>
    <div></div>
</template>
<script>
    export default {
    }  
</scirpt>

// App.vue
import Home from ./Home.vue
Vue.component ('app-server-status', Home);

``` 

### Register Component locally in Home.vue ###
* Child.vue
```vue
<template>
    <div></div>
</template>
<script>
    export default {
    }  
</scirpt>
```

* Home.vue
```vue
<template>
    <app-child-component></app-child-component>
</template>

<script>
    import Child from './Child.vue';

    export default {
        data() {
        },
        components: {
            'app-child-component': Child
        }   
    }  
</scirpt>
``` 