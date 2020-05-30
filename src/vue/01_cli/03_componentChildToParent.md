# Components Parent -> Child #
Emitting custom event - $emit(nameOfEvent, data)
* Child.vue
```vue
<template>
    <button @click="changeName">Change my name</button>
</template>
<script>
    export default {
        props: {
            nameFromChild: {
                type: String
            }
        },
        methods: {
            changeName() {
                this.nameFromChild = "Ana";
                this.$emit('eventName', this.nameFromChild);
            }
        }      
    }  
</scirpt>
```
* Parent.vue - "@eventName" - name from this.$emit('eventName', this.nameFromChild);
```vue
<template>
    <p>{{name}}</p>
    <app-child :name="name" @eventName="name = $event"></app-child>
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