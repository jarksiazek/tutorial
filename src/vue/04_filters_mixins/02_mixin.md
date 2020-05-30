# MIXIN #
### Links ###
- shared part of code

* fruits.js
```javascript
export const fruits = {
    data() {
        return {
            fruits: ['Apple', 'Mango'],
            selectedFruit: ''
        }
    },
    computed: {
        filteredFruits() {
            return this.fruits.filter(
                (element)=> {return element.match(this.selectedFruit)} 
            )       
        }    
    }
};
```

```vue
<template>
    <div>
        <p>{{ toUpperCaseString | toUppercase | secondFilter }}</p>
    </div>
</template>
<script>
import {fruits} from './fruits'

export default {
    mixins: [fruits]
}
</script>
```

### global mixin ###

* main.js
```javascript
Vue.mixin({
    
});
```