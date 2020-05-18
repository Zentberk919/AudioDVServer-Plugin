<div align="center"><h1>ADV-Plugin</h1></div>

<div align="center"><img src="https://github.com/Mashiro-Sorata/ADV-Plugin/blob/master/Image/ADV_demo.png?raw=true"></div>
<div align="center">Powered By <a href="http://mashirosorata.vicp.io">Mashiro_Sorata</a></div>

---

## 目录
1. [简介](#u1)
2. [下载](#u2)
3. [安装](#u3)
4. [使用说明](#u4)
5. [开发接口/API](#u5)
6. [更多](#u6)
7. [License](#u7)

---

<h2 id="u1">简介</h2>

`ADV-Plugin`是[SAO Utils](http://sao.gpbeta.com/)的第三方插件，可以提供系统音频数据的可视化服务。安装启用插件后，仅需用`SAO Utils`的“桌面网页挂件”打开ADV网页客户端即可显示系统音频频谱。

---

<h2 id="u2">下载</h2>

下载最新版本的插件：[ADV_Plug-in.zip](https://github.com/Mashiro-Sorata/ADV-Plugin/releases/latest)，将下载的 `ADV_Plug-in.zip` 压缩文件解压。
```html
文件夹结构如下
│  readme.txt
│
├─ADV_Client
│      adv.js
│      index.html
│
└─AudioDVServer
        advConfig.ini
        module64.dll
```

---

<h2 id="u3">安装</h2>

将解压缩根目录下的`AudioDVServer`文件夹拷贝至SAO Utils根目录的`Plugins`文件夹中，重启SAO即可。

---

<h2 id="u4">使用说明</h2>

### 启用插件
安装完成后打开`SAO Utils`首选项中的插件管理页面，将名称为`AudioDVServer`的插件选择启用后点击保存。

### 插件配置
安装完成后打开`SAO Utils`首选项中的插件管理页面，将名称为`AudioDVServer`的插件选择启用后点击保存。

通过更改`AudioDVServer`文件夹中的`advConfig.ini`文件来配置插件。当配置数据错误或无配置文件时使用默认值，配置值不区分大小写。
- ip：可选，默认值为`127.0.0.1`，可更改为`any`，指代地址`0.0.0.0`。只支持`any`与默认参数`local`，定义插件提供服务的地址。
- port：可选，默认值为`5050`，定义插件提供服务的端口号。
- maxClient：可选，默认值为`5`，定义客户端最大连接数。

`advConfig.ini` 文件示例：
```ini
[Server]
ip = local
port = 5050
maxClient = 4
```

### 客户端配置
压缩包内提供了一个频谱显示客户端的示例，可用SAO Utils桌面网页挂件打开。通过设置`ADV_Client`文件夹内的`index.html`文件来配置地址，端口号以及显示频谱的样式。必须保证客户端与插件设置的地址与端口号一致。示例文件已配置好，可以直接使用。也可通过编写HTML文件来定义自己的频谱显示客户端。

---

<h2 id="u5">开发接口/API</h2>
`ADV_Client`文件夹内的`adv.js`封装了一个`ADV_Plugin`类，并提供了一个`ondata()`接口方便数据的引用。

引用方法：
```javascript
var adv = new ADV_Plugin("ANY",5050);
adv.ondata = function(audioData){ //do something with audioData...};
```

每当客户端收到插件发送的频谱数据就会触发`ondata`事件。
其中`audioData`是数据长度为`128`的数组，前面`64`个数据为左声道FFT数据，后面`64`个数据为右声道FFT数据。每一个声道的FFT数据位从低到高对应频谱频率的由低到高。

---

<h2 id="u6">更多</h2>

我博客的[文章](http://mashirosorata.vicp.io/ADV-Plugin%E2%80%94%E2%80%94SAO%20Utils%E9%9F%B3%E9%A2%91%E5%8F%AF%E8%A7%86%E5%8C%96%E6%8F%92%E4%BB%B6.html)和这个`README`的内容上大致相同，但说明了这个项目的由来与实现，有兴趣的可以看一下。

---

<h2 id="u7">License</h2>

[MIT LICENSE](https://github.com/Mashiro-Sorata/ADV-Plugin/blob/master/LICENSE)
