# vue-filter-char
自定义一个vue指令 全局禁止输入特殊字符


```html
<!--   .vue     -->
<template>
    <div id="">
        <input type="text" v-model="newValue" v-filter-special-char="name">
    </div>
</template>
<script>
    export default {
        name: '',
        data(){
            return {
                name:''
            }
        },
        mounted(){

        },
        methods:{

        }
    }
</script>
```


```js
// main.js
Vue.directive('filterSpecialChar', {
    update: function (el, {value,modifiers},vnode) {
        try {
            let newValue = value? value.replace( /[`~!#$%^&*()_\-+=<>?:"{}|,;'\\[\]·~！#￥%……&*（）——\-+={}|《》？：“”【】、；‘’，。、]/g, ""):'';
            if(value !== newValue){
                // 原生input
                if(el.value){
                    el.value = newValue
                    el.dispatchEvent(new Event(modifiers.lazy ? 'change' : 'input'))
                }
                // element ui input
                else {
                    el.children[0].value = newValue
                    el.children[0].dispatchEvent(new Event(modifiers.lazy ? 'change' : 'input'))
                }
            }

        } catch (e) {
            console.log(e)
        }
    }
})
```
