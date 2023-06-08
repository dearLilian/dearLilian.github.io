---
layout: post
title: Jekyll个人博客构建之路
date: 2016-12-09 
tag: 博客
---


## 目录

* TOC 
{:toc}


- 本博客的搭建真是历经了千辛万苦啊。

### 参考博客

- <a href='http://baixin.io/2016/10/jekyll_tutorials1/'>Jekyll搭建个人博客</a>

### 说在前面的话

- 我们需要做很多事情。包括环境配置，账号注册，域名购买（不是必须）等。然而不要害怕。即使你现在什么都不懂也没关系。一开始我看到Jekyll搭建博客的相关内容时一度以为会很难，要学习很多新的东西。于是在我以8元的价格买了一个域名之并简单的链接到一个github页面后就不了了之了。直到昨天又萌生出了搭建博客的心思，才又重新搞起。好在，经过一天的瞎搞，弄出来了。

### 几个关键内容

- Jekyll
	- Ruby
	- DevKit
	- Pygments
	- Python
- Github
	- 账号
	- 客户端
- 域名
- 网站统计
	- 百度
	- google
- 多说评论系统

## 一步一步建立自己的小站

### 建立github

- 注册github。

- 建立仓库。仓库名为<用户名>.github.io，详细请参看该博客<a href="http://blog.csdn.net/renfufei/article/details/37725057/">github建立个人博客</a>

- 上述都是在github网页中操作。为了后续测试及更新博客的方便安装github客户端。（百度云盘地址：）

### 域名等设置

- 我是在<a href="https://sg.godaddy.com/zh/">Godaddy</a>网站购买。也可以去其他地方。注册用户，挑选合适的域名，付款（支付宝，比较方便）。然后需要域名空间绑定，找域名服务器管理商进行管理。时间久了我不记得自己的域名是用哪个服务商解析的了。解析过程百度吧。

### Windows上安装Jekyll

- 参考：<a href="http://blog.csdn.net/rainloving/article/details/45745491">Windows 上安装 Jekyll</a>。安装好Jekyll后。打开github客户端，登录。将之前建立的仓库clone到本地。例如我的：dearLilian.github.io， clone到d://lilian/下。就会看到d://lilian/下出现了一个名为dearLilian.github.io的文件夹。

### MacOs安装Jekyll

参考： <a href="https://jekyllrb.com/docs/installation/macos/">Mac安装Jekyll</a>

安装的时候可能会出现权限问题。可以用以下命令先设置当前用户的相关权限。

```shell
sudo chown -R $(whoami):admin /usr/local/* && sudo chmod -R g+rwx /usr/local/*
```

安装ruby3.1.3成功后，会出现：

```shell
>>> Successfully installed ruby 3.1.3 into /Users/lilianli/.rubies/ruby-3.1.3
```


```
echo "source $(brew --prefix)/opt/chruby/share/chruby/chruby.sh" >> ~/.bash_profile
echo "source $(brew --prefix)/opt/chruby/share/chruby/auto.sh" >> ~/.bash_profile
echo "chruby ruby-3.1.3" >> ~/.bash_profile # run 'chruby' to see actual version
````

然后记得执行下：


```shell
source ~/.bash_profile"
````

要不然一直没有生效。

这时候再执行

```shell
gem install jekyll
```

来安装jekyll。

成功后显示：

```
Done installing documentation for webrick, unicode-display_width, terminal-table, safe_yaml, rouge, forwardable-extended, pathutil, mercenary, liquid, kramdown, kramdown-parser-gfm, ffi, rb-inotify, rb-fsevent, listen, jekyll-watch, google-protobuf, sass-embedded, jekyll-sass-converter, concurrent-ruby, i18n, http_parser.rb, eventmachine, em-websocket, colorator, public_suffix, addressable, jekyll after 30 seconds
28 gems installed
```





### 网站评论与统计

