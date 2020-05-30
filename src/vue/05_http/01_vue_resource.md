# VUE RESOURCE #
### Links ###
https://github.com/pagekit/vue-resource
### npm ###
```bash
npm install vue-resource
```

### setup ###
* main.js
```javascript
import VueResource from 'vue-resource';

Vue.use(VueResource);
```

### POST ###
* App.vue
```vue
<script>
export default {
    data() {
        return { 
            user: {
                username: '', 
                email: ''
            }
        }
    },
    methods: {
        submit() {
            this.$http.post('url/data.json', this.user)
                .then(response => {
                    console.log(response);
                }, error => {
                    console.log(error);
                }); 
        }
    }   
}
</script>
```

### GET ###
* App.vue
```vue
<script>
export default {
    data() {
        return { 
            users: []
        }
    },
    methods: {
        fetch() {
            this.$http.get('url/data.json')
                .then(response => {
                    return response.json()
                })
                .then(data => {
                    const resArray = [];
                    for (let key in data) {
                        resArray.push(data[key]);
                    }   
                    this.users = data;
                })      
        }
    }   
}
</script>
```

### INTERCEPTORS REQUEST AND RESPONSE (next) ###
* main.js
```javascript
Vue.http.interceptors.push((request, next) => {
    console.log(request);
    request.method = 'PUT';
    next(response => {
        console.log(response);
    });
})
```

### RESOURCE ###
* main.js  
```vue
<script>
export default {
    data() {
        return { 
            user: {
                name: '', 
                email: ''
            },
            resources: {}
        }
    },
    methods: {
        submit(){
            this.resource.save({}, this.user);
        }   
    },
    created() {
        this.resource = this.$resource('data.json')
    }   
}
</script>
```

### CUSTOM RESOURCE ###
* main.js  
```vue
<script>
export default {
    methods: {
        submit() {
            this.resource.saveAlt(this.user);
        }
    },
    created() {
        const customActions() = {
            saveAlt: {method : 'POST', url: "customUrl"}
        };           
        this.resource = this.$resource('data.json', {}, customActions)
    }   
}
</script>
```

### URI TEMPLATES ###
https://medialize.github.io/URI.js/uri-template.html