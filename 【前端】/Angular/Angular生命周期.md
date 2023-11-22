#### 绑定数据改变时触发的生命周期函数

**ngDoCheck** 查看数据是否改变

**ngAfterContentChecked **组件渲染完成，做一些自定义操作

**ngAfterViewChecked **组件渲染完成后调用

**ngOnChanges **当被绑定的输入属性的值发生变化时调用(父子组件传值的时候会触发)



#### 带有Init的生命周期函数只会触发一次

**ngOnInit** 初始化组件 指令

**ngAfterContentInit** 组件挂载完成

**ngAfterViewInit** 组件初次挂载完成后只调用一次

