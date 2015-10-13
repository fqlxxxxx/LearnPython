为了安装 gitbook ,不得不安装node 和 npm, 本以为很简单的事情, 网上的教程写很简单, 目测半小时肯定能搞定. 但实际上遇到了N 多坑.

##从官网下载的Pkg,安装 node.js以及 npm 
安装node 和 npm 过程还好, 正常.
但是安装 gitbook 是出现了各种问题, 掉坑里, 爬上来, 又掉坑里, 不断折腾, 
终于一次尝试不知道怎么 gitbook 安装成功了, 
但是接下去执行 gitbook 命令的时候又出现各种错误, 
搜索实在无解, 搁着!

但是任务来了, 要安装disqus, 结果执行命令式也出错了, 又掉坑里了, 掉下去, 爬上来, 又掉下去, 又爬上来 … …
放弃!!!
重新安装 node 和 npm

##尝试通过 MacPorts 安装 node 
MacPorts是Mac 下的套件管理工具, 看着不错.
但是看到安装条件之一是需要安装 Xcode, 心凉了一半, 前段时间刚卸载了, 再安装怎么也得下载个两天, 自从之前的 Xghost事件, 不敢随便下载 Xcode.

##继续找方案, 发现了 Homebrew 
Homebrew 是套件OS X 上的不可获取的套件管理工具. 
Homebrew 的好处是:
* 命令行反馈的内容都是人话!! 能看懂大部分, 
* 而且还很贴心的给出下一步可能使用到的命令,
* 安装插件的时候还有进度提示,
* 居然还有中文版官网, 不过估计是用 Google 翻译的

后来了解到,还有以下好处:
* 可以通过 berw 安装很多 mac 上的 app 
* 对于极客来说省了很多安装 app 的步骤

Homebrew 官网: 

http://brew.sh (英文)

http://brew.sh/index_zh-cn.htmlx  (中文)

###开始重新安装 node 和 npm

####第0步安装 brew
安装homebrew,终端中输入
```
ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go/install)"
```
安装完以后, 可以使用doctor來测试brew是否可正常执行
```
brew doctor
```
提示我:刚才安装的 MacPorts 安装的有问题, 可能需要卸载掉,并且给出了卸载的路径和指令, 太贴心了, 确实刚才安装了一半因为没有 Xcode结果卡住了, 按照提示卸载了.

```
Warning: You have MacPorts or Fink installed:
  /opt/local/bin/port

This can cause trouble. You don't have to uninstall them, but you may want to
temporarily move them out of the way, e.g.

  sudo mv /opt/local ~/macports
  ```


####第1步安装 node和 npm
**需要注意:**一般安装node时,会同时安装npm, 因此最好选择同一个途径安装,如果之前通过其他途径安装了一部分,最好要清理干净后,再通过 brew 安装,否则后面升级也有会有问题.

一般來說node套件會預設裝在/usr/local/bin，所以請將以下的目錄都要砍掉

```
rm -rf /usr/local/bin/node
rm -rf /usr/local/bin/npm
rm -rf /usr/local/bin/node_modules
```

**安装 node**
```
brew install node
```

结果好像安装又出问题了:
```
==> Downloading https://homebrew.bintray.com/bottles/node-4.1.2.el_capitan.bottle.1.tar.gz
######################################################################## 100.0%
==> Pouring node-4.1.2.el_capitan.bottle.1.tar.gz
Error: The `brew link` step did not complete successfully
The formula built, but is not symlinked into /usr/local
Could not symlink share/doc/node/gdbinit
Target /usr/local/share/doc/node/gdbinit
already exists. You may want to remove it:
  rm '/usr/local/share/doc/node/gdbinit'

To force the link and overwrite all conflicting files:
  brew link --overwrite node

To list all files that would be deleted:
  brew link --overwrite --dry-run node

Possible conflicting files are:
/usr/local/share/doc/node/gdbinit
/usr/local/share/systemtap/tapset/node.stp
==> Caveats
Bash completion has been installed to:
  /usr/local/etc/bash_completion.d
==> Summary
🍺  /usr/local/Cellar/node/4.1.2: 2744 files, 36M
localhost:~ alex$ rm '/usr/local/share/doc/node/gdbinit'
override rw-rw-r--  root/wheel for /usr/local/share/doc/node/gdbinit? 
localhost:~ alex$ brew link --overwrite node
Linking /usr/local/Cellar/node/4.1.2... 
Error: Could not symlink share/doc/node/gdbinit
/usr/local/share/doc/node is not writable.
localhost:~ alex$ brew link --overwrite --dry-run node
Would remove:
/usr/local/share/doc/node/gdbinit
/usr/local/share/systemtap/tapset/node.stp
localhost:~ alex$ brew link --overwrite node
Linking /usr/local/Cellar/node/4.1.2... 
Error: Could not symlink share/doc/node/gdbinit
/usr/local/share/doc/node is not writable.
```
大概意思好像是没有和某个文件夹关联上, 不可写入, 执行了建议的命令, 但是好像无效.

