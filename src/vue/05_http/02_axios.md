# AXIOS #
### Links ###
https://github.com/axios/axios
### npm ###
```bash
npm install --save axios
```

### POST ###
* App.vue
```vue
<script>
import axois from 'axios';
export default {
    methods: {
        onSubmit() {
            const formData = {
                name: this.name, 
                email: this.user
            }
            axois.post('url', formData)
                .then(response => console.log(response))
                .catch(error => console.log(error)); 
        }   
    }
}
</script>
```

### GET ###
* App.vue
```vue
<script>
import axois from 'axios';
export default {
    created() {
        axois.get('url')
            .then(response => console.log(response))
            .catch(error => console.log(error)); 
    }   
}
</script>
```

