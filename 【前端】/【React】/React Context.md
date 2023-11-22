## 先看看React官网对于Context的介绍



> Context 提供了一个无需为每层组件手动添加 props，就能在组件树间进行数据传递的方法。在一个典型的 React 应用中，数据是通过 props 属性自上而下（由父及子）进行传递的，但这种做法对于某些类型的属性而言是极其繁琐的（例如：地区、用户偏好、UI 主题），这些属性是应用程序中许多组件都需要的。Context 提供了一种在组件之间共享此类值的方式，而不必显式地通过组件树的逐层传递 props。



个人理解转成大白话：`Context`提供了一个**局部的全局作用域**，使用Context则无需再手动的逐层传递`props`。

**本文主要介绍3种`Context`的使用方式：**

1. `React.createContext`提供的`Provider`和`Consumer`
2. 函数组件：`React.createContext`提供的`Provider`和`useContext`钩子
3. Class组件：`React.createContext`提供的`Provider`和`class`的`contextType`属性

### 第一种：React.createContext提供的Provider和Consumer

先写好使用`Context`的基础环境条件，后续的代码都是基于此环境

```javascript
//创建一个文件，暂且命名为context.js，导出createContext()的返回值
import { createContext } from "react";

export default createContext();
复制代码
```

在根组件`App.jsx`中，导入上面写的`context`，并使用`context`提供的`Provider`组件进行包裹，圈定**局部的全局作用域**，传值后可以提供给子组件进行消费

> 当 Provider 的 value 值发生变化时，它内部的所有消费组件都会重新渲染。Provider 及其内部 consumer 组件都不受制于 shouldComponentUpdate 函数，因此当 consumer 组件在其祖先组件退出更新的情况下也能更新。

```javascript
import React, { createContext } from "react";
import MyContext from "./context";

import GeneralC from "./GeneralC";
import FnC from "./FnC";
import ClassC from "./ClassC";

export default function App() {
  return (
    //Provider组件接收一个value属性，此处传入一个带有name属性的对象
    <MyContext.Provider value={{ name: `context's value is string!` }}>
      {/*这里写后面要进行包裹的子组件,此处先行导入后续需要消费context的3个组件*/}
      <GeneralC/>
      <hr/>
      <FnC/>
      <hr/>
      <ClassC/>
    </MyContext.Provider>
  );
}
复制代码
```

在`GeneralC`组件中,导入`context`,使用其提供的`Consumer`组件来订阅`Context`的变更,需要一个函数作为子元素,函数的第一个形参便是`Provider`组件提供的`value`值

```javascript
import React, { useReducer } from "react";
import MyContext from "./context";

const GeneralC = () => {
  return (
    //
    <MyContext.Consumer>
      {(value) => {
        return (
          <div>
            第一种使用Context方式获取的值：{JSON.stringify(value)}
          </div>
        );
      }}
    </MyContext.Consumer>
  );
};

export default GeneralC;
复制代码
```

此时页面中应该出现json格式的value值

![img](D:\Markdown\图片\5aff96ff41b9415984a25c8e21799b00tplv-k3u1fbpfcp-zoom-in-crop-mark3024000.webp)

### 第二种：函数组件：React.createContext提供的Provider和useContext钩子

导入`useContext`钩子函数,该函数接收`createContext()`的返回值,返回的结果为该`context`的当前值,当前的 `context` 值由上层组件中距离当前组件最近的 `<MyContext.Provider>` 的 `value prop` 决定。

```javascript
import React, { useContext } from "react";
import MyContext from "./context";

const FnC = () => {
  const context = useContext(MyContext);
  return <div>第二种使用Context方式获取的值：{JSON.stringify(context)}</div>;
};

export default FnC;
复制代码
```

此时页面中应该出现两条json格式的value值

![img](D:\Markdown\图片\275d2a4ada7d4a5c8c9ef09b8ffc78actplv-k3u1fbpfcp-zoom-in-crop-mark3024000.webp)

### 第三种：Class组件：React.createContext提供的Provider和class的contextType属性

> 挂载在 class 上的 contextType 属性会被重赋值为一个由 React.createContext() 创建的 Context 对象。这能让你使用 this.context 来消费最近 Context 上的那个值。你可以在任何生命周期中访问到它，包括 render 函数中。 使用`static`关键字添加静态属性，和直接在`class`添加属性效果一致,最终都会添加到类上，而不是类的实例上

```javascript
import React, { Component } from "react";
import context from "./context";

class ClassC extends Component {
  static contextType = context;
  render() {
    const value = this.context;
    return <div>第三种使用Context方式获取的值：{JSON.stringify(value)}</div>;
  }
}

// ClassC.contextType = context; //此处与写static关键字作用一致
export default ClassC;
复制代码
```

此时页面中应该出现三条json格式的value值 ![img](D:\Markdown\图片\012b668cc5de4c2998c12b456839b76dtplv-k3u1fbpfcp-zoom-in-crop-mark3024000.webp)

### 既然能读Context，也自然能写Context，改写下代码(部分代码省略)

在`App.js`组件中更改`context`，只是调用组件自身的`setStore`函数

```javascript
import React, { useState } from "react";
//导入useState钩子
...

const value = {
  name: `context's value is string!`
};

export default function App() {
  const [store, setStore] = useState(value);
  //Provider的value不再传入一个简单结构的对象，而是将useState的返回值作为新对象的key/value,子组件便能调用App的setStore函数进行更新
  return (
    <MyContext.Provider value={{ store, setStore }}>
       {/* 在父组件更改Context */}
      <button
        onClick={() => {
          setStore({
            name: "App change value!"
          });
        }}
      >
        App的change context
      </button>
       {/* 此处为组件引入,省略... */}
    </MyContext.Provider>
  );
}
复制代码
```

此时页面中应该出现一个按钮，点击`App的...`按钮时，`store`更新为`App change value!`，订阅了`context`的子组件都能更新到最新的值 ![img](D:\Markdown\图片\0c7da20c38ef4c568d89cd4a8ef708f5tplv-k3u1fbpfcp-zoom-in-crop-mark3024000.webp)

再来改写子组件，在子组件中更新`context`，这里选择`FnC`组件来更新，原代码不需要更改，新增一个按钮，用来调用`context`传入的`setStore`函数

```javascript
import React, { useContext } from "react";
import MyContext from "./context";

const Component = () => {
  const context = useContext(MyContext);
  return (
    <div>
      第二种使用Context方式获取的值：{JSON.stringify(context)}
      <button
        onClick={() => {
          context.setStore({
            name: "FnC change value!"
          });
        }}
      >
        FnC子组件的change context
      </button>
    </div>
  );
};

export default Component;
复制代码
```

此时页面中应该再出现一个按钮，点击`FnC的...`按钮时，`store`更新为`FnC change value!`，效果和在`App`组件中修改一致，这样子组件便也有了更新`context`的能力 ![img](D:\Markdown\图片\4082646f0c1f4ee095c9a7eac0259358tplv-k3u1fbpfcp-zoom-in-crop-mark3024000.webp)

#### 以上便是React中使用Context的3种方式的介绍，可以查阅React官方文档查阅更多对于[Context](https://link.juejin.cn?target=https%3A%2F%2Fzh-hans.reactjs.org%2Fdocs%2Fcontext.html)的介绍


