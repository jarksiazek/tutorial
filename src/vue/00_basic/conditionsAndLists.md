# CONDITIONS #
### v-if v-show ###

Official Docs - Conditionals: http://vuejs.org/guide/conditional.html  
Official Docs - Lists: http://vuejs.org/guide/list.html

v-if removing element from DOM
v-show hiding element from DOM
```html
<div>
    <p v-if="show">Show if</p>
    <p v-else="show">Show else</p>
    <p v-show="show">Some data2</p>
</div>
```
```javascript
new Vue({
  data: {
      show: true
      }
})
```

### v-for ###
v-if removing element from DOM
v-show hiding element from DOM
```html
<div>
    <ul>
        <li v-for="item in ingredients">{{ item }}</li>
        <li v-for="(item, index) in ingredients"> {{ index }} {{ item }}</li>
    </ul>
    <ul>
        <li v-for="person in persons">
            <span v-for="(value, key, index) in person">{{value}}</span>
        </li>
    </ul>
    <span v-for="n in 100"></span>
</div>
```
```javascript
new Vue({
  data: {
    ingredients: ['meat', 'fruit', 'cookies'],
    persons: [
       {name: 'Max', age: 27, color: 'red'},
       {name: 'Anna', age: 'unknown', color: 'blue'}
    ]
  }
})
```