然后doctor一下

```
brew doctor
```

发现反馈代码最后多了一个提示:

```
Warning: You have unlinked kegs in your Cellar
Leaving kegs unlinked can lead to build-trouble and cause brews that depend on
those kegs to fail to run properly once built. Run `brew link` on these:
    node
```
Google 了一下:` Run brew link on these:node `,从 stackoverflow上查到类似的解决方法:
[Can't brew link an unlinked keg](http://stackoverflow.com/questions/10868133/cant-brew-link-an-unlinked-keg)

分别执行:
```
brew cleanup
brew link node
```
终于解决了, 提示如下:
```
Linking /usr/local/Cellar/node/4.1.2... 7 symlinks created
```
查看版本号, 确认了node 和 npm 都已经安装成功
```
node -v
v4.1.2
npm -v
2.14.6
```
>参考资料:[Mac 重新安裝npm](http://iambigd.blogspot.com/2014/06/npm.html)

###第2步安装 gitbook
以为终于可以开心的安装 gitbook 了,结果遇到两个坑:
* npm 被屏蔽
* 还是需要安装 Xcode
* sudo 管理权权限安装 gitbook

####第1坑

通过 npm 安装 gitbook 
```
npm install gitbook -g
```
提示, 因为使用代理,所以连接不上npm 服务器, 无法安装gitbook

```
npm ERR! Darwin 15.0.0
npm ERR! argv "/usr/local/Cellar/node/4.1.2/bin/node" "/usr/local/bin/npm" "install" "gitbook" "-g"
npm ERR! node v4.1.2
npm ERR! npm  v2.14.6
npm ERR! code ECONNRESET

npm ERR! network tunneling socket could not be established, cause=connect ETIMEDOUT 42.120.63.172:8080
npm ERR! network This is most likely not a problem with npm itself
npm ERR! network and is related to network connectivity.
npm ERR! network In most cases you are behind a proxy or have bad network settings.
npm ERR! network 
npm ERR! network If you are behind a proxy, please make sure that the
npm ERR! network 'proxy' config is set properly.  See: 'npm help config'

npm ERR! Please include the following file with any support request:
npm ERR!     /Users/alex/npm-debug.log
```

**原因:**
网友[Way Lau](http://www.waylau.com/faster-npm/)的一篇博客分析道:npm 默认是从国外的源获取和下载包信息，不慢才怪，有时甚至被墙，导致无法正常安装软件。

**有3种方式解决:**

可以采用国内的 npm 镜像来解决网速慢的问题, 也可以配置代理。

这里以“淘宝 NPM 镜像”举例。淘宝 NPM 镜像这是一个完整 npmjs.org 镜像，你可以用此代替官方版本(只读)，同步频率目前为 10分钟 一次以保证尽量与官方服务同步，镜像地址为 registry.npm.taobao.org， 是从 registry.npmjs.org 进行全量同步的。

1. 配置代理
2. 安装 cnpm, cnpm 是 npm 中国镜像的 npm 客户端
3. 切换 npm 到中国镜像 cnpm

#####方法1
由于我选择的科学上网方式, 不知道具体的代理网络地址, 所以放弃了第一种方式. 但可以参考这两篇

[Is there a way to make npm install (the command) to work behind proxy?](http://stackoverflow.com/questions/7559648/is-there-a-way-to-make-npm-install-the-command-to-work-behind-proxy)

[如何给 NPM 设置代理](http://blog.csdn.net/cnbird2008/article/details/8442333)


#####方法2
我采用的这种方式, cnpm 是 npm 中国镜像的 npm 客户端，可以代替 npm。
先用 npm 安装 cnpm
```
npm install -g cnpm
```

#####方法3
设置国内的镜像为默认镜像源：
```
npm config set registry=http://registry.npm.taobao.org
```

####第2坑:

通过 cnpm 安装gitbook

```
cnpm install gitbook -g
```

提示没有找到 Xcode, 但是查了很多资料有的说只需要安装CommandLineTools 即可, 但也有人说从10.9开始就必须要安装 Xcode 才行, 得!!! 我还是下一个吧.
现在从 AppStore 下载还挺快.
```
xcode-select: error: tool 'xcodebuild' requires Xcode, but active developer directory '/Library/Developer/CommandLineTools' is a command line tools instance

xcode-select: error: tool 'xcodebuild' requires Xcode, but active developer directory '/Library/Developer/CommandLineTools' is a command line tools instance
```

安装后 Xcode 后再执行gitbook安装命令, 没有任何报错, 安装成功.

但是查询版本号的时候

```
gitbook -V
```

提示没有找到这个命令, 我晕!!!哪里姿势不对? 试了help 命令也一样的反馈.

```
-bash: gitbook: command not found
```

####第3坑:

原来需要管理员权限(sudo)下安装才行.....

```
sudo cnpm install gitbook -g
```
安装后查看版本号,看是否安装成功,结果提示:需要卸了 gitbook ,先安装 gitbook-cli
```
You need to install 'gitbook-cli' to have access to the gitbook command anywhere on your system.
If you've installed this package globally, you need to uninstall it.
>> Run 'npm uninstall -g gitbook' then 'npm install -g gitbook-cli'
```
按照指示执行卸载 gitbook
```
sudo cnpm uninstall gitbook -g
Password:
unbuild gitbook@2.4.2
```

再安装 gitbook-cli
```
sudo npm install -g gitbook-cli
```

终于成功安装了:
```
gitbook -V
0.3.6
```
**有2个问题一直想知道,但是没有去深究,:**
* gitbook-lic 和 gitbook 有什么区别?
* gitbook -V 和 gitbook versions 查出来的版本号为啥不一样?

**微信中一位同学做了解答:**

> gitbook -V

> 0.3.6

> 输出的是 gitbook-cli（GitBook command line interface）的版本



> gitbook versions

> 2.4.3

> 输出的是 gitbook-cli 当中已安装的 GitBook 的版本。


**还学到一些有用的通用性命令:**
1. gitbook help  

查看 gitbook 的帮助菜单, 可以查看 gitbook 的一些基本操作
```
  build [book] [output] 	 build a book
    --format 	 Format to build to (Default is website; Values are website, json, ebook)
    --log 	 Minimum log level to display (Default is info; Values are debug, info, warn, error, disabled)

  pdf [book] [output] 	 build a book to pdf
    --log 	 Minimum log level to display (Default is info; Values are debug, info, warn, error, disabled)

  epub [book] [output] 	 build a book to epub
    --log 	 Minimum log level to display (Default is info; Values are debug, info, warn, error, disabled)

  mobi [book] [output] 	 build a book to mobi
    --log 	 Minimum log level to display (Default is info; Values are debug, info, warn, error, disabled)

  serve [book] 	 Build then serve a gitbook from a directory
    --port 	 Port for server to listen on (Default is 4000)
    --lrport 	 Port for livereload server to listen on (Default is 35729)
    --watch 	 Enable/disable file watcher (Default is true)
    --format 	 Format to build to (Default is website; Values are website, json, ebook)
    --log 	 Minimum log level to display (Default is info; Values are debug, info, warn, error, disabled)

  install [book] 	 install plugins dependencies

  init [directory] 	 create files and folders based on contents of SUMMARY.md
  ```

2. gitbook 

可以查看到 gitbook 相关的配置操作和解释

```
  Usage: gitbook [options] [command]


  Commands:

    versions                          list installed versions
    versions:print                    print current version to use in the current directory
    versions:available                list available versions on NPM
    versions:install [version]        force install a specific version of gitbook
    versions:link [version] [folder]  link a version to a local folder
    versions:uninstall [version]      uninstall a specific version of gitbook
    help                              list commands for a specific version of gitbook
    *                                 run a command with a specific gitbook version

  Options:

    -h, --help               output usage information
    -V, --version            output the version number
    -v, --gitbook [version]  specify GitBook version to use
    -d, --debug              enable verbose error

```
这两个命令对npm 和 node 也同样有效.





** 一些关于brew操作命令 **

安装 node
$ brew install node

卸载
$ brew uninstall node

brew cleanup
brew link node
brew uninstall node
brew install node

参考资料: http://iambigd.blogspot.com/2014/06/npm.html

###感受

节后回来就开始安装 git , node , npm , gitbook , 玩玩没想到卡在node 和 npm上差不多一周的时间.

各种不顺利, 不过也有收获非常多:
* 为了解决问题, 逼迫自己阅读了大量的英文文档和解决方案
* 初步了解了终端中反馈的内容读法, 知道怎么看反馈信息, 如何可以搜索到对应错误的相关信息
* 接触到了不少命令行, 虽然还不能熟练应用
* 最重要的是有些时候竟然享受这样被虐的状态, 囧! 但如果两天内还解不出来兼职要崩溃
* 是否偏离学习 Python的巷道?不尽然,我觉得应该算是开始接触到真实的程序员工作环境和状态了吧
* 看到了国外的程序员如何在 stackoverflow 和 github 上讨论问题, 解决问题




