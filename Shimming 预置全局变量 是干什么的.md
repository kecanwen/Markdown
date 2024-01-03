Shimming（或称为Polyfilling）是一种在浏览器环境中模拟或填充缺失功能的技术。在Webpack中，Shimming可以用于预置全局变量，即在编译过程中向代码中注入全局变量的定义。

预置全局变量的目的是为了解决一些代码依赖于全局变量的情况。例如，某个库或框架可能依赖于全局变量 `jQuery`，但在项目中并没有显式地引入该全局变量。在这种情况下，可以使用Shimming技术来在编译过程中自动注入全局变量的定义，以满足代码的依赖关系。

通过Webpack的配置，可以使用 `ProvidePlugin` 插件来进行预置全局变量的设置。该插件允许你指定一个全局变量和对应的模块，当代码中使用该全局变量时，Webpack会自动将指定的模块注入到代码中。

下面是一个使用 `ProvidePlugin` 插件预置全局变量的示例：

```javascript
const webpack = require('webpack');

module.exports = {
  // ...
  plugins: [
    new webpack.ProvidePlugin({
      $: 'jquery',
      jQuery: 'jquery',
      'window.jQuery': 'jquery'
    })
  ]
};
```

在上述示例中，我们将全局变量 `$`、`jQuery` 和 `window.jQuery` 都指定为 `jquery` 模块。当代码中使用这些全局变量时，Webpack会自动将 `jquery` 模块注入到代码中，以满足对这些全局变量的依赖。

通过预置全局变量，我们可以方便地处理代码中对全局变量的依赖，而无需手动引入或在每个模块中显式声明全局变量。这提供了一种简化代码依赖管理的方式，并使代码更具可维护性和可移植性。