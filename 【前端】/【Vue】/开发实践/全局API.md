###  extend 有什么作用

这个 API 很少用到，作用是**扩展组件生成一个构造器**，通常会与`$mount`一起使用

```js
// 创建组件构造器
let Component = Vue.extend({  template: '<div>test</div>'})
// 挂载到 #app 上
new Component().$mount('#app')
// 除了上面的方式，还可以用来扩展已有的组件
let SuperComponent = Vue.extend(Component)
new SuperComponent({    
    created() {       
       console.log(1)    
    }
})
new SuperComponent().$mount('#app')
```