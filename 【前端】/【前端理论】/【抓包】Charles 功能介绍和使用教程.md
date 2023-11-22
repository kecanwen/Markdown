## Charles 简介

Charles 是在 PC 端常用的网络封包截取工具，在做移动开发时，我们为了调试与服务器端的网络通讯协议，常常需要截取网络封包来分析。除了在做移动开发中调试端口外，Charles 也可以用于分析第三方应用的通讯协议。配合 Charles 的 SSL 功能，Charles 还可以分析 Https 协议。

Charles 通过将自己设置成系统的网络访问代理服务器，使得所有的网络访问请求都通过它来完成，从而实现了网络封包的截取和分析。

> Charles 是收费软件，可以免费试用 30 天。试用期过后，未付费的用户仍然可以继续使用，但是每次使用时间不能超过 30 分钟，并且启动时将会有 10 秒种的延时。因此，该付费方案对广大用户还是相当友好的，即使你长期不付费，也能使用完整的软件功能。只是当你需要长时间进行封包调试时，会因为 Charles 强制关闭而遇到影响。

Charles 主要的功能包括：

- 截取 Http 和 Https 网络封包。
- 支持重发网络请求，方便后端调试。
- 支持修改网络请求参数。
- 支持网络请求的截获并动态修改。
- 支持模拟慢速网络。

## 下载安装 Charles



![img](D:\Markdown\图片\16556d8a1d1b5c03tplv-t2oaga2asx-zoom-in-crop-mark3024000.webp)

Charles 支持的操作系统包括：



- Windows 64 bit(msi)
- Windows 32 bit(msi)
- macOS(dmg)
- Linux 64 bit(tar.gz)
- Linux 32 bit(tar.gz)

