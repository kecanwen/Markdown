## XSS（跨站脚本攻击）和CSRF（跨站请求伪造）防御

- XSS（Cross Site Script）是利用用户对指定网站的信任
- CSRF（Cross Site Request Forgery）是利用网站对用户的信任

### XSS：跨站脚本

当用户浏览该页时，这些嵌入在html的恶意代码就会被执行，用户浏览器被攻击者控制。

1. 盗取用户的cookies，伪造用户身份。
2. 控制用户浏览器
3. URL跳转漏洞
4. 钓鱼网站

### CSRF：跨站请求伪造(冒充用户，伪造请求)

冒充用户在站内的正常操作。绝大多数网站是通过 cookie 等方式辨识用户身份（包括使用服务器端 Session 的网站，因为 Session ID 也是大多保存在 cookie 里面的），再予以授权的。

**CSRF漏洞检测：**
	最简单的方法就是抓取一个正常请求的数据包，去掉Referer字段后再重新提交

​	如果该提交还有效，那么基本上可以确定存在CSRF漏洞。

**防御CSRF攻击**:

主要有三种策略：验证 HTTP Referer 字段；在请求地址中添加 token 并验证；在 HTTP 头中自定义属性并验证。
（1）验证 HTTP Referer 字段
	HTTP 头中有一个字段叫 Referer，它记录了该 HTTP 请求的来源地址。
	问题： Referer 值会记录下用户的访问来源，有些用户认为这样会侵犯到他们自己的隐私权。

（2）在请求地址中添加 token 并验证
	  token 可以在用户登陆后产生并放于 session 之中，然后在每次请求时把 token 从 session 中拿出，与请求中的 token 进行	比对，但这种方法的难点在于如何把 token 以参数的形式加入请求。

（3）在 HTTP 头中自定义属性并验证
	  不是把 token 以参数的形式置于 HTTP 请求之中，而是把它放到 HTTP 头中自定义的属性里。通过 XMLHttpRequest 这个类，可以一次性给所有该类请求加上 csrftoken 这个 HTTP 头属性，并把 token 值放入其中。

