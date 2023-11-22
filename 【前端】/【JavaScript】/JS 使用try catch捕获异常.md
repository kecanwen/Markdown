### **try catch finally使用**

> try语句允许定义在执行时进行错误测试的代码块。
>
> catch语句允许定义当 try代码块发生错误时，所执行的代码块。
>
> finally语句在 try和 catch之后无论有无异常都会执行。

**注意点：** **`catch` 和 `finally`语句都是可选的，但在使用 `try`语句时必须至少使用一个。当错误发生时， JavaScript 会停止执行，并生成一个错误信息。可以使用`throw`语句 来创建自定义消息(抛出异常)**

```js
try {
    // tryCode - 尝试执行代码块
}
catch(err) {
    // catchCode - 捕获错误的代码块
}
finally {
    // finallyCode - 无论 try / catch 结果如何都会执行的代码块
}
```

### **异常处理的必要**

增强用户体验，准确定位问题，完善的前端处理方案比如前端监控系统

### **异常处理的场景**

> 1. JS 语法错误、代码异常
> 2. Promise 异常
> 3. Iframe 异常
> 4. 跨域异常
> 5. 接口请求AJAX 请求异常
> 6. 静态资源导入加载异常

### **try catch的注意点**

> 只能捕获到同步的异常，不能捕获语法和异步的异常，在日常使用中需要注意

```js
// 不能捕获语法的异常
try { 
  let name = 'aaa   // 少写'
  } catch(e) {
  console.log('捕获到异常：',e); 
}
// VM421:1 Uncaught SyntaxError: Unexpected identifier

// 不能捕获异步的异常
try { 
  setTimeout(() => { 
    console.log(a) // 未声明a变量
  }, 1000) } catch(e) { 
  console.log('捕获到异常：',e); 
} 
// blog.js:1 Uncaught ReferenceError: a is not defined
```