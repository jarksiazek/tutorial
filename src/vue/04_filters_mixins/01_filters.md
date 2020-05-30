# FILTERS #
### Links ###
- changes only view of output, not data 
- example: string input to uppercase letters
- no built-in filters 
- to more complex calculation use "computed" 
* global filter
```javascript
//newGlobalFilter
Vue.filter('newGlobalFilter', 
    (value) => value.toUpperCase()
)
```

* local filter
```vue
<template>
    <div>
        <p>{{ toUpperCaseString | toUppercase | secondFilter }}</p>
    </div>
</template>
<script>
export default {
    data() {
        return {
            toUpperCaseString: 'Hello World'
        }   
    }, 
    filters: {
        toUppercase(value) { //'to-uppercase'()
            return value.toUpperCase();     
        }   
    }
}
</script>
```