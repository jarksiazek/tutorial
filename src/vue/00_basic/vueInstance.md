# Vue instance #
https://vuejs.org/v2/api/  
http://vuejs.org/guide/instance.html
### $el ###
- it refers to our template
```javascript
new Vue({
  data: {
      applied: false
      },
  computed: {
    divClass() {
        return {classNameVariable: applied};
    }   
  }
})
```

### $data ###
- holds data properties
```javascript
const vm1 = new Vue({
  data: {
      title: "Title"
  } 
})

console.log(vm1.$data.title);
```

```javascript
const data = { title: "title" }
const vm1 = new Vue({
  data: {
      title: data
  } 
})

console.log(vm1.$data === data);
```

### $refs ###
```html
<div id="app">
 <div ref="myDiv"></div>
</div>
```
```javascript
const data = { title: "title" }
const vm1 = new Vue({
    el: "app",
    data: {
      title: data
    },
    methods: {
        getRef(){
            console.log(this.$refs.myDiv)    
        }       
    }    
})

console.log(vm1.$data === data);
```

### mount ###
```javascript
const vm1 = new Vue({
    data: {
      title: data
    },
    methods: {
        getRef(){
            console.log(this.$refs.myDiv)    
        }       
    }    
})

vm1.$mount("app") //similar to #el:"app"
```

### template ###
```javascript
const vm1 = new Vue({
    el: "app"
    template: `<div></div>`
})
```

### Component ###
```html
<hello></hello>
```
```javascript
Vue.component ('hello', { template: `<h1>hello</h1>` })
```
