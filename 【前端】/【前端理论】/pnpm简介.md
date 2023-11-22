#### 一、概念

performant npm ，意味“高性能的 npm”。pnpm由npm/yarn衍生而来，解决了npm/yarn内部潜在的bug，极大的优化了性能，扩展了使用场景。被誉为“最先进的包管理工具”

#### 二、特点：

速度快、节约磁盘空间、支持monorepo、安全性高

pnpm 相比较于 yarn/npm 这两个常用的包管理工具在性能上也有了极大的提升，根据目前官方提供的 benchmark 数据可以看出在一些综合场景下比 npm/yarn 快了大概两倍。

#### 三、存储管理：

按内容寻址、采用symlink

#### 四、依赖管理：

npm1、npm2采用递归管理，npm3、npm3+、yarn依赖扁平化管理消除依赖提升。

pnpm依赖策略：消除依赖提升、规范拓扑结构

#### 五、安全

之前在使用 npm/yarn 的时候，由于 node_module 的扁平结构，如果 A 依赖 B， B 依赖 C，那么 A 当中是可以直接使用 C 的，但问题是 A 当中并没有声明 C 这个依赖。因此会出现这种非法访问的情况。 但 pnpm 自创了一套依赖管理方式，很好地解决了这个问题，保证了安全性。

#### 六、安装：

```js
npm i pnpm -g
```

#### 七、查看版本信息： 

```
pnpm -v
```

#### 八、升级版本

```js
pnpm add -g pnpm to update 
```

#### 九、设置源： 

```js
pnpm config get registry //查看源

pnpm config set registry https://registry.npmmirror.com //切换淘宝源 
```

#### 十、安装项目依赖 

```js
pnpm install
```

#### 十一、运行项目

```js
pnpm run dev 
```

