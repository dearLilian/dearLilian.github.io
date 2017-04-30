---
layout: post
title: linux下的svn客户端安装配置
date: 2017-04-16
tags: linux
---



目录

* TOC 
{:toc}

## svn客户端安装配置

参考：https://jingyan.baidu.com/article/3c343ff7039de20d37796306.html

### apr安装

- 下载，进入http://apr.apache.org/download.cgi，下载最新apr。
- 解压。

命令行

```shell
tar xfvz 文件名
```

或者右击extract here。

- 新建安装目录。假如整个svn及其包含的内容都安装在```/usr/local/svnapp```

```shell
sudo mkdir /usr/local/svnapp
sudo mkdir /usr/local/svnapp/apr
```

- 进入解压后的目录。

```shell
sudo ./configure --prefix=/usr/local/svnapp/apr
make
sudo make test
sudo make install
```

### apr-util安装

- 下载，进入http://apr.apache.org/download.cgi，下载最新apr-util。
- 解压。

命令行

```shell
tar xfvz 文件名
```

或者右击extract here。

- 新建安装目录

```shell
sudo mkdir /usr/local/svnapp/apr-util
```

- 进入解压后的目录，这里prefix是指定安装目录，with-apr是指定apr的安装目录。

```shell
sudo ./configure --prefix=/usr/local/svnapp/apr-util --with-apr=/usr/local/svnapp/apr/
make
sudo make test
sudo make install
```

### 安装sqlite

- 下载：http://www.sqlite.org/2017/sqlite-autoconf-3180000.tar.gz
- 解压
- 新建安装目录

```shell
sudo mkdir /usr/local/svnapp/sqlite
```

- 进入解压后的目录，安装，可以在下面命令前加上sudo，如果你的安装目录有权限要求的话。

```shell
sudo ./configure --prefix=/usr/local/svnapp/sqlite
sudo make
sudo make install
```
### 安装zlib

- 下载：http://www.zlib.net/zlib-1.2.11.tar.gz

- 解压

- 新建安装目录

```shell
sudo mkdir /usr/local/svnapp/zlib
```

- 进入解压后的目录，安装

```shell
sudo ./configure --prefix=/usr/local/svnapp/zlib
sudo make
sudo make install
```

### 安装svn

- 下载：http://apache.fayea.com/subversion/subversion-1.9.5.tar.bz2

- 解压

- 新建安装目录

```shell
sudo mkdir /usr/local/svnapp/svn
```

- 进入解压后的目录，安装。

```shell
sudo ./configure --prefix=/usr/local/svnapp/svn --with-apr=/usr/local/svnapp/apr --with-apr-util=/usr/local/svnapp/apr-util --with-sqlite=/usr/local/svnapp/sqlite --with-zlib=/usr/local/svnapp/zlib
sudo make
sudo make install
```
### 环境变量配置

加入svn path

命令：

```shell
sudo gedit /etc/profile
```

在profile文件末添加，

```sh
PATH=/usr/local/svnapp/svn/bin:$PATH
export PATH
```
保存并关闭，使得改变生效：

```shell
source /etc/profile
```

结束。

## linux下svn的使用

参考：http://www.cnblogs.com/xulb597/archive/2012/07/02/2573575.html


### 将文件checkout到本地目录

从目标地址checkout出文件。比如地址是svn://121.49.110.54/dm

```shell
svn co svn://121.49.110.54/dm /home/svn/
```

其中```svn://121.49.110.54/dm```是源地址，```/home/svn/```是你本地的目标路径。

### 在版本库中新建文件夹

```shell
svn mkdir /home/wenbao/svn/network/liwenbao
```

这里要注意， 此时/home/wenbao/svn/network是一个working copy。

所以可以在她下面再创建目录liwenbao。


### 往版本库中添加新的文件

接上一个，我们在liwenbao文件夹下本地创建一个test.txt文件。

然后命令：

```shell
svn add /home/wenbao/svn/network/liwenbao/test.txt
```

这样就把该文件加入版本库中了。但是这还是本地的情况。我们还需要提交到服务端。

### 将改动的文件提交到版本库

```shell
svn commit -m "LogMessage" /home/wenbao/svn/network/liwenbao/test.txt
```

简写为```svn ci```


网速太差，每次都提交不动。



## linux下安装Rapidsvn来管理svn

参考：[Ubuntu 16.04下安装RapidSVN版本控制器及配置](http://www.linuxidc.com/Linux/2017-03/142300.htm)