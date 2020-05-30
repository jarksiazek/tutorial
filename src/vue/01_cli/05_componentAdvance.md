# Components Advanced #
Slots
* Parent.vue 
```vue
<template>
    <app-child>
        <p>Param1</p>    
        <div>Div1</div>    
    </app-child>
</template>
<script>
    import Child1 from './Child1.vue'
    export default {
        components: {
            appChild: Child1
        }
    }
</scirpt>
```

* Child1.vue - "props" 
```vue
<template>
    <div>
        <slot></slot>
    </div>
</template>
<script>    
</scirpt>
```

Named slots
* Parent.vue 
```vue
<template>
    <app-child>
        <p slot="title">Param1</p>    
        <div slot="content">Div1</div>    
    </app-child>
</template>
<script>
    import Child1 from './Child1.vue'
    export default {
        components: {
            appChild: Child1
        }
    }
</scirpt>
```

* Child1.vue - "props" 
```vue
<template>
    <div>
        <slot name="title"></slot>
        <slot name="content"></slot>
    </div>
</template>
<script>    
</scirpt>
```

Default Content
* Parent.vue 
```vue
<template>
    <app-child>
        <div slot="content">Div1</div>    
    </app-child>
</template>
<script>
    import Child1 from './Child1.vue'
    export default {
        components: {
            appChild: Child1
        }
    }
</scirpt>
```

* Child1.vue - "props" 
```vue
<template>
    <div>
        <slot name="title">Default Content</slot>
        <slot name="content"></slot>
    </div>
</template>
<script>    
</scirpt>
```

Dynamic Component 

new hooks for keep alive components:  
    - deactivated()  
    - activated() 

* Parent.vue - "props" 
```vue
<template>
    <div>
        <button @click="seclectedComponent = 'appChild1'">Child1</button>
        <button @click="seclectedComponent = 'appChild2'">Child2</button>
        <button @click="seclectedComponent = 'appChild3'">Child3</button>
        <p>{{ selectedComponent }}</p>
        <component :is="selectedComponent"></component> <!--destroying-->
        <keep-alive>
            <component :is="selectedComponent"></component> <!-- not destroying-->
        </keep-alive>    
</div>
</template>
<script>
    import Child1 from './Child1.vue'
    import Child2 from './Child2.vue'
    import Child3 from './Child3.vue'

    export default {
        data() {
            return {
                selectedComponent: 'appChild1'
            }   
        },
        components: {
            appChild1: Child1, 
            appChild2: Child2, 
            appChild3: Child3, 
        }
    }
</scirpt>
```