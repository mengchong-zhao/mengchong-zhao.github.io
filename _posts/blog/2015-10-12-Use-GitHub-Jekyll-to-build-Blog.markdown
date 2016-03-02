---
layout: post
title:  "Use GitHub Jekyll to build Blog"
date:   2015-10-12 14:51:11
categories: blog
---

**使用GitHub和Jekyll构建一个属于自己的博客**
----------
# 前言 #
也曾经写过技术博客，但内心深处总感觉在CSDN上写写画画并非一个专业程序猿所为。在网上看到这样一句话，作为题引分享给大家：
“阮一峰说，喜欢写博客的人，会经历三个阶段：

  第一阶段，刚接触Blog，觉得很新鲜，试着选择一个免费空间来写。  

  第二阶段，发现免费空间限制太多，就自己购买域名和空间，搭建独立博客。 

第三阶段，觉得独立博客的管理太麻烦，最好在保留控制权的前提下，让别人来管，自己只负责写文章。”
	
  以下介绍在Windows环境下利用Github+Jekyll搭建一个博客：
# 环境搭建 #
## 注册GitHub ##
- GitHub是一个基于Git的代码仓管理平台；打开官网[https://github.com/](https://github.com/)，注册即可。注册成功后，在主页的右下方会看到创建Git仓的标示

![](http://i.imgur.com/J9TsyZr.jpg)

- 在GitHub上创建一个仓库，名称为*username*.github.io,如下图所示

![](http://i.imgur.com/ZxLVz4i.jpg)

- 使用Git命令将仓拉到本地（Windows系统的前提是安装了Git Bash）	

(1)  将代码库克隆到本地 git clone https://github.com/*username*/*username*.github.io.git

(2)  查看当前仓库状态和所处分支情况，分别用 git status 和 git branch查看，可以看到我们当前在master分支上；

至此，我们在GitHub上要操作的就结束了

## 搭建Jekyll ##
Windows环境中搭建Jekyll较繁琐，网上看到一种可以直接安装的，没有测试，给出网址供大家使用：
[http://blog.csdn.net/u012844814/article/details/28869997](http://blog.csdn.net/u012844814/article/details/28869997)

以下是本人所使用的方法，虽然繁琐，可以让我们更多的了解Jekyll；

- 安装Ruby

从Ruby官网[RubyInstallers](http://rubyinstaller.org/downloads)下载一个 Ruby 安装包，我选择的是“Ruby 2.2.4 (x64)”。

安装的时候注意勾选“Add Ruby executables to your PATH”，设置环境变量，这样一来，你将能在 Windows 命令行直接使用 Ruby 的相关命令。

![](http://i.imgur.com/jN2s0uf.jpg)

- 安装 Ruby DevKit

除了Ruby,Jkeyll还需要依赖Ruby DevKit，同样在[官网](http://rubyinstaller.org/downloads)上下载相应的版本，这里下载的是DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe

这是一个压缩包， 为它建个目录（永久）并解压进去，例如 C:\RubyDevKit，进入此目录并初始化。

	cd C:\RubyDevKit
	ruby dk.rb init
若它不能自动获取 Ruby 目录时，需编辑其目录下的 config.yml 文件手动照葫芦画飘在后面加上

	-C:/Ruby22-x64
最后安装 DevKit

	ruby dk.rb install

- 安装Jekyll

Windows上的安装跟Linux一样简单，只需要在命令行输入以下命令：

	gem install jekyll
等待安装后，你就可以使用 Jekyll，使用 jekyll new 命令即可简单生成一个默认的博客，例如

	jekyll new blog
如下图所示

![](http://i.imgur.com/qCPo7PO.jpg)         ![](http://i.imgur.com/LY6SjW6.jpg)

这样就在c盘目录下创建了一个Jkeyll格式的blog模板文件，后续我们会对Jekyll进行介绍。

## 选择模板 ##
到这里，我们已经顺利搭建后Jekyll环境，接下来就是选择一个喜欢的博客模板（上面我们通过Jekyll命令也创建过一个blog,只不过这个模板很简单）；常用的模板有：[jekyllthemes.org](http://jekyllthemes.org/)

我选择的是Sleek Blog，打开该demo的git地址，将工程clone到本地，如下：

	git clone https://github.com/bawn92/sleek_blog.git	

在本地看到这个工程的目录（是不是跟Jekyll new出来的blog工程结构一致）：

![](http://i.imgur.com/c6K6Xiq.jpg)

将这些文件全部拷贝到你在GitHub上创建的工程仓库目录下（通常还需要对其中的_config.yml配置文件进行修改，Sleek Blog模板中只需要将其中的name改成自己的username即可），将文件提交到远程仓，命令如下：

	git add -A
	git commit -m "Initialize the repository"
    git push origin master

查看GitHub上的工程是否更新，如果更新，访问username.github.io就可以看到你的博客首页了。

## 如何写第一篇博客 ##
在介绍如何创建第一篇博客前，先对Jekyll做一个简单的介绍：
### 什么是Jekyll ###
Jekyll 的核心其实是一个文本转换引擎。它的概念其实就是： 你用你最喜欢的标记语言来写文章，可以是 Markdown，也可以是 Textile,或者就是简单的 HTML, 然后 Jekyll 就会帮你套入一个或一系列的布局中。在整个过程中你可以设置URL路径, 你的文本在布局中的显示样式等等。这些都可以通过纯文本编辑来实现，最终生成的静态页面就是你的成品了。

### Jekyll目录结构 ###
![](http://i.imgur.com/EgXfll2.jpg)

_config.yml:保存配置数据

_drafts:创建的草稿文件，用于存放尚未完成的博客

_includes:存放页面片段，即页头（head.html）、页脚（footer.html）、导航（navigation.html）、评论（disqus_comments.html）等，这些资源通过标签添加到index.html中，从而形成一个完整的页面。

_layouts:存放模板文件，包括文章模板，首页模块等

_posts:存放博客文章的文件。并且文章文件名称要符合YEAR-MONTH-DAY-title.MARKUP格式

_site:经过Jekyll转换的页面

_index.html:网站首页

_other files:其它的文件，存放css,js,image等

### Jekyll的加载流程 ###
- 首先会加载_posts及文件夹下的所有文章，将其参数和文章内容组织保存在内存中，所有的文章的内容、参数都在site.posts对象（其他文件夹下的文章不会放入site.posts中）。

- 其次加载_layouts文件夹下的所有模板。

- 再次加载_includes文件夹下的所有需要被引入的内容。

- 最后根据每一篇需要编译的文章选择的其参数定义的模板来创建一个模板，并将当前文章的内容、参数等进行扩展后放在page对象、content对象中，然后进行模板的编译，生成html文件，并按照一定规则放在_site文件夹下。也就是说在创建一篇文章时，其实所有文章的内容都已经被读取出来了，这也为文章相互之间的关联提供了可能。

### 结合Sleek Blog模块了解下Jekyll ###

打开Sleek Blog工程，_layouts文件下的post.html文件，如下图：

![](http://i.imgur.com/wzMTxZZ.jpg)

其对应的是博客首页的这个部分：

![](http://i.imgur.com/vJqy2dh.jpg)

对照着分析下：
Jekyll工程先加载的是_posts下的博客文件，存在site.posts中，这里对_post下的文件进行了分类，分成了blog和portfolio，文件具体属于哪一类，（这里以md文件为例）需要看文件头部的yml

![](http://i.imgur.com/DURbxnu.jpg)

post.html中的代码可以解读为，遍历site.posts中，类型属于blog的文件，分别按照for语句块中的格式加载在页面上。并且这里限定了，在首页的博客部分，最多执行for循环的次数是6，也就是首页上，博客区最多呈现6篇博客标题。
更详细的Jekyll学习解读，参考：[Jekyll基础](https://alfred-sun.github.io/blog/2015/01/10/jekyll-liquid-syntax-documentation/)

关于如何编辑博客，这里推荐一款好用的文本编辑器，Markdownpad2。