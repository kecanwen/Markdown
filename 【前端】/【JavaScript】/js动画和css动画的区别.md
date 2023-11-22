# [关于JS动画和CSS3动画的性能差异](https://www.cnblogs.com/kirachen/p/4614788.html)

Chromium项目里，渲染线程分为

> * main thread
>
> * compositor thread


如果CSS只是改变`transforms`和`opacity`，这时整个CSS动画得以在compositor thread完成

而JS动画则会在main thread执行，然后触发compositor进行下一步操作
		

在JS执行一些昂贵的任务时，main thread繁忙，CSS动画由于使用了compositor thread可以保持流畅

> 在主线程main thread中，维护了一棵Layer树，管理了TiledLayer
>
> 在compositor thread，维护了同样一颗LayerTreeHostImpl，管理了LayerImpl，
>
> 这两棵树的内容是拷贝关系,因此可以彼此不干扰.
>
> 当Javascript在main thread操作LayerTreeHost的同时，compositor thread可以用LayerTreeHostImpl做渲染。
>
> 当Javascript繁忙导致主线程卡住时，合成到屏幕的过程也是流畅的。
>
> 为了实现防假死，鼠标键盘消息会被首先分发到compositor thread，然后再到main thread。
>
> 这样，当main thread繁忙时，compositor thread还是能够响应一部分消息
>
> 例如，鼠标滚动时，加入main thread繁忙，compositor thread也会处理滚动消息，滚动已经被提交的页面部分（未被提交的部分将被刷白）。

CSS动画比JS流畅的前提：

- 在Chromium基础上的浏览器中
- JS在执行一些昂贵的任务
- 同时CSS动画不触发（layout）回流或（paint）重绘
  在CSS动画或JS动画触发了paint或layout时，需要main thread进行Layer树的重计算，这时CSS动画或JS动画都会阻塞后续操作。

如下属性的修改才符合“仅触发Composite，不触发layout或paint：

- backface-visibility
- opacity
- perspective
- perspective-origin
- transfrom

所以只有用上了3D加速或修改opacity时，才有机会用得上CSS动画的这一优势。

因此，在大部分应用场景下，效率角度更值得关注的还是下列问题。

- 是否导致layout
- repaint的面积
- 是否是有高消耗的属性（css shadow等）
- 是否启用硬件加速

------

现今CSS动画和JS动画主要的不同点是

- 功能涵盖面，JS比CSS3大

  > - 定义动画过程的`@keyframes`不支持递归定义，如果有多种类似的动画过程，需要调节多个参数来生成的话，将会有很大的冗余（比如jQuery Mobile的动画方案），而JS则天然可以以一套函数实现多个不同的动画过程
  > - 时间尺度上，`@keyframes`的动画粒度粗，而JS的动画粒度控制可以很细
  > - CSS3动画里被支持的时间函数非常少，不够灵活
  > - 以现有的接口，CSS3动画无法做到支持两个以上的状态转化

- 实现/重构难度不一，CSS3比JS更简单，性能调优方向固定

- 对于帧速表现不好的低版本浏览器，CSS3可以做到自然降级，而JS则需要撰写额外代码

- CSS动画有天然事件支持（`TransitionEnd`、`AnimationEnd`，但是它们都需要针对浏览器加前缀），JS则需要自己写事件

- CSS3有兼容性问题，而JS大多时候没有兼容性问题