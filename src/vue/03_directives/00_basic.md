# DIRECTIVES #
### Links ###

### built-in ###
* v-on
* v-mode
* v-text
* v-html  

### custom directive ###
Directive's hooks: 
* <strong>bind(el, binding, vnode)</strong> - once directive is attached  
* inserted(el, binding, vnode) - inserted in parent node
* <strong>update(el, binding, vnode, oldVnode)</strong> - once component is updated (without children)
* componentUpdated(el, binding, vnode, oldVnode) - once component is updated (with children)
* unbind(el, binding, vnode) - once directive is removed

Two options: 
* global - main.js
```javascript
//can be used by v-newGlobalDirectiveName
Vue.directives('newGlobalDirectiveName', { 
    bind(el, binding, vnode){
        el.style.backgroundColor = 'green';
    }
})

//can be used by v-newGlobalDirectiveNamePassingValue
Vue.directives('newGlobalDirectiveNamePassingValue', { 
    bind(el, binding, vnode){
        el.style.backgroundColor = binding.value;
    }
})

//can be used by v-newGlobalDirectiveNameWithManyValues
Vue.directives('newGlobalDirectiveNameWithManyValues', { 
    bind(el, binding, vnode){
        el.style.backgroundColor = binding.value.firstColor;
    }
})

//can be used by v-newGlobalDirectiveNamePassingValueAndStyle
Vue.directives('newGlobalDirectiveNamePassingValueAndStyle', { 
    bind(el, binding, vnode){
        if (binding.arg == 'backgroundColor') {
            el.style.backgroundColor = binding.value;
        }       
    }
})
//can be used by v-newGlobalDirectiveNamePassingValueAndStyleWithDelay
Vue.directives('newGlobalDirectiveNamePassingValueAndStyleWithDelay', { 
    bind(el, binding, vnode){
        if (binding.arg == 'backgroundColor' && binding.modifiers['delayed']) {
            setTimeout(() => el.style.backgroundColor = binding.value, 5);
        }       
    }
})
```
```vue
<template>
    <div>
        <p v-newGlobalDirectiveName>Color this</p>
        <p v-newGlobalDirectiveNamePassingValue="'red'">Color this</p>
        <p v-newGlobalDirectiveNameWithManyValues="{firstColor:'red', secondColor: 'green'}">Color this</p>
        <p v-newGlobalDirectiveNamePassingValueAndStyle:background="'red'">Color this</p>
        <p v-newGlobalDirectiveNamePassingValueAndStyleWithDelay:background.delayed="'red'">Color this</p>
    </div>
</template>
<script>
export default {

}
</script>
```
* locally - Any.vue
```vue
<template>
    <div>
        <p v-newLocalDirectiveName>Color this</p>
    </div>
</template>
<script>
export default {
    directives: {
        'newLocalDirectiveName' : {
            bind(el, binding) {
            
            }       
        }
    }   
}
</script>
```
```