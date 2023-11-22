### setState真的是异步的吗？

这两天自己简单的看了下 setState 的部分实现代码，在这边给到大家一个自己个人的见解，可能文字或图片较多，没耐心的同学可以直接跳过看总结(**源码版本是16.4.1**)。

**看之前，为了方便理解和简化流程，我们默认react内部代码执行到performWork 、performWorkOnRoot、performSyncWork、performAsyncWork这四个方法的时候，就是react去update更新并且作用到UI上。**

### 一、合成事件中的setState

首先得了解一下什么是合成事件，react为了解决跨平台，兼容性问题，自己封装了一套事件机制，代理了原生的事件，像在jsx中常见的onClick、onChange这些都是合成事件。

```react
class App extends Component {
  state = { val: 0 }
  increment = () => {
    this.setState({ val: this.state.val + 1 })
    console.log(this.state.val) // 输出的是更新前的val --> 0
  }
  render() {
    return (
      <div onClick={this.increment}>
        {`Counter is: ${this.state.val}`}
      </div>
    )
  }
```

}