打开浏览器访问 [Charles 官网](https://link.juejin.cn?target=https%3A%2F%2Fwww.charlesproxy.com%2F) ，下载相应系统的 [Charles 安装包](https://link.juejin.cn?target=https%3A%2F%2Fwww.charlesproxy.com%2Fdownload%2F)，然后安装即可：

- **Windows：** 运行安装应用程序以在程序菜单中安装 Charles。
- **Mac OS X：** 通过双击解压缩下载文件，然后将 Charles 应用程序复制到 Applications 目录中。
- **Linux：** Charles 拥有 [APT](https://link.juejin.cn?target=https%3A%2F%2Fwww.charlesproxy.com%2Fdocumentation%2Finstallation%2Fapt-repository%2F) 和 [YUM](https://link.juejin.cn?target=https%3A%2F%2Fwww.charlesproxy.com%2Fdocumentation%2Finstallation%2Fyum-repository%2F) 存储库，如果你有基于 `Debian` 或基于 `Red Hat` 的 Linux 发行版，这是安装 Charles 的首选方法。否则，将 `tar.gz` 文件解压缩到适当的站点。如果您以前安装过 Charles 并且正在进行升级；首先确保 Charles 没有运行，然后安装或复制在以前安上。通过运行 `bin/charles` 脚本启动 Charles。

> 如果使用 Firefox，也可以下载 Firefox 插件。参考[Firefox Add-On](https://link.juejin.cn?target=https%3A%2F%2Fwww.charlesproxy.com%2Fdocumentation%2Fconfiguration%2Fbrowser-and-system-configuration%2F)

## Charles 主界面介绍

Charles 的主界面视图如下图所示：

![img](D:\Markdown\图片\16560927ac9848eftplv-t2oaga2asx-zoom-in-crop-mark3024000.webp)



### 工具导航栏

Charles 顶部为菜单导航栏，菜单导航栏下面为工具导航栏。视图如下图所示：

![img](D:\Markdown\图片\16560de1a421b600tplv-t2oaga2asx-zoom-in-crop-mark3024000.webp)

工具导航栏中提供了几种常用工具：



- ![img](D:\Markdown\图片\16db3867658eeecetplv-t2oaga2asx-zoom-in-crop-mark3024000.webp) ：清除捕获到的所有请求
- ![img](D:\Markdown\图片\16db386b4b6e0eadtplv-t2oaga2asx-zoom-in-crop-mark3024000.webp) ：红点状态说明正在捕获请求，灰色状态说明目前没有捕获请求。
- ![img](D:\Markdown\图片\16db386f0e10a371tplv-t2oaga2asx-zoom-in-crop-mark3024000.webp) ：灰色状态说明是没有开启网速节流，绿色状态说明开启了网速节流。
- ![img](D:\Markdown\图片\16db38710d3217c3tplv-t2oaga2asx-zoom-in-crop-mark3024000.webp) ：灰色状态说明是没有开启断点，红色状态说明开启了断点。
- ![img](D:\Markdown\图片\16db387471d369dctplv-t2oaga2asx-zoom-in-crop-mark3024000.webp) ：编辑修改请求，点击之后可以修改请求的内容。
- ![img](D:\Markdown\图片\16db387c21f47e6etplv-t2oaga2asx-zoom-in-crop-mark3024000.webp) ：重复发送请求，点击之后选中的请求会被再次发送。
- ![img](D:\Markdown\图片\16db387fb3206808tplv-t2oaga2asx-zoom-in-crop-mark3024000.webp) ：验证选中的请求的响应。
- ![img](D:\Markdown\图片\16db388436059c60tplv-t2oaga2asx-zoom-in-crop-mark3024000.webp) ：常用功能，包含了 Tools 菜单中的常用功能。
- ![img](D:\Markdown\图片\16db3887609ae613tplv-t2oaga2asx-zoom-in-crop-mark3024000.webp) ：常用设置，包含了 Proxy 菜单中的常用设置。

### 主界面视图

Charles 主要提供两种查看封包的视图，分别名为 `Structure` 和 `Sequence`。

- **Structure**： 此视图将网络请求按访问的域名分类。
- **Sequence**： 此视图将网络请求按访问的时间排序。

使用时可以根据具体的需要在这两种视图之前来回切换。请求多了有些时候会看不过来，Charles 提供了一个简单的 `Filter` 功能，可以输入关键字来快速筛选出 URL 中带指定关键字的网络请求。

> 对于某一个具体的网络请求，你可以查看其详细的请求内容和响应内容。如果请求内容是 POST 的表单，Charles 会自动帮你将表单进行分项显示。如果响应内容是 JSON 格式的，那么 Charles 可以自动帮你将 JSON 内容格式化，方便你查看。如果响应内容是图片，那么 Charles 可以显示出图片的预览。

## Charles 菜单介绍

Charles 的主菜单包括：`File`、`Edit`、`View`、`Proxy`、`Tools`、`Window`、`Help`。用的最多的主菜单分别是 `Proxy` 和 `Tools`。

### Proxy 菜单

Charles 是一个 HTTP 和 SOCKS 代理服务器。代理请求和响应使 Charles 能够在请求从客户端传递到服务器时检查和更改请求，以及从服务器传递到客户端时的响应。下面主要介绍 Charles 提供的一些代理功能。Proxy 菜单的视图如下图所示：

![img](D:\Markdown\图片\1655b588d3eb9714tplv-t2oaga2asx-zoom-in-crop-mark3024000.webp)



Proxy 菜单包含以下功能：

- Start/Stop Recording：开始/停止记录会话。
- Start/Stop Throttling：开始/停止节流。
- Enable/Disable Breakpoints：开启/关闭断点模式。
- Recording Settings：记录会话设置。
- Throttle Settings：节流设置。
- Breakpoint Settings：断点设置。
- Reverse Proxies Settings：反向代理设置。
- Port Forwarding Settings：端口转发。
- Windows Proxy：记录计算机上的所有请求。
- Proxy Settings：代理设置。
- SSL Proxying Settings：SSL 代理设置。
- Access Control Settings：访问控制设置。
- External Proxy Settings：外部代理设置。
- Web Interface Settings：Web 界面设置。

#### Recording Settings(记录会话设置)

Recording Settings 和 Start/Stop Recording 配合使用，在 Start Recording 的状态下，可以通过 Recording Settings 配置 Charles 的会话记录行为。Recording Settings 的视图如下图所示：

![img](D:\Markdown\图片\1655b593cefa68c7tplv-t2oaga2asx-zoom-in-crop-mark3024000.webp)

Recording Settings 有 `Options`、`Include`、`Exclude` 三个选项卡：



- Options：通过 Recording Size Limits 限制记录数据的大小。当 Charles 记录时，请求、响应头和响应体存储在内存中，或写入磁盘上的临时文件。有时，内存中的数据量可能会变得太多，Charles 会通知您并停止录制。在这种情况下，您应该清除 Charles 会话以释放内存，然后再次开始录制。在录制设置中，您可以限制 Charles 将记录的最大大小; 这根本不会影响你的浏览，Charles 仅会停止录制。
- Include：只有与配置的地址匹配的请求才会被录制。
- Exclude：只有与配置的地址匹配的请求将不会被录制。

`Include` 和 `Exclude` 选项卡的操作相同，选择 `Add`，然后填入需要监控的Procotol、Host 和 Port等信息，这样就达到了过滤的目的。如下图所示：

![img](D:\Markdown\图片\1655b874abb33809tplv-t2oaga2asx-zoom-in-crop-mark3024000.webp)

还有一种方法就是在一个请求网址上右击选择 `Focus`，然后其他的请求就会被放到一个叫 `Other Host` 的分类里面，这样也达到了过滤的目的。



#### Throttle Settings(节流设置)

Throttle Settings 和 Start/Stop Throttling 配合使用，在 Start Throttling 的状态下，可以通过 Throttle Settings 配置 Charles 的网速模拟配置。Throttle Settings 的视图如下图所示：

![img](D:\Markdown\图片\1655b8f4b564f837tplv-t2oaga2asx-zoom-in-crop-mark3024000.webp)

勾选 Enable Throttling 启用网速模拟配置，在 Throttle Preset 下选择网络类型即可，具体设置可以根据实际情况自行设置。如果只想模拟指定网站的慢速网络，可以再勾选上图中的 `Only for selected hosts` 项，然后在对话框的下半部分设置中增加指定的 hosts 项即可。



Throttle Settings 视图中的选项含义如下：

- Bandwidth：带宽
- Utilistation：利用百分比
- Round-trip：往返延迟
- MTU：字节

#### Breakpoint Settings(断点设置)

Breakpoint Settings 和 Enable/Disable Breakpoints 配合使用，在 Enable Breakpoints 的状态下，可以通过 Breakpoint Settings 配置 Charles 的断点模式。Breakpoint Settings 的视图如下图所示：

![img](D:\Markdown\图片\1655b972ead68ccatplv-t2oaga2asx-zoom-in-crop-mark3024000.webp)

勾选 Enable Breakpoints 启用断点模式，选择 `Add`，然后填入需要监控的Scheme、Procotol、Host 和 Port 等信息，这样就达到了设置断点的目的。然后可以来观察或者修改请求或者返回的内容，但是在这过程中需要注意请求的超时时间问题。或者可以在某个想要设置断点的请求网址上右击选择 Breakpoints 来设置断点。



#### Reverse Proxies Settings(反向代理设置)

反向代理在本地端口上创建 Web 服务器，该端口透明地将请求代理给远程 Web 服务器。反向代理上的所有请求和响应都可以记录在 Charles 中。

如果您的客户端应用程序不支持使用 HTTP 代理，或者您希望避免将其配置为使用代理，那么反向代理很有用。创建原始目标 Web 服务器的反向代理，然后将客户端应用程序连接到本地端口； 反向代理对客户端应用程序是透明的，使您可以查看 Charles 以前可能无法访问的流量。

有关反向代理的更多信息，请访问 [Reverse proxy](https://link.juejin.cn?target=http%3A%2F%2Fen.wikipedia.org%2Fwiki%2FReverse_proxy)

#### Port Forwarding Settings(端口转发)

可以将任何 `TCP/IP` 或 `UDP` 端口配置为使用 `Port Forwarding` 工具从 Charles 转发到远程主机。这样可以调试 Charles 中的任何协议。

在 Macromedia Flash 中调试 XMLSocket 连接时，这尤其有用。

还可以使用 Charles 作为 SOCKS 代理，因此无需设置端口转发。

#### Windows Proxy(记录计算机上的所有请求)

如果想要抓取电脑端的请求，勾选 Windows Proxy 选项即可；如果只需要抓取手机请求，则取消勾选这个选项。

#### Proxy Settings(代理设置)

Proxy Settings 的视图如下图所示：

![img](D:\Markdown\图片\1655bbc155d038e4tplv-t2oaga2asx-zoom-in-crop-mark3024000.webp)

代理端口默认为 8888(可以修改)，并且勾上 `Enable transparent HTTP proxying` 就完成了在 Charles 上的代理设置。



#### SSL Proxy Settings(SSL 代理设置)

SSL Proxy Settings 的视图如下图所示：

![img](D:\Markdown\图片\1655bbfd5ffc683atplv-t2oaga2asx-zoom-in-crop-mark3024000.webp)

勾上 `Enable SSL proxying` 就完成了在 Charles 上的 SSL 代理设置。之后也可以选择 `Add`，然后填入需要监控的 Host 和 Port 信息，这样就达到了针对某个域名启用 SSL 代理的目的。



#### Access Control Settings(访问控制设置)

Access Control Settings 表示访问控制设置。访问控制列表确定谁可以使用此 Charles 实例。通常，您在自己的计算机上运行 Charles，并且您只打算自己使用它，因此 localhost 始终包含在访问控制列表中。也可以选择 `Add`，然后填入允许访问的 IP，这样就达到了允许某个 IP 访问 Charles 的目的。

#### External Proxy Settings(外部代理设置)

External Proxy Settings 表示外部代理设置。可能在网络上有一个代理服务器，必须使用该代理服务器才能访问 Internet。在这种情况下，需要将 Charles 配置为在尝试访问 Internet 时使用现有代理。

可以配置单独的代理地址和端口：

- HTTP
- HTTPS
- SOCKS

> 如果您有 SOCKS 代理，Charles 将把它用于所有非 HTTP(S) 流量，例如端口转发。

#### Web Interface Settings(Web 界面设置)

Web Interface Settings 表示 Web 界面设置。Charles 有一个 Web 界面，可以让您从浏览器控制 Charles，或使用 Web 界面作为 Web 服务使用外部程序。

在 External Proxy Settings 视图中勾选 `Enable the web interface` 选项启用 Web 界面。可以允许匿名访问，也可以配置用户名和密码。还可以通过在配置使用 Charles 作为其代理的 Web 浏览器中访问 [`http://control.charles/`](https://link.juejin.cn?target=http%3A%2F%2Fcontrol.charles%2F) 来访问 Web 界面。

Web界面提供对以下功能的访问：

- 节流控制
  - 激活或停用任何已配置的限制预设
- 录音控制
  - 开始和停止会话录制
- 工具
  - 激活和停用工具
- 会话控制
  - 清除当前会话
  - 以任何支持的格式导出当前会话
  - 以 Charles 的本机会话格式下载当前会话
- 退出查尔斯

通过检查 Web 界面 HTML ，您可以推导出如何将其用作 Web 服务来自动化 Charles。

### Tools 菜单

Charles 是一个 HTTP 和 SOCKS 代理服务器，所有的请求都会经过 Charles。下面主要介绍 Charles 提供的一些实用工具。Tools 菜单的视图如下图所示：

![img](D:\Markdown\图片\1655b590cbdfb345tplv-t2oaga2asx-zoom-in-crop-mark3024000.webp)



Tools 菜单包含以下功能：

- No Caching Settings：禁用缓存设置。
- Block Cookies Settings：禁用 Cookie设置。
- Map Remote Settings：远程映射设置。
- Map Local Settings：本地映射设置。
- Rewrite Settings：重写设置。
- Black List Settings：黑名单设置。
- White List Settings：白名单设置。
- DNS Spoofing Settings：DNS 欺骗设置。
- Mirror Settings：镜像设置。
- Auto Save Settings：自动保存设置。
- Client Process Settings：客户端进程设置。
- Compose：编辑修改。
- Repeat：重复发包。
- Repeat Advanced：高级重复发包。
- Validate：验证。
- Publish Gist：发布要点。
- Import/Export Settings：导入/导出设置。
- Profiles：配置文件。
- Publish Gist Settings：发布要点设置。

#### No Caching Settings(禁用缓存)

No Caching 工具可防止客户端应用程序（如 Web 浏览器）缓存任何资源。因此，始终向远程网站发出请求，您始终可以看到最新版本。

##### 适用范围

该工具可以作用于每个请求(选中 `Enable No Caching` 即可)，也可以仅对你配置的请求启用(启用 No Caching 的同时，请选中 `Only for selected locations`)。当用于选定的请求时，可以使用简单但功能强大的模式匹配将工具的效果限制为指定的主机和路径。

##### 工作原理

No Caching 工具通过操纵控制响应缓存的 HTTP 请求头来防止缓存。从请求中删除 If-Modified-Since 和 If-None-Match 请求头，添加 Pragma：no-cache 和 Cache-control：no-cache。从响应中删除 Expires，Last-Modified 和ETag 请求头，添加 Expires：0 和 Cache-Control：no-cache。

#### Block Cookies Settings(禁用 Cookie)

Block Cookies 工具阻止了 Cookie 的发送和接收。它可用于测试网站，就像在浏览器中禁用了 Cookie 一样。 请注意，网络爬虫（例如 Google）通常不支持 Cookie，因此该工具还可用于模拟网络爬虫网站的视图。

##### 适用范围

该工具可以作用于每个请求(选中 `Enable Block Cookies` 即可)，也可以仅对你配置的请求启用(启用 Block Cookies 的同时，请选中 `Only for selected locations`)。当用于选定的请求时，可以使用简单但功能强大的模式匹配将工具的效果限制为指定的主机和路径。

##### 工作原理

Block Cookies 工具通过操纵控制响应 Cookies 的 HTTP 请求头来禁用 Cookies。从请求中移除 Cookie 请求头，防止 Cookie 值从客户端应用程序（例如 Web 浏览器）发送到远程服务器。从响应中删除 Set-Cookie 请求头，防止请求设置客户端应用程序从远程服务器接收的 Cookie。

#### Map Remote Settings(远程映射)

Map Remote 工具根据配置的映射更改请求站点，以便从新站点透明地提供响应，就好像这是原始请求一样。

通过此映射，您可以从另一个站点提供全部或部分站点。例如：

- 可以把 xk72.com/charles/ 映射到 localhost/charlesdev/ 来为 xk72.com 提供一个子目录；
- 可以把 xk72.com/*.php 这种指定后缀的所有文件映射到 localhost/charlesdev/。

##### 使用建议

如果您拥有站点的开发版本并且希望能够通过开发提供的某些请求浏览实时站点，则 Map Remote 非常有用。例如，您可能希望从开发服务器提供 css 和 images 目录。使用 live.com/css/ 等映射到 dev.com/css/ 或 live.com/*.css 到 dev.com 。

##### 映射类型

- 可以将目录映射到目录，如 xk72.com/charles/ 映射到 localhost/charlesdev/；
- 可以将文件映射到文件，如 xk72.com/charles/download.php 映射到 abc.com/testing/test.html；
- 可以将带有文件模式的目录映射到目录，如 xk72.com/charles/*.php 到 localhost/charlesdev/；
- 如果在目标映射中未指定路径，则 URL 的路径部分将不会更改。如果要映射到根目录，请在目标路径字段中已 `/` 结尾。

##### HTTPS

Map Remote 工具可以将 HTTP 请求映射到 HTTPS 目标，反之亦然，因此您可以将 HTTP 或 HTTPS 站点映射到其对立面。

##### 站点匹配

每个站点匹配可能包含协议、主机、端口和路径模式，以匹配特定的 URL。站点可能包括通配符。当您向此工具添加新站点时，可能会找到有关创建站点匹配的更多帮助。

#### Map Local Settings(本地映射)

Map Local 工具使您可以使用本地文件，就像它们是远程网站的一部分一样。您可以在本地开发文件，并像在线上一样测试它们。本地文件的内容将返回给客户端，就像它是正常的远程响应一样。

Map Local 可以大大加快开发和测试速度，否则您必须将文件上传到网站以测试结果。使用 Map Local，您可以在开发环境中安全地进行测试。

##### 动态文件

动态文件（例如包含服务器端脚本的文件）不会由 Map Local 执行，因此如果文件中有任何脚本，脚本将按原样返回到浏览器，这可能不是预期的结果。如果您想使用动态文件，就好像它们是远程网站的一部分一样，请参阅 Map Remote 工具。

##### 工作原理

当请求与 Map Local 映射匹配时，它会检查与路径匹配的本地文件。它不包括查询字符串（如果有）。如果在本地找到所请求的文件，则将其作为响应返回，就好像它是从远程站点加载的一样，因此它对客户端是透明的。如果在本地找不到所请求的文件，那么该请求会像平常一样由网站提供，返回由真正的服务器提供的数据。

##### 站点匹配

每个站点匹配可能包含协议、主机、端口和路径模式，以匹配特定的 URL。站点可能包括通配符。当您向此工具添加新站点时，可能会找到有关创建站点匹配的更多帮助。

#### Rewrite Settings(重写)

Rewrite 工具允许创建请求和响应在通过 Charles 时修改他们的规则。如：添加或更改头信息、搜索和替换响应内容中的某些文本等。

##### 重写集

重写集可以单独激活和停用。每个集合包含站点和规则的列表。这些站点选择规则将要运行的请求和响应。

##### 重写规则

每个规则都描述了一次重写操作。规则可能会影响请求URL的 Header，正文或部分内容；它可以根据请求或响应来操作；它可以定义搜索、替换或者仅替换样式重写。

##### 站点匹配

每个站点匹配可能包含协议、主机、端口和路径模式，以匹配特定的 URL。站点可能包括通配符。当您向此工具添加新站点时，可能会找到有关创建站点匹配的更多帮助。

##### 调试

当重写操作未按预期工作时，重写工具可能难以调试。如果您遇到问题，请尝试添加一个非常基本的规则，例如添加明显头信息的规则，以便您可以查看规则是否与请求完全匹配。同时打开错误日志中的调试，以获取从 Charles 中的 Window 菜单访问的错误日志中打印的一些调试信息。

#### Black List Settings(黑名单)

Black List 工具允许输入应该被阻止的域名。当 Web 浏览器尝试从被列入黑名单的域名请求任何页面时，该请求将被 Charles 阻止。您还可以输入通配符来阻止其子域名。

#### White List Settings(白名单)

Black List 工具允许输入仅仅被允许的域名。Black List 工具将阻止除被列入白名单的域名之外的所有请求。

> 白名单工具用于仅允许指定的域名；黑名单工具，用于仅屏蔽指定的域名。
>
> 如果一个请求与“黑名单”和“白名单”都匹配，则该请求会被阻止。

#### DNS Spoofing Settings(DNS 欺骗)

DNS Spoofing 工具允许通过将自己的主机名指定给远程地址映射来欺骗 DNS 查找。 当请求通过 Charles 时，您的 DNS 映射将优先。

Charles 包含配置的域名到 IP 地址映射的列表。当针对列出的域名发出请求时，Spoof DNS 插件会发现欺骗 IP 将请求重定向到该地址。主机HTTP标头保持不变，因此就像您的 DNS 服务器返回欺骗性 IP一样。

##### 虚拟主机

虚拟主机是指单个IP地址上有多个站点，Web 服务器根据浏览器中键入的名称确定要请求的站点。更准确地说，它查看请求中发送的主机头。

如果没有为您的站点设置 DNS，那么您通常无法测试它，因为您不能只输入 IP 地址，因为服务器无法获取名称，因此无法将请求与网站。使用 DNS 欺骗工具来克服此问题。

#### Mirror Settings(镜像)

Mirror 工具会在浏览指定站点时，把接收到的响应内容克隆一份，并保存在磁盘上指定的路径下。

保存文件的路径会与浏览站点的目录结构相同，并且 Charles 会为主机名创建一个根目录。文件名从 URL 导出并转换为适合的数据进行保存。查询字符串包含在文件名中。如果收到相同 URL 的两个响应，则后面一个文件会覆盖前面的同名文件，因此保存在镜像中在的响应内容将始终为最新的。

##### 选定站点

可以为每个请求启用该工具，也可以仅为指定站点启用该工具。当用于选定的站点时，可以使用简单但功能强大的模式匹配将工具的效果限制为指定的主机和/或路径。

##### 副作用

如果为请求启用镜像工具，它将导致任何压缩或编码的响应被解码。因此，如果服务器提供了压缩响应，Charles 将在传递给客户端之前对其进行解压缩，这通常不会产生任何影响。但是如果您已经构建了自己的客户端，或者客户端希望得到压缩响应，此时将会产生影响。使用 web 浏览器则没有任何影响。

#### Auto Save Settings(自动保存)

Auto Save 工具会按设定的时间间隔自动保存和清除记录会话。

如果您让 Charles 长时间监控网络活动，并希望将记录分解为可管理的单元，或者避免因数据量过大而可能出现的内存不足情况，这将非常有用。

输入以分钟为单位的保存间隔以及保存会话文件的目录。您可以选择是否在每次运行 Charles 时启动 `Auto Save` 工具，否则在 Charles 启动时将始终禁用 `Auto Save` 工具。

会话文件的名称中保存时间戳，格式为 `yyyyMMddHHmm`，即年月日时分，以便按字母顺序排序时，它们以正确的顺序显示。

#### Client Process Settings(客户端进程)

Client Process 工具显示负责发出每个请求的本地客户端进程的名称。客户端进程通常是您的 Web 浏览器(例如 firefox.exe)，但客户端进程工具可以帮助您发现许多可能未知的 HTTP 客户端。

客户端进程名称显示在每个请求的 `Notes` 区域中。

如果您可以在 Charles 中看到不确定原始进程的请求，则客户端进程工具很有用。 它仅适用于在运行 Charles 的计算机上发出的请求。

在 Charles 接受每个连接之前，该工具将引入一个短暂的延迟。 延迟通常不明显或不显著。

##### 选定站点

可以为每个请求启用该工具，也可以仅为指定站点启用该工具。当用于选定的站点时，可以使用简单但功能强大的模式匹配将工具的效果限制为指定的主机和/或路径。

#### Compose(编辑修改)

Compose 工具允许在原有的请求基础上修改。

#### Repeat(重复)

Repeat 工具允许选择一个请求并重复它。Charles 将请求重新发送到服务器，并将响应显示为新请求。如果您正在进行后端更改并希望在浏览器(或其他客户机)中重复请求的情况下测试这些更改，那么这将非常有用。特别是如果重新创建请求需要花费一些精力，例如在游戏中获得分数，这将节省大量精力。

重复请求是在 Charles 内部完成的，因此无法在浏览器或其他客户端中查看响应，响应只能在 Charles 中查看。

#### Repeat Advanced(高级重复)

Repeat Advanced 工具扩展了 Repeat 工具，提供了迭代次数和并发数的选项。这对于负载测试非常有用。

#### Validate(验证)

Validate 工具允许 Charles 通过将它们发送到 W3C HTML 验证器、W3C CSS 验证器和 W3C Feed 验证器来验证记录的响应。

验证报告在 Charles 中显示，其中包含与响应源中相应行相关联的任何警告或错误（双击错误消息中的行号可以切换到源视图）。

因为 Charles 测试它记录的响应，所以它可以测试不易测试的场景，例如在提交表单后呈现错误消息。

##### 重新验证

验证后，可以从验证结果中选择响应并 `Repeat`，重复原始请求，然后重新验证结果。

#### Publish Gist(发布要点)

Publish Gist 工具可以将将所选请求和响应作为要点发布。默认情况下，这个要点将匿名发布，这意味着你将无法做到 删除它。可以在 `Tools` 菜单的 `Publish Gist Settings` 中授权 Charles 使用您的 GitHub 帐户进行发布。

#### Import/Export Settings(导入/导出)

Import/Export 工具允许导入/导出 Charles 的 `Proxy`、`Tools`、`Preferences` 等设置。

#### Profiles(配置)

Profiles 包含所有配置设置的完整副本。

每次更改当前设置时，系统都会更新当前活动的配置文件，当您更改活动配置文件时，所有设置都将恢复为上次使用该配置文件时的状态。

请注意，如果导入已保存的配置，则会覆盖当前配置文件的设置。建议使用导入/导出来备份或创建当前配置和配置文件的快照，以维护多个并行工作区。

## Charles 使用教程

### 通过 Charles 进行 PC 端抓包

Charles 会自动配置浏览器和工具的代理设置，所以说打开工具直接就已经是抓包状态了。只需要保证一下几点即可：

1. 确保 Charles 处于 Start Recording 状态。
2. 勾选 **Proxy | Windows Proxy** 和 **Proxy | Mozilla  FireFox Proxy**。

### 通过 Charles 进行移动端抓包

手机抓包的原理，和 PC 类似，手机通过把网络委托给 Charles 进行代理与服务端进行对话。具体步骤如下：

1. 使手机和电脑在一个局域网内，**不一定非要是一个 IP 段，只要是在同一个路由器下即可**。
2. 电脑端配置：
   - 关掉电脑端的防火墙（这点很重要）。
   - 打开 Charles 的代理功能：通过主菜单打开 **Proxy | Proxy Settings** 弹窗，填入代理端口(端口默认为 `8888`，不用修改)，勾选 `Enable transparent HTTP proxying`。
   - 如果不需要抓取电脑上的请求，可以取消勾选 **Proxy | Windows Proxy** 和 **Proxy | Mozilla  FireFox Proxy**。
3. 手机端配置：
   - 通过 Charles 的主菜单 **Help | Local IP Address** 或者通过命令行工具输入 `ipconfig` 查看本机的 IP 地址。
   - 设置代理：打开手机端的 WIFI 代理设置，输入电脑 IP 和 Charles 的代理端口。
4. 设置好之后，我们打开手机上的任意需要网络请求的程序，就可以看到 Charles 弹出手机请求连接的确认菜单（只有首次弹出），点击 **Allow** 即可完成设置。
5. 完成以上步骤，就可以进行抓包了。

### 通过 Charles 进行 HTTPS 抓包

HTTPS 的抓包需要在 HTTP 抓包基础上再进行设置。需要完成一下步骤：

1. 完成 HTTP 抓包配置。
2. 电脑端安装 Charles 证书：通过 Charles 的主菜单 **Help | SSL Proxying | Install Charles Root Certificate** 安装证书。
3. 设置 SSL 代理：通过主菜单打开 **Proxy | SSL Proxy Settings** 弹窗，勾选 `Enable SSL proxying`。
4. 移动端安装 Charles 证书：通过 Charles 的主菜单 **Help | SSL Proxying | Install Charles Root Certificate on a Mobile Device or Remote Browser** 安装证书。
5. 设置好之后，我们打开手机上的任意需要网络请求的程序，就可以看到 Charles 弹出手机请求连接的确认菜单（只有首次弹出），点击 **Allow** 即可完成设置。
6. 完成以上步骤，就可以进行 HTTPS 抓包了。


