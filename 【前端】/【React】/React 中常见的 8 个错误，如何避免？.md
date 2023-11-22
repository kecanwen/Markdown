 React 开发中常见的一些错误，以及如何避免这些错误。理解这些问题背后的细节，防止犯下类似的错误。

## 1. 组件卸载后执行状态更新

**报错信息：** Can’t perform a React state update on an unmounted component

这个报错就是因为在组件树的某个地方，状态更新被触发到已经卸载的组件上了。也就是说，我们不能在组件销毁后更新 state，防止出现内存泄漏。

```
const Component = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetchAsyncData().then((data) => setData(data));
  }, []);

  // ...
};
```

比如，在请求数据时，由于跳转到了B页面，A页面的数据请求还在进行中，但是页面已经销毁了，就会出现这种情况。那该如何解决这个问题呢？有两种方法：

### （1）组件卸载时取消异步请求

第一种方法（推荐），就是在组件卸载时取消异步请求。一些异步请求库提供了取消异步请求的方法。如果没有使用第三方库，可以使用 `AbortController` 来取消。这种方法本质上就是在组件卸载时取消副作用：

```
const Component = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    const controller = new AbortController();
    fetch(url, { signal: controller.signal }).then((data) => setData(data));
    return () => {
      controller.abort();
    }
  }, []);

  // ...
};
```

### （2）跟踪组件是否已挂载

另外，可以跟踪组件的挂载状态，如果还没挂载或已经卸载，返回 false；否则返回 true：

```
const Component = () => {
  const [data, setData] = useState(null);
  const isMounted = useRef(true);

  useEffect(() => {
    fetchAsyncData().then(data => {
      if(isMounted.current) {
        setData(data);
      }
    });

    return () => {
      isMounted.current = false;
    };
  }, []);

  // ...
}
```

不过，不建议使用这种方法。这样保留了未挂载组件的引用，可能会导致内存泄漏和性能问题。

## 2. 渲染列表时不使用 key

**报错信息：** Warning: Each child in a list should have a unique key prop

React 开发中最常见的就是遍历数组来渲染组件。在JSX中，可以使用`Array.map`将该逻辑嵌入到组件中，并在回调中返回所需的组件。如下：

```
import { Card } from "./Card";

const data = [
  { id: 1, text: "JavaScript" },
  { id: 2, text: "TypeScript" },
  { id: 3, text: "React" }
];

export default function App() {
  return (
    <div className="container">
      {data.map((content) => (
        <div className="card">
          <Card text={content.text} />
        </div>
      ))}
    </div>
  );
}
```

这样会收到如下警告：`Warning: Each child in a list should have a unique key prop`，这表示需要给生成的每个组件一个唯一的key。所以，要在`map`回调返回的JSX的最外层元素添加一个`key`值，该值应该是一个字符串或者数字，并且在这个组件列表中应该是唯一的。

```
export default function App() {
  return (
    <div className="container">
      {data.map((content) => (
        <div key={content.id} className="card">
          <Card text={content.text} />
        </div>
      ))}
    </div>
  );
}
```

尽管不遵守这个要求也不会导致应用崩溃，但它可能会导致一些意外的情况。React 会使用这些`key`来确定列表中的哪些子项发生了更改，并使用此信息来确定可以重用先前 DOM 的哪些部分，以及在重新渲染组件时应该重新计算哪些部分。因此，建议添加 key。

## 3. Hooks 调用顺序错误

**报错信息：** React Hook "useXXX" is called conditionally. React Hooks must be called in the exact same order in every component render

先来看下面的代码：

```
const Toggle = () => {
  const [isOpen, setIsOpen] = useState(false);

  if (isOpen) {
    return <div>{/* ... */}</div>;
  }
  const openToggle = useCallback(() => setIsOpen(true), []);
  return <button onClick={openToggle}>{/* ... */}</button>;
};
```

当 `isOpen` 的值为`true`时，就会直接`return`那个`div`元素。这样当`isOpen`的值为`true`和`false`时`useCallback` Hook的调用顺序就不一致了。这时React就会警告我们：`React Hook "useCallback" is called conditionally. React Hooks must be called in the exact same order in every component render`。这其实就是React官方文档中所说的，**不要在循环，条件或嵌套函数中调用 Hook， 确保总是在 React 函数的最顶层以及任何 `\**return\**` 之前调用他们**。遵守这条规则才能确保 Hook 在每一次渲染中都按照同样的顺序被调用。

可以这样来修改上面的代码：

```
const Toggle = () => {
  const [isOpen, setIsOpen] = useState(false);
  const openToggle = useCallback(() => setIsOpen(true), []);

  if (isOpen) {
    return <div>{/* ... */}</div>;
  }
  return <button onClick={openToggle}>{/* ... */}</button>;
};
```

## 4. useEffect 缺少依赖

**报错信息：** React Hook useEffect has a missing dependency: 'XXX'. Either include it or remove the dependency array

先来看看 React 官网给出的例子：

```
function Example({ someProp }) {
  function doSomething() {
    console.log(someProp);
  }

  useEffect(() => {
    doSomething();
  }, []); 
}
```

