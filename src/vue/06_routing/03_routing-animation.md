# VUE ROUTING ANIMATION #
### Links ###
https://router.vuejs.org/

### Animation with transition ###
* App.vue 
```vue
<template>
    <div>
        <transition name="slide" mode="out-in">
            <router-view></router-view>
        </transition>
    </div>
</template>
<style>
    /* adding some animation css */ 
</style>
```