---
layout: post
title: linux下shadowsocks客户端安装及配置
date: 2017-04-17
tags: linux
---



目录

* TOC 
{:toc}


## linux下使用shadowsocks进行科学上网


参考：<a href="http://blog.csdn.net/scythe666/article/details/52015213" target="_blank">http://blog.csdn.net/scythe666/article/details/52015213</a> 及<a href="http://www.linuxdiyf.com/linux/23584.html" target="_blank">http://www.linuxdiyf.com/linux/23584.html</a>

### 安装shadowsocks图形界面客户端

命令行：

```shell
sudo add-apt-repository ppa:hzwhuang/ss-qt5
sudo apt-get update
sudo apt-get install shadowsocks-qt5
```


### 获取shadowsocks免费账号

shadowsocks感觉用着还挺好的。但是是收费的，网上也有一些提供免费的，但是不稳定，或者要经常换密码之类的。

我在网上找到这个，[悠悠代理](http://www.uudaili.org/free.html)

可以根据自己的情况使用免费的或者收费的。获取:

- server
- server_port
- password
- method

下面的配置要使用。


### 配置shadowsocks客户端

首先假如已经有服务端账号了。


在你常用的文件夹下建立一个文件

```shell
gedit gui-config.json
```

在里面输入类似以下内容:

```json
{
"server":"11.22.33.44",
"server_port":50003,
"local_address":"127.0.0.1",
"local_port":1080,
"password":"123456",
"timeout":600,
"method":"aes-256-cfb"
}
```

保存退出。


打开shadowsocks。在快速启动上搜索shadowsocks可以找到。


点击connection->add->From config.json找到刚刚的json文件。

输入profile name，点击OK即可。然后在主界面此时已经有了这个新建代理了。

我们选中它，点击Connect即可。

经过上面的配置，你只是启动了sslocal。但是要上网你还需要配置下浏览器到指定到代理端口比如1080才可以正式上网。


### 配置终端Terminal

参考：http://www.linuxdiyf.com/linux/23584.html

终端下采用的是Privoxy，Privoxy是一款带过滤功能的代理服务器，针对HTTP、HTTPS协议。通过Privoxy的过滤功能，用户可以保护隐私、对网页内容进行过滤、管理cookies，以及拦阻各种广告等。Privoxy可以用作单机，也可以应用到多用户的网络。

#### 安装Privoxy

```shell
sudo apt-get install privoxy
```

#### 配置privoxy

```shell
sudo gedit /etc/privoxy/config
```

找到4.1. listen-address这一节，确认监听的端口号。

```shell
listen-address    localhost:8118
#
# 4.2. toggle
```

找到5.2. forward-socks4, forward-socks4a, forward-socks5 and forward-socks5t这一节，加上如下未注释的那一行配置```forward-socks5 / 127.0.0.1:1080 .```，注意最后的点号。

```shell
#        forward         192.168.*.*/     .
#        forward            10.*.*.*/     .
#        forward           127.*.*.*/     .
#
#      Unencrypted connections to systems in these address ranges
#      will be as (un)secure as the local network is, but the
#      alternative is that you can't reach the local network through
#      Privoxy at all. Of course this may actually be desired and
#      there is no reason to make these exceptions if you aren't sure
#      you need them.
#
#      If you also want to be able to reach servers in your local
#      network by using their names, you will need additional
#      exceptions that look like this:
#
#       forward           localhost/     .
forward-socks5 / 127.0.0.1:1080 .
#
#
#  5.3. forwarded-connect-retries
#  ===============================

```


#### 配置环境变量

```shell
sudo gedit /etc/profile
```

加入下面两句：

```shell
export http_proxy="127.0.0.1:8118"
export https_proxy="127.0.0.1:8118"
```

为了方便，设置开机启动，在```/etc/rc.local```中添加如下命令，注意在```exit 0```之前。

```shell
sudo sslocal -c /etc/
```


测试效果：

```shell
wget http://www.google.com
```

成功会在当前目录下生成index.html.1，不成功的话电脑重启一下。

### 配置firefox

在firefox中```preference->advanced->network->connection->settings```中选择```Manual proxy configuration```，设置```HTTP Proxy```:127.0.0.1 ```Port```: 8118