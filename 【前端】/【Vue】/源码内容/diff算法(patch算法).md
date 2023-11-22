## patch算法

**一 .原因**

​	减少直接操纵Dom,显著提升性能;操作javaScript的效率远高于操作DOM

**二**.**具体过程**

* 当oldVnode不存在时，直接使用vnode渲染视图；
* 当oldVnode和vnode都存在但并不是同一个节点时，使用vnode创建的DOM元素替换旧的DOM元素；
* 当oldVnode和vnode是同一个节点时，使用更详细的对比操作对真实的DOM节点进行更新。

**三.图解**

​	![image-20220215162451218](C:\Users\10072598\AppData\Roaming\Typora\typora-user-images\image-20220215162451218.png)	

[TOC]

diff算法完整流程

![img](file:///D:/Mycomputer/My Documents/WXWork/1688858224239468/Cache/Image/2022-02/企业微信截图_16449146215085.png)		   	

