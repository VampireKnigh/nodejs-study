# nodejs-study

##nodejs开发环境配置
其实这过程特别简单:

先安装一个 [nvm](https://github.com/creationix/nvm)
```
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.25.2/install.sh | bash
```
nvm 的全称是 Node Version Manager，之所以需要这个工具，是因为 Node.js 的各种特性都没有稳定下来，所以我们经常由于老项目或尝新的原因，需要切换各种版本。

安装完成后，你的 shell 里面应该就有个 nvm 命令了，调用它试试
```
$ nvm
```
当看到有输出时，则 nvm 安装成功。

安装 Node.js

使用 nvm 的命令安装 Node.js 最新稳定版，现在是 v6.9.4
```
$ nvm install 6.9.4
```
或者直接使用以下命令直接安装
```
node install stable
```

安装完成后，查看一下
```
$ nvm ls
```
这时候可以看到自己安装的所有 Node.js 版本，输出应如下：



（图1）

那个绿色小箭头的意思就是现在正在使用的版本，我这里是 v6.9.4。我还安装了 v7.4.0，但它并非我当前使用的版本。

如果你那里没有出现绿色小箭头的话，告诉 nvm 你要使用7.4.0版本

$ nvm use 7.4.0
然后再次查看，这时候小箭头应该出现了。

OK，我们在终端中输入

$ node
REPL(read–eval–print loop) 应该就出来了，那我们就成功了。

随便敲两行命令玩玩吧。

比如 > while (true) {}，这时你的 CPU 应该会飚高。

完善安装

上述过程完成后，有时会出现，当开启一个新的 shell 窗口时，找不到 node 命令的情况。

这种情况一般来自两个原因

一、shell 不知道 nvm 的存在

二、nvm 已经存在，但是没有 default 的 Node.js 版本可用。

解决方式：

一、检查 ~/.profile 或者 ~/.bash_profile 中有没有这样两句

export NVM_DIR="/Users/YOURUSERNAME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm
没有的话，加进去。

这两句会在 bash 启动的时候被调用，然后注册 nvm 命令。

二、

调用

$ nvm ls

看看像不像上述图1中一样，有 default 的指向。

如果没有的话，执行

$ nvm alias default 0.12

再

$ nvm ls

看一下









#《一个最简单的 express 应用》

###**目标**

建立一个 lesson1 项目，在其中编写代码。当在浏览器中访问 http://localhost:3000/ 时，输出 Hello World。

###**挑战**

访问 http://localhost:3000/ 时，输出 你好，世界。

###**知识点**

包管理器 npm 。使用 npm 安装包，并自动安装所需依赖。
框架 express 。学习新建 express 实例，并定义 routes ，产生输出。
课程内容

按照惯例，我们来个 helloworld 入门。

####**包管理器 npm**

npm 可以自动管理包的依赖. 只需要安装你想要的包, 不必考虑这个包的依赖包.

在 PHP 中, 包管理使用的 Composer, python 中，包管理使用 easy_install 或者 pip，ruby 中我们使用 gem。而在 Node.js 中，对应就是 npm，npm 是 Node.js Package Manager 的意思。

####**框架 Express**

express 是 Node.js 应用最广泛的 web 框架，现在是 4.x 版本，它非常薄。跟 Rails 比起来，完全两个极端。

express 的官网是 http://expressjs.com/ ，我常常上去看它的 API。

首先我们需要得到一个 express。

不同于 ruby 的 gem 装在全局，Node.js 的依赖是以项目为单位管理的，直接就安装在项目的 node_modules 目录下，而且每个依赖都可以有指定版本的其他依赖，这些依赖像一棵树一样。根据我自己的使用经验来说，npm 的体验在 pip 和 gem 之上。
```
npm install express
```
安装完成后，我们的目录下应该会出现一个 node_modules 文件夹，ls 看看
```
$ ls node_modules
```
里面如果出现 express 文件夹则说明安装成功。

或者 npm命令提供更清晰直观的显示:
```
$ npm list
```
我们继续应用程序的编写。

新建一个 app.js 文件

copy 进去这些代码
```
// 这句的意思就是引入 `express` 模块，并将它赋予 `express` 这个变量等待使用。
var express = require('express');
// 调用 express 实例，它是一个函数，不带参数调用时，会返回一个 express 实例，将这个变量赋予 app 变量。
var app = express();

// app 本身有很多方法，其中包括最常用的 get、post、put/patch、delete，在这里我们调用其中的 get 方法，为我们的 `/` 路径指定一个 handler 函数。
// 这个 handler 函数会接收 req 和 res 两个对象，他们分别是请求的 request 和 response。
// request 中包含了浏览器传来的各种信息，比如 query 啊，body 啊，headers 啊之类的，都可以通过 req 对象访问到。
// res 对象，我们一般不从里面取信息，而是通过它来定制我们向浏览器输出的信息，比如 header 信息，比如想要向浏览器输出的内容。这里我们调用了它的 #send 方法，向浏览器输出一个字符串。
app.get('/', function (req, res) {
  res.send('Hello World');
});

// 定义好我们 app 的行为之后，让它监听本地的 3000 端口。这里的第二个函数是个回调函数，会在 listen 动作成功后执行，我们这里执行了一个命令行输出操作，告诉我们监听动作已完成。
app.listen(3000, function () {
  console.log('app is listening at port 3000');
});
```
执行

$ node app.js

这时候我们的 app 就跑起来了，终端中会输出 app is listening at port 3000。这时我们打开浏览器，访问 http://localhost:3000/，会出现 Hello World。如果没有出现的话，肯定是上述哪一步弄错了，自己调试一下。

##**补充知识**

在这个例子中，node代码监听了3000端口，用户通过访问http://localhost:3000/ 得到了内容，为什么呢？

###**端口**

端口的作用：通过端口来区分出同一电脑内不同应用或者进程，从而实现一条物理网线(通过分组交换技术-比如internet)同时链接多个程序 Port_(computer_networking)

端口号是一个 16位的 uint, 所以其范围为 1 to 65535 (对TCP来说, port 0 被保留，不能被使用. 对于UDP来说, source端的端口号是可选的， 为0时表示无端口).

app.listen(3000)，进程就被打标，电脑接收到的3000端口的网络消息就会被发送给我们启动的这个进程

###**URL**

RFC1738 定义的url格式笼统版本<scheme>:<scheme-specific-part>， scheme有我们很熟悉的http、https、ftp，以及著名的ed2k，thunder。

通常我们熟悉的url定义成这个样子

<scheme>://<user>:<password>@<host>:<port>/<url-path>
用过ftp的估计能体会这么长的，网页上很少带auth信息，所以就精简成这样:

<scheme>://<host>:<port>/<url-path>
在上面的例子中, scheme=http, host=localhost, port=3000, url-path=/, 再联想对照一下浏览器端window.location对象。 著名的localhost，你可以在电脑的hosts文件上找到

在这篇文章中提到： ```URI schemes are frequently and incorrectly referred to as "protocols", or specifically as URI protocols or URL protocols, since most were originally designed to be used with a particular protocol, and often have the same name```，比较认同这个观点，尤其是今天移动设备的时代里， android和ios的开发中大量使用uri作为跨app通讯通道，把scheme理解为协议略狭隘了。

###**尾声**

在了解完端口和url之后，再去看例子代码，相信应该好理解很多。 有必要的话，还可以在解刨一下express的use逻辑，对峙http.createServer，相信还有火花，:)
