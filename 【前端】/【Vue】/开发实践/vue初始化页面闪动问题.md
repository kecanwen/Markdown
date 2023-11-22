使用vue开发时，**在vue初始化之前，由于div是不归vue管的**，所以我们写的代码在还没有解析的情况下会容易出现花屏现象，看到类似于{{message}}的字样，虽然一般情况下这个时间很短暂，但是还是有必要让解决这个问题的。

首先：在css里加上以下代码：

```js
[v-cloak] {display: none;}
```

> 如果没有彻底解决问题，则在根元素加上
> 		`style="display: none;" :style="{display: 'block'}"`