JavaScript默认是同步加载（又称阻塞模式），这种模式在加载js文件时，会影响后续页面的渲染，一旦网速不好，整个页面将会等待js文件的加载，从而不进行后续页面的渲染，这也是提倡将<script>标签放在</body>标签之前的原因。

另外，有些js文件是按需加载的，用的时候加载，不用时不必加载。所以引入了异步加载模式（非阻塞模式），即浏览器在下载执行js文件时，会同时进行后续页面的处理。

1.**defer** —— 以前适用于IE，现在适用于所有主流浏览器

defer属性规定是否对脚本执行进行延迟，直到页面加载为止

defer属性的值只有defer一个，即 defer = 'defer'，可直接写defer

用法：在script标签里加入defer属性即可，适用于所有script脚本

<script src='http://cdn.bootcss.com/jquery/3.0.0-beta1/jquery.min.js' defer></script>
添加defer属性后，js脚本在所有元素加载完成后执行，而且是按照js脚本声明的顺序执行

2.**async** —— h5新属性

async属性规定一旦脚本可用，则会异步执行

async的用法和defer一样，但async只适用于外部引用的脚本，即script有src属性时才可使用

<script src='http://cdn.bootcss.com/jquery/3.0.0-beta1/jquery.min.js' async></script>
不同的是，添加async属性后，js脚本是**乱序执行**的，不管你声明的顺序如何，只要某个js脚本加载完就立即执行

3.动态生成script标签

在js里创建script标签，插入DOM中，加载完成后callback
这样所有的js脚本都会在onload事件后才加载，onload事件会在所有文件内容（包括文本、图片、CSS文件等）加载完成后才开始执行，极大的优化了网页的加载速度，提高了用户体验

