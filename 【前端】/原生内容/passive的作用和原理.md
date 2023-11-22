## passived到底有什么用？

passived主要用于优化浏览器页面滚动的性能，让页面滚动更顺滑~~

## passived产生的历史时间线

addEventListener()：大家都是认识的，为dom添加触发事件，故事就从这里开始。
在早期addEventListener是这样的：

```reasonml
addEventListener(type, listener, useCapture)
```

useCapture:是否允许事件捕捉，但是很少会传true，然后就变成可选项了：

```reasonml
addEventListener(type, listener[, useCapture ])
```

到现在就变成了这个样子：

```flix
addEventListener(type, listener, {
    capture: false, //捕获
    passive: false, 
    once: false    //只触发一次
})
```

我们的主角passive就出现了

## passive为什么能优化页面的滚动性能？

### 简述chrome的线程化渲染框架

#### chrome的线程化渲染框架的两个线程：

- 内核线程（Main/Render Thread）：负责DOM树构建、元素的布局、图层绘制记录部分（main-thread side）、JavaScript的执行
- 合成线程（Compositor Thread）：图层绘制实现部分（impl-side）、图层图像合成

![clipboard.png](D:\Markdown\图片\bVbkwyp.png)
上图可知，页面Frame#1在内核线程中完成js执行、布局和绘制后，经过一个周期合成线程去执行Frame#1页面图像的合成。

用户输入事件分类：

- 在内核线程处理的事件
- 直接由合成线程处理的事件

#### 那么有什么区别呢？

**在内核线程处理的事件：需要经过内核线程处理的输入事件要在内核线程执行逻辑，遇到内核线程在忙，无法立即响应。**如用户的大部分输入事件都跟页面元素有关系，一旦页面元素注册了对应事件的监听器，监听器的逻辑代码（JavaScript）必须在内核线程中执行（V8引擎运行在内核线程），因此这种输入事件经常无法立即得到响应。
**直接由合成线程处理的事件：不经过内核线程就能快速处理的输入事件为手势输入事件（滑动、捏合）**。

**划重点：最骚的来了，虽然手势事件可以不在内核线程处理，但是手势事件的产生还是离不开内核线程。**

### 页面卡顿的原因

手势事件有个属性 cancelable,作用是告诉浏览器该事件是否允许监听器通过 preventDefault() 方法阻止，默认为true。如果在touch事件内部调用preventDefault()，事件默认行为被取消，页面也就静止不动了。但是浏览器并不知道touch事件内部是否调用了preventDefault()，**浏览器只有等内核线程执行到事件监听器对应的JavaScript代码时，才能知道内部是否会调用preventDefault函数来阻止事件的默认行为，所以浏览器本身无法优化这种场景**。手势输入事件是由连续的普通输入事件组成的，在这种场景下，无法快速产生，会导致页面无法快速执行滑动逻辑，从而让用户感觉到页面卡顿。

而Chrome团队从统计数据中分析得出，注册了mousewheel/touch相关事件监听器的页面中，80%的页面内部都不会调用preventDefault函数来阻止事件的默认行为。对于这80%的页面，即使监听器内部什么都没有做，相对没有注册mousewheel/touch事件监听器的页面，在滑动流畅度上，有10%的页面增加至少100ms的延迟，1%的页面甚至增加500ms以上的延迟。Chrome团队认为对于统计中的这80%的页面来说，他们都是不希望因为注册mousewheel/touch相关事件监听器而导致滑动延迟增加的。

### passive的诞生

所以，passive 监听器诞生了，passive 的意思是“顺从的”，表示它不会对事件的默认行为说 no，浏览器知道了一个监听器是 passive 的，它就可以在两个线程里同时执行监听器中的 JavaScript 代码和浏览器的默认行为了。

经过上面的分析，我们了解到了Passive Event Listeners特性实际上是为了解决浏览器页面滑动流畅度而设计的，它通过扩展事件属性passive让Web开发者来告知浏览器监听器是否会阻止事件的默认行为，从而让浏览器可以更智能地决策并优化，这其中涉及到了Chrome的多线程渲染框架、输入事件处理等知识。