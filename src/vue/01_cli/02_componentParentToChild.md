# Components Parent -> Child #
http://vuejs.org/guide/components.html#Props
* Parent.vue
```vue
<template>
    <button @click="changeName">Change my name</button>
    <app-child :nameChild="name"></app-child>
</template>
<script>
    import Child from './Child.vue'

    export default {
        data() {
            return {
                name: "Max"
            }       
        },      
        components: {
            appChild: Child
        },
        methods: {
            changeName() {
                this.name = "Ana";
            }
        }      
    }  
</scirpt>
```
* Child.vue - "props" 
```vue
<template>
    <p> User name : {{ nameChild }} </p>
    <p> User name : {{ switchName() }} </p>
</template>
<script>
    export default {
        props: ['nameChild'],
        methods: {
            switchName(){
                return this.name.split("").reverse().join("");
            }   
        }       
    }  
</scirpt>
```

* Child.vue - validate "props" 
```vue
<template>
    <p> User name : {{ name }} </p>
    <p> User name : {{ nameMultiType }} </p>
</template>
<script>
    export default {
        props: {
            name: String,
            nameMultiType: [String, Array],
            nameRequired: {
                type: String, 
                required: true
            },
            nameWithDefault: {
                type: String, 
                default: "Max"
            }  
        }
    }  
</scirpt>
```