在`useEffect`中定义空的依赖数组是不安全，因为它调用的 `doSomething` 函数使用了 `someProp`。这时就会报错：`React Hook useEffect has a missing dependency: 'XXX'. Either include it or remove the dependency array`。当`props`中的`someProp`发生变化时，函数`doSomething`的结果就会发生变化，然而`useEffect`的依赖数组为空，所以就不会执行回调中的内容。

有两种方式来解决这个问题：

- 在`useEffect`中声明其所需函数，这种方式适用于只需要调用一次的函数，比如初始化函数：

```
function Example({ someProp }) {
  useEffect(() => {
    function doSomething() {
      console.log(someProp);
    } 
    doSomething();
  }, [someProp]); 
}
```

- 使用`useCallback`来定义依赖项，确保当自身依赖发生改变时函数主体也会改变：

```
function Example({ someProp }) {
  const doSomething = useCallback(() => {
    console.log(someProp);
  }, [someProp])

  useEffect(() => {
    doSomething();
  }, [doSomething]); 
}
```

## 5. 重新渲染过多

**报错信息：** Too many re-renders. React limits the number of renders to prevent an infinite loop

这个报错就是说重新渲染过多。React 限制渲染的数量以防止无限循环。当组件在很短的时间有太多状态更新时，就可能会发生这种情况。导致无限循环的最常见原因是：

- 直接在渲染中执行状态更新；
- 未向事件处理程序提供适当的回调。

如果遇到这个警告，可以检查组件的这两个方面：

```
const Component = () => {
  const [count, setCount] = useState(0);

  setCount(count + 1); // 渲染中的状态更新

  return (
    <div className="App">
      {/* onClick 没有正确的回调 */}
      <button onClick={setCount((prevCount) => prevCount + 1)}>
        Increment that counter
      </button>
    </div>
  );
}
```

## 6. 渲染的单条数据为对象

**报错信息：** Objects are not valid as a React child / Functions are not valid as a React child

在 React 中，我们可以在组件中渲染到 DOM 中的东西有很多，比如：HTML标签、JSX元素、原始 JavaScript 值、JavaScript 表达式等。但是不能将对象和函数渲染到 DOM 中，因为这两个值不会解析为有意义的值，如果渲染了对象或函数，就会报上面的错误。解决这个问题的方法很简单，就是检查渲染的内容是否是有效的值：

```
const Component = ({ body }) => (
  <div>
    <h1>{/* */}</h1>
    {/* 必须确保 body 是有效的 React child */}
    <div className="body">{body}</div>
  </div>
);
```

## 7. 相邻JSX元素没有包装在封闭标记中

**报错信息：** Adjacent JSX elements must be wrapped in an enclosing tag

这个报错就是说相邻JSX元素必须包装在封闭标记中，也就是必须要有一个根元素：

```
const Component = () => (
  <Nice />
  <Bad />
);
```

从 React 开发人员的角度来看，这个组件只会在另一个组件内部使用。因此，在他们的心智模型中，从一个组件返回两个元素是有意义的，因为生成的 DOM 结构将是相同的，无论外部元素是在此组件中定义还是在父组件中定义。但是，React 无法做出这种假设。该组件可能会在根目录中使用并破坏应用，因为它会导致无效的 DOM 结构。

所以，应该始终将组件返回的多个 JSX 元素包装在一个封闭标记中。可以是一个元素、一个组件或者 React Fragment：

```
const Component = () => (
  <React.Fragment>
    <Nice />
   <Bad />
  </React.Fragment>
);
```

或者直接使用一个空标签来包装两个 JSX 元素：

```
const Component = () => (
  <>
    <Nice />
   <Bad />
  </>
);
```

## 8. 使用旧的状态

先来看一个计数器的例子：

```
const Increaser = () => {
  const [count, setCount] = useState(0);
  
  const increase = useCallback(() => {
    setCount(count + 1);
  }, [count]);
  
  const handleClick = () => {
    increase();
    increase();
    increase();
  };
  
  return (
    <>
      <button onClick={handleClick}>+</button>
      <div>Counter: {count}</div>
    </>
  );
}
```

这里的`handleClick`方法会在点击按钮后执行三次增加状态变量`count`的操作。那么点击一次是否会增加3呢？事实并非如此。点击按钮之后，`count`只会增加1。问题就在于，当我们点击按钮时，相当于下面的操作：

```
const handleClick = () => {
  setCount(count + 1);
  setCount(count + 1);
  setCount(count + 1);
};
```

当第一次调用`setCount(count + 1)`时是没有问题的，它会将`count`更新为1。接下来第2、3次调用`setCount`时，`count`还是使用了旧的状态（count为0），所以也会计算出`count`为1。发生这种情况的原因就是状态变量会在下一次渲染才更新。

解决这个问题的办法就是，**使用函数的方式来更新状态：**

```
const Increaser = () => {
  const [count, setCount] = useState(0);
  
  const increase = useCallback(() => {
    setCount(count => count + 1);
  }, [count]);
  
  const handleClick = () => {
    increase();
    increase();
    increase();
  };
  
  return (
    <>
      <button onClick={handleClick}>+</button>
      <div>Counter: {count}</div>
    </>
  );
}
```

这样改完之后，React就能拿到最新的值，当点击按钮时，就会每次增加3。所以需要记住：**如果要使用当前状态来计算下一个状态，就要使用函数的式方式来更新状态：**