# data-*

**data-\*** [全局属性](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes) 是一类被称为**自定义数据属性**的属性，它赋予我们在所有 HTML 元素上嵌入自定义数据属性的能力，并可以通过脚本在 [HTML](https://developer.mozilla.org/zh-CN/docs/Web/HTML) 与 [DOM](https://developer.mozilla.org/zh-CN/docs/Web/API/Document_Object_Model) 表现之间进行专有数据的交换

### 用法

通过添加 **data-\*** 属性，即使是普通的 HTML 元素也能变成相当复杂且强大的编程对象。例如，在游戏里的太空船 "[sprite](https://en.wikipedia.org/wiki/Sprite_(computer_graphics))" 可以是一个带有一个 [class](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes/class) 属性和几个 data-* 属性的简单 [``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/img) 元素：

```html
<img class="spaceship cruiserX3" src="shipX3.png"
  data-ship-id="324" data-weapons="laserI laserII" data-shields="72%"
  data-x="414354" data-y="85160" data-z="31940"
  onclick="spaceships[this.dataset.shipId].blasted()">
</img>
```

data-* 属性用于存储私有页面后应用的自定义数据。

data-* 属性可以在所有的 HTML 元素中嵌入数据。

自定义的数据可以让页面拥有更好的交互体验（不需要使用 Ajax 或去服务端查询数据）。



### **data-* 属性由以下两部分组成：**

1. 属性名不要包含大写字母，在 data- 后必须至少有一个字符。
2. 该属性可以是任何字符串

**注意：** 自定义属性前缀 "data-" 会被客户端忽略。

