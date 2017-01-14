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
