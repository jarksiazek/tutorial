# EventBus #
Communication between siblings   
http://vuejs.org/guide/components.html#Custom-Events 
http://vuejs.org/guide/components.html#Non-Parent-Child-Communication   
Object to serve data between components
* main.js
```javascript
export const eventBus = new Vue();

new Vue({
    el:'app',
    render: h=>h(App)
})
```

* Child1.vue - "props" 
```vue
<template>
    <p> User name : {{ userAgeChild1 }} </p>
</template>
<script>
    import { eventBus } from ./main.js;

    export default {
        props: ['userAgeChild1'],
        methods: {
            editAge(){
                // this.$emit('ageWasEdited', this.userAge);
                eventBus.$emit('ageWasEdited', this.userAgeChild1);
            }   
        }       
    }  
</scirpt>
```

* Child1.vue - "props" 
```vue
<template>

</template>
<script>
    import { eventBus } from ./main.js;

    export default {
        props: ['userAgeChild2'],
        created() {
            eventBus.$on ('ageWasEdited', (data) => {
                   this.userAgeChild2 = data;
            })
        }   
    }  
</scirpt>
```