## 用闭包实现重载的过程学习闭包

```javascript
let global = {
    overLoad:function(){}
};
function Refactoring(func) {
  let oldFunc = global.overLoad; 
  global.overLoad = function () { 
    if (func.length === arguments.length) {//js函数length属性表示有多少个参数
      return func.apply(this, arguments);//arguments:调用global.overLoad函数的参数
    } else if (typeof oldFunc === "function") {
      return oldFunc.apply(this, arguments);//global调用的overLoad函数,所以this指向global
    }
  }
}
Refactoring((name) => console.log(`${name}`))
Refactoring((name, age) => console.log(`${name},${age}岁`))
Refactoring((name, age, province) => console.log(`${name},${age}岁,${province}人`))
global.overLoad('Kecvin') // Kecvin
global.overLoad('Kecvin', 28) // Kecvin，28岁
global.overLoad('Kecvin', 28, '安徽') // Kecvin，28岁，安徽人
```

- #### **什么叫函数的重载**？

  > 根据参数(arguments)数量的不同，返回不同的结果

- ### 以上哪里用到了闭包？

> 关于闭包，网上有很多定义，建议看阮一峰老师这篇，虽然有点久远，但并不过时
>
> [学习JavaScript闭包](http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html)
>
> 其实不必咬文嚼字，我一直认为对于闭包最通俗易懂的解释就是下面的一句话
>
> ***闭包是个函数，而它「记住了周围发生了什么」，我们可以通过它，拿到它周围的东西***
>
> 换言之，闭包就是将函数内部和函数外部连接起来的一座桥梁

- ### 闭包在什么时候销毁 ？

  > js中内存分为【栈 】和 【堆】，闭包函数主体存储在【堆】中，它的引用存储在 【栈】 中，js会定时清理 【堆 】中没有引用的函数

  



