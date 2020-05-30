# FORM #
### Input ###
```vue
<input
    type="text"
    id="email"
    class="form-control"
    v-model="email"
>
<script>
export default {
    data() {
        return {
            email: ''
        }
    }
}
</script>
``` 
### Input Group data ###
```vue
<div class="form-group">
    <input
        type="text"
        id="email"
        class="form-control"
        v-model="user.email"
    >
    <input
        type="password"
        id="password"
        class="form-control"
        v-model="user.password"
    >
</div>
<script>
export default {
    data() {
        return {
            user: {
                email: '',
                password: ''
            }           
        }
    }
}
</script>
``` 

### Input Modifiers ###
* v-model.lazy - changing binding type
* v-model.lazy.trim - trim white space
* v-model.lazy.number - forces inputting numbers
```vue
<div class="form-group">
    <input
        type="text"
        id="email"
        class="form-control"
        v-model.lazy="user.email"
    >
    <input
        type="password"
        id="password"
        class="form-control"
        v-model="user.password"
    >
</div>

<script>
export default {
    data() {
        return {
            user: {
                email: '',
                password: ''
            }           
        }
    }
}
</script>
```

### Text area ###
* white-space: pre - keeping line breaking
```vue
<div class="raw">
    <textarea
        id="message"
        rows="5"
        class="form-control"
        v-model = 'user.message'
    ></textarea>
</div>
<script>
export default {
    data() {
        return {
            user: {
                email: '',
                password: '',
                message: ''
            }           
        }
    }
}
</script>
``` 
### Checkbox ###
```vue
<div class="form-group">
    <label for="sendEmail">
        <input
            type="checkbox"
            id="sendEmail"
            value="SendEmail"
            v-model="user.sendEmail"
        > Send Email: 
    </label>
    <label for="sendSms">
        <input
            type="checkbox"
            id="sendSms"
            value="SendSms"
            v-model="user.sendSms"
        >
    </label>
</div>
<script>
export default {
    data() {
        return {
            user: {
                email: '',
                password: '',
                message: '', 
                sendEmail: false, 
                sendSms: false   
            }           
        }
    }
}
</script>
``` 
### Radio ###
```vue
<div class="form-group">
    <label for="male">
        <input
            type="radio"
            id="male"
            value="Male"
            v-model="gender"
        > Male
    </label>
    <label for="female">
        <input
            type="radio"
            id="female"
            value="Female"
            v-model="gender"
        > Female
    </label>
</div>
<script>
export default {
    data() {
        return {
            user: {
                gender: 'Male'  
            }           
        }
    }
}
<script>
``` 

### Dropdowns select/option  ###
```vue
<div class="form-group">
    <label for="selection">
        <select
            id="selection"
            class="form-control"
            v-model="selectedOption"
        >
            <option 
                v-for="option in options" 
                :selected="option == 'Option1'">
                {{option}}
            </option>
        </select>
    </label>
</div>
<script>
export default {
    data() {
        return {
            options: ['option1', 'option2', 'option3'],
            selectedOption: ''   
        }
    }
}
<script>
``` 

### Submitting form ###
* @click.prevent - the submit event will no longer reload the page
```vue
<form>
    <div class="form-group">
        <button @click="submit">Submit</button>
    </div>
</form>
<script>
export default {
    data() {
        return {
            user: {
                name: '',
                password: ''
            }
        }
    }, 
    methods: {
        submit() {
            
        }   
    }
}
<script>
``` 

### Input component with @input  ###
```vue
<div class="form-group">
    <input
        type="text"
        id="email"
        class="form-control"
        :value= "user.email"
        @input= "user.email = $event.target.value"
    >
</div>
```
```javascript
new Vue({
    data() {
        return {
            options: ['option1', 'option2', 'option3'],
            selectedOption: ''   
        }
    }
})
``` 
### Custom input component  ###
* Custom.vue
```vue
<template>
    <div>
        <div
            id="on"
            @click="sendToParent(true)"
            :class="{active: value}">On</div>
        <div
            id="off"
            @click="sendToParent(false)"
            :class="{active: !value}">Off</div>
    </div>
</template>
<script>
export default {
    props: ['value'],
    methods: {
        sendToParent(newVale) {
            this.value = newVale;
            return this.$emit('input', newVale);
        }
    }     
}
</script>    
```

* App.vue
```vue
<template>
    <div>
        <app-custom
        v-model:customComponentValue
        ></app-custom>
    </div>
</template>
<script>
import Custom from './Custom.vue'
export default {
    data() {
        return {
            customComponentValue: true
        }
    },
    components: {
        appCustom : Custom
    }      
}
</script>    
```