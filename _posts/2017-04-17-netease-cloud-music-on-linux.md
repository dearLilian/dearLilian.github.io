---
layout: post
title: linux下的安装网易云音乐
date: 2017-04-17
tags: linux
---



目录

* TOC 
{:toc}


## linux下的安装网易云音乐

参考：[http://blog.csdn.net/intellectualman/article/details/51803607](http://blog.csdn.net/intellectualman/article/details/51803607) 


### 下载网易云音乐安装包


- 下载：linux下的安装网易云音乐，[下载链接](http://music.163.com/#/download) 


### 安装依赖


- 命令行安装

```shell
sudo apt-get install libqt5x11extras5
```

或者直接

```shell
sudo dpkg -i netease-cloud-music.deb
```

会发现报错，我们使用依赖安装命令：

```shell
sudo apt-get -f install
```

### 安装网易云音乐

```shell
sudo dpkg -i netease-cloud-music.deb
```


感觉不能更棒啦哈哈。再也不担心听歌不方便啦。

