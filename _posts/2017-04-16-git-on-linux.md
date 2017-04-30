---
layout: post
title: linux下的git配置
date: 2017-04-16
tag: linux
---

 目录

* TOC 
{:toc}

## git配置

参考：http://www.cnblogs.com/sunada2005/archive/2013/06/06/3121098.html

### 为github账号添加ssh keys

命令：

```shell
ssh-keygen -t rsa -C "liwenbao930116@gmail.com"
```

然后系统提示输入文件保存位置等信息，连续敲三次回车即可，生成的ssh keys文件保存在```~/.ssh/id_rsa.pub```中

然后用文本编辑打开该文件，复制里面的内容。

登录你的github账号（如果没有，则自己创建个）

然后点击settings。点击SSH and GPG keys，添加一个新的ssh key，名字自己起，内容为刚刚复制的ssh内容。


完成后，验证：

```shell
ssh -T git@github.com
```

根据提示，输入yes。

结果显示

```txt
Hi dearLilian! You've successfully authenticated, but GitHub does not provide shell access.
```

dearLilian是我的github用户名。

表示配置成功。


### 从服务器clone project到本地

加入我现在要把我的博客的repository克隆到本地。

地址为：https://github.com/dearLilian/dearLilian.github.io

命令为：

```shell
git clone https://github.com/dearLilian/dearLilian.github.io.git
```

### 提交修改（例子）

```
$git clone https://github.com/username/Spoon-Knife.git
$cd Spoon-Knife
$git add filename.py 　　　　　　　　　　　　　　　　　　　　　　　　　#添加文件到版本库
$git commit -m 'add filename.py to src' 　　　　　　　　　　　　　　#提交，产生版本记录，注意代码依然在本地
$vim README.md　　　　　　　　　　　　　　　　　　　　　　　　　　　　　#修改Spoon-Knife中的README.md文件内容
$git commit -m 'modify the README.md' 　　　　　　　　　　　　　  　#提交，产生版本记录，注意代码依然在本地
$git [remote] rm filename1.py　　　　　　　　　　　　　　　　　　　　#删除repo中的filename1.py文件
$git commit -m 'delete filename1.py' 　　　　　　　　　　　　　 　 　#提交，产生版本记录，注意代码依然在本地
$git push origin 　　　　　　　　　　　　　　　　　　　　　　　　　　　 #将修改提交到github上

```
