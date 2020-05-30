# CSS #
### Attach or not class by click code in htlm ###
```html
<div 
    @click = "applied = !applied"
    :class="['red-text', {classNameVariable: applied}]"
></div>
```
```javascript
new Vue({
  data: {
      applied: false
      }
})
```
```css
.classNameVariable {
    background-color: red;
} 
.red-text {
    color: red;
} 
```
### Attach or not class by click code in vue ###
```html
<div 
    @click = "applied = !applied"
    :class="divClass"
></div>
```
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

### CSS Multi classes ###
```html
<div 
    @click = "applied = !applied"
    :class="[divClass, {red : attached}]"
></div>
```

### Attach CSS without classes ###
```html
<div 
    :style="{'background-color' : 'red'}"
    :style="{backgroundColor : color}"
    :style="myStyle"
></div>
```
```javascript
new Vue({
  data: {
      color: 'green'
  }, 
  computed: {
    myStyle() {
        return { backgroundColor: this.color };
    }   
  }
})
```