- 首先是网站统计，你需要在<a href="http://tongji.baidu.com/web/register">百度统计</a>和<a href="https://www.google.com/analytics/">Google Analytics</a>注册账号，并提取相应的id（详细操作请baidu or google）例如我的baidu id为e572ae9801b3a18891f123796b889f77，google id为UA-88738012-1，后面会使用。
- 其次是网站的评论管理系统，在<a href="http://duoshuo.com/">多说</a>(点击我要安装)上注册账号，设置域名。比如我的是www.lilian.duoshuo.com。即多说的用户名为lilian（后面会用到）

### 选择博客模板

- 例如，我选择了<a href="https://github.com/leopardpan/leopardpan.github.io/">baixin</a>的博客模板。如果大家喜欢，可以将这个download下来。也可以去<a href="https://github.com/dearLilian/dearLilian.github.io/">我的github</a>上fork我的。

### 将模板修改为自己的博客

- 将上述模板下载后，解压。并将leopardpan.github.io-master里面的文件copy到dearLilian.github.io文件夹里。此时，如果你打开Jekyll服务，即：命令行模式输入

```shell
cd d://lilian/dearLilian.github.io
jekyll serve
```

最开始构建发现很多包都没有。jekyll server无法执行成功。需要安装依赖包。


在项目根目录执行：

```shell
bundle install
```

失败的情况下，试试：
````shell
gem install ffi -v '1.13.1' -- --with-cflags="-Wno-error=implicit-function-declaration"
```
gem install ffi -v '1.9.18' -- --with-cflags="-Wno-error=implicit-function-declaration"

试试了各种方法好像也不对。
但是等等，，最后很奇怪，也不知道咋修复这个问题了。


然后浏览器打开：localhost:4000，此时就能看到本地环境的博客内容了

那么现在来修改模板，呈现你的东西吧。（为了方便编辑各种格式的文件，建议事先安装sublime Text）

工作路径：```d://lilian/dearLilian.github.io```

#### 1、修改配置文件

首先打开```_config.yml```文件。(以我的该文件为例子)，原文件内容如下：

```markdown
# Basic
title: LILIAN
subtitle: 心灵之窗
description: 经过了这么多年，我们终于看清了自己
# 头像里面的标题
avatarTitle: dearLilian
# 头像里面的描述
avatarDesc: 数据挖掘 / 机器学习
url: "http://lilian.info"

# Comment
comment:
    # disqus: lilian
    duoshuo: lilian 

# Social
social:
    weibo: 2344041987
    github: dearLilian
    weixin: lwb116xhn
    #gsite: liliandreamworld
    csdn: lilianforever
    # twitter: 
    mail: liwenbao930116@gmail.com

# 百度统计 
# 使用博客模板请去掉或者更换 id 
baidu:
    id: e572ae9801b3a18891f123796b889f77

# Google Analytics
# 使用博客模板请去掉或者更换 id
ga:
    id: UA-88738012-1   
    host: auto  


# 《----------------- 上面的信息修改成你自己的 ---------------------------》
#
#
#  _post/ 下的文章更换成你自己的文章
#  帮忙star一下，感谢~😆 地址： https://github.com/dearLilian/dearLilian.github.io
#
#
# 《--------------- 下面的信息可以自行选择是否修改 ------------------------》


permalink: /:year/:month/:title/
# Format
highlighter: rouge

# supported colors: blue, green, purple, red, orange or slate. If you need clear, leave it empty.
cover_color: clear

# The blog button should not be removed.
blog_button:
    title: 博客主页

# Navigation buttons in the front page.s
nav:
    - {title: 所有文章, description: archive, url: '/archive'}   
    - {title: 标签, description: tags, url: '/tags'}
    - {title: 留言板, description: messages, url: '/messages'}   #这是我的模板新增的。如果你使用的是baixin的模板，则删除这一行
    - {title: 关于我, description: about, url: '/about'}      
    

# Pagination
gems: [jekyll-paginate,jekyll-sitemap]
paginate: 20
paginate_path: "page/:num/"
```

