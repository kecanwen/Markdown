https://blog.csdn.net/qq_41960279/article/details/124817190

## 前言

写过hybrid的同学，想必都会遇到这样的需求，如果用户安装了自己的APP，就打开APP或跳转到APP内某个页面，如果没安装则引导用户到对应页面或应用商店下载。这里就涉及到了H5与Native之间的交互，为什么H5能够唤起APP并且跳转到对应的页面？

就算你没写过想必也体验过，最常见的就是抖音里面的一些广告，如果你点击了广告，他判断你手机装了对应APP，那他就会去打开那个APP，如果没安装，他会帮你跳转到应用商店去下载，这个还算人性化一点的，有些直接后台给你去下载，你完全无感知。



## 唤端体验

有了这项技术我们就可以实现H5唤起APP应用了，现阶段的引流方式大都得益于这种技术，比如广告投放、用户拉新、引流等。


唤端技术我们也称之为deep link技术。当然，不同平台的实现方式有些不同，

**一般常见的有这几种，分别是：**

- URL Scheme（通用）

- Universal Link （iOS）
- App Link、Chrome Intents（android）

#### URL Scheme（通用）

这种方式是一种比较通用的技术，各平台的兼容性也很好，它一般由协议名、路径、参数组成。

这个一般是由Native开发的同学提供，我们前端同学再拿到这个scheme之后，就可以用来打开APP或APP内的某个页面了。

```js
URL Scheme 组成
[scheme:][//authority][path][?query][#fragment]

常用APP的 URL Scheme
APP	微信	支付宝	淘宝	QQ	知乎
URL Scheme	weixin://	alipay://	taobao://	mqq://	zhihu://
常用的有以下这几种方式
```

直接通过window.location.href跳转window.location.href = 'zhihu://'

#### **判断是否成功唤起**

当用户唤起APP失败时，我们希望可以引导用户去进行下载。

那么我们怎么才能知道当前APP是否成功唤起呢？

我们可以监听当前页面的visibilitychange事件，如果页面隐藏，则表示唤端成功，

否则唤端失败，跳转到应用商店。

首先我手机上并没有安装腾讯微博，所以也就无法唤起，我们让他跳到应用商店对应的应用下载页，

这里就用淘宝的下载页来代替一下～



```vue
<template>
  <div class="open_app">
      <div class="open_app_title">前端南玖唤端测试Demo</div>
      <div class="open_btn" @click="open">打开腾讯微博</div>
  </div>
</template>
<script>
let timer
export default {
    name: 'openApp',
    methods: {
        watchVisibility() {
            window.addEventListener('visibilitychange', () => {
                // 监听页面visibility
                if(document.hidden) {
                    // 如果页面隐藏了，则表示唤起成功，这时候需要清除下载定时器
                    clearTimeout(timer)
                }
            })
        },
        open() {
            timer = setTimeout(() => {
              // 没找到腾讯微博的下载页，这里暂时以淘宝下载页代替
                window.location.href = 'http://apps.apple.com/cn/app/id387682726'
            }, 3000)
            window.location.href = 'TencentWeibo://'
        }
    }
}
</script>

<style lang="less">
.open_app_title {
    font-size: (20/@rem);
}
.open_btn{
    margin-top:(20/@rem);
    padding:(10/@rem) 0;
    border-radius: (8/@rem);
    background: salmon;
    color: #fff;
    font-size: (16/@rem);
}
</style>
```

### 适用性

URL Scheme 这种方式兼容性好，无论安卓或者 iOS 都能支持，是目前最常用的方式。

**从上图我们能够看出它也有一些比较明显的缺点：**

无法准确判断是否唤起成功，因为本质上这种方式就是打开一个链接，并且还不是普通的 http 链接，所以如果用户没有安装对应的 APP，

那么尝试跳转后在浏览器中会没有任何反应，通过定时器来引导用户跳到应用商店，

但这个定时器的时间又没有准确值，不同手机的唤端时间也不同，我们只能大概的估计一下它的时间来实现，一般设为3000ms左右比较合适；

从上图中我们可以看到会有一个弹窗提示你是否在对应 APP中打开，这就可能会导致用户流失；

有 URL Scheme 劫持风险，比如有一个 app 也向系统注册了 zhihu:// 这个 scheme ，唤起流量可能就会被劫持到这个 app 里；

容易被屏蔽，app 很轻松就可以拦截掉通过 URL Scheme 发起的跳转，比如微信内经常能看到一些被屏蔽的现象。

