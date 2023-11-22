```javascript
component: (resolve) => require(['@/views/features/404'], resolve),
```

这里使用了动态导入（dynamic import）的方式加载组件，其中 `require` 函数用于异步加载指定路径的模块或文件。在这种语法下，**`resolve` 是 `require` 函数的第二个参数，它是一个回调函数，用于处理加载完成后的结果**。

在这个特定的例子中，`resolve` 回调函数接收一个参数，表示成功加载的模块。当 `require(['@/views/features/404'], resolve)` 执行完毕时，会将成功加载的模块作为参数传递给 `resolve` 回调函数。

因此，整个表达式的作用是：当路由需要渲染该组件时，通过动态导入的方式异步加载位于 `'@/views/features/404'` 路径下的组件，并将加载完成的模块作为参数传递给 `resolve` 回调函数。这样可以实现按需加载组件，提高应用程序的性能和加载速度