需要修改的项目包括：
- ```titile```:你的博客标题
- ```subtitle```:你的博客子标题
- ```description```:你的博客描述
- ```avatarTitle```：你的头像里的标题
- ```avatarDesc```：你的头像描述
- ```url```:改成你的域名
- ```comment```里的```duoshuo```:改成你的多说的用户名
- ```social```里面的
	- ```weibo```：你的微薄id（不是用户昵称）
	- ```github```：你的github用户名
	- ```mail```:你的邮箱
	- 其他的可以补充，没有的可以不写，将原文中的删除即可
- ```baidu```: ```id```：你的百度统计的id
- ```ga```: ```id```:你的Google Analytics的id

#### 2、修改域名配置文件```CNAME```

修改为你自己的域名：如```lilian.info```，如果没有直接清空（后面访问时，直接访问自己的github page即可）

#### 3、修改个人文件```about.md```

这里也应该修改为你自己的介绍。（要求会基本的markdown语法。）

#### 4、头像

如果你想使用自己的头像，那么请打开```images```文件夹，将你自己的头像图片放在该文件夹，并重命名为```avatar.jpg```。

#### 5、网站图标

如果你想使用自己的个性网站图标，同样的将你的图标图片放在该文件夹，并重命名为```favicon.png```。

#### 6、博客文章

最后就是你的博客内容。请打开```_posts```文件夹，可以把原来的文件都删除掉，然后编辑你自己的博客。例如：新建文件，编辑以下内容：

```markdown
---
layout: post
title: 我的第一篇博客
date: 2016-08-04 
tag: 博客
---

### 我的第一篇博客

今天我成功搭建好了我的个人博客。欢迎大家来围观。

```

这里面，你在新建博客时必须包含前6行的内容，其中```title```后写你自己的博客标题，```date```后写你自己的时间（但格式要保持一致），```tag```后写你自己的标签。后面的内容则是markdown语法的内容。
将上述文件保存，命名为：```2016-08-04-MyFirstBlog.md```。

此时重新启动jekyll服务

```shell
cd d://lilian/dearLilian.github.io
jekyll serve
```

然后打开```localhost:4000```，打开博客主页，就可以看到你刚刚发布的这篇博客了。


### 博客上线

之前的操作都是在本地，剩下最关键的一步啦。就是在github客户端将这些changes统统```commit```并sync到服务端。详细请查询github如何commit以及sync（客户端就点击几下就ok了）。用git shell的话使用如下命令：

```git
git commit -a
git push
```

当同步完成后，在浏览器输入你的域名，比如我的是：```lilian.info```，然后就能看到你的博客了。任何人都可以看到哦。

## 掉进过的那些坑

### 关于jekyll

- 在启动jekyll时候，由于gemfile中需要的gem没有安装好，或者有依赖的没有安装，总会报错。解决办法是在官网上查询好依赖关系，依次安装好。
- 其次，项目中所需要的gem必须都要在gemfile中声明好，否则启动服务失败。

### 关于github提交冲突的问题

- 发生冲突后，会发现冲突的文件会出现两种内容，当然会有一定的标志。这时候需要将你不需要的那个版本（以及冲突的那个标志）去掉。具体还需要去进一步学习github的相关内容。

## 后续学习

### 版本控制git

- 因为需要经常更新博客。而且不只在一个终端。所以要学习好git来更熟练的操作。

### markdown

- 博客的内容基本采用markdown编写，需要熟知markdown语法才能写出更美观的博客。

### HTML,CSS

- 觉得现在的模板太丑了？那你要学习怎么去设置及设计更符合你审美的博客外观。

### jekyll,ruby

- 本博客是基于jekyll搭建的，然而到现在我还是不太知道jekyll到底是个啥。同时jekyll是基于ruby的，哦，ruby我知道是个编程语言。然而不知道怎么编，那还是去学习一下基本语法及常见应用场景吧。

### 搜索

- 我还想给自己的博客添加一个搜索功能。后续再想想怎么做吧。


## 结束语

由于我也是个菜鸟新手。所以如果大家有什么问题的话，可以email（liwenbao930116@gmail.com）我，请教谈不上，大家一起探讨。