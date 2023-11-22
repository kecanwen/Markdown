> Vue能够随意调整 **绑定的粒度**，本质还要归功于 **变化侦测**

**Vue中渲染页面的过程：**

1. 通过编译，将模板转换成渲染函数
2. 执行渲染函数，就可以得到一个虚拟节点树
3. 将新的虚拟节点树和旧的虚拟节点树通过 diff 算法进行对比
3. 最后更新视图

![image-20220212110032654](C:\Users\10072598\AppData\Roaming\Typora\typora-user-images\image-20220212110032654.png)

> Vue目前对状态的侦测策略采用了中等粒度。当状态发生变化时，只通知到组件级别，然后组件内使用虚拟DOM来渲染视图

![image-20220212112309146](C:\Users\10072598\AppData\Roaming\Typora\typora-user-images\image-20220212112309146.png)

VNode是一个类，可以生成不同类型的vnode实例，而不同的vnode可以生成不同类型的DOM元素