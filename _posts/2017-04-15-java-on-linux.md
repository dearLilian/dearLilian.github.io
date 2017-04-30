---
layout: post
title: linux下的java安装与配置
date: 2017-04-15
tag: linux
---

目录

* TOC 
{:toc}


## java安装与配置


### java安装

首先是下载jdk文件。假如已经下载得到```jdk-8u121-linux-x64.tar.gz```，存放在```Downloads```目录下。

```ctrl+alt+t```打开终端，进入```Downloads```目录。
命令为：

```shell
cd /home/Downloads

```

- 首先解压上述的文件，命令为

```shell
tar -xzvf jdk-8u121-linux-x64.tar.gz
```

此时当前目录下多了一个```jdk1.8.0-121```的文件夹。

- 创建java安装目录。我们将java安装在```/usr/local/java/```下。首先创建这样一个目录（```/usr/local/```是存在的，但是```java```不存在）。

命令为：

```shell
sudo mkdir /usr/local/java
```

- 将```jdk1.8.0-121```整个文件夹移动到```/usr/local/java/```里

命令为：

```shell
sudo mv jdk1.8.0-121 /usr/local/java
```

这里必须用```sudo```，因为```/usr/local/```文件夹是有权限保护的。


到这里，java其实已经安装好了。只需要我们配置她的路径了。


### java环境变量配置

首先从上述知道，java的安装路径为```/usr/local/java/jdk1.8.0-121/```

- 打开终端

- 打开```/etc/profile```文件。命令为：

```shell
sudo gedit /etc/profile
```

这里也可以用```vim``或者其他编辑器打开，权看个人喜好。也可以用下面介绍的sublime（命令为subl)打开。


在该文件最底部添加下面几行内容：

```sh
export JAVA_HOME=/usr/local/java/jdk1.8.0_121
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
```

请务必熟悉这个文件，因为你以后所有的环境变量配置都是在这里。后面我们来学习一点shell的知识后，再来解析下上面几句的意思。

保存并关闭文件。

- 使得命令生效，方法一是重启系统。方法二：直接命令行输入```source /etc/profile```。

- 测试java安装成功了没

打开终端，输入```java -version```，如果显示java的版本信息（比如我们安装的1.8.0-121）即表示安装成功。

- 进一步的测试。

新建一个简单的HelloWorld程序。

命令行输入：

```shell
gedit HelloWorld.java
```

在打开的文档中输入：

```java
public class HelloWorld

{
      //程序的主函数入门

      public static void main(String args[])

      {
           //输出打印字符语句

          System.out.println("HelloWorld...");

      }

}
```

保存并关闭文件。

编译HelloWorld.java，命令为：

```shell
javac HelloWorld.java
```

回车后，没有任何信息，同时当前目录已经多了一个```HelloWorld.class```文件，表示编译成功。


然后运行	HelloWorld，命令为：

```shell
java HelloWorld
```

结果显示

```shell
HelloWorld...
```

表示成功运行。


### 踩踩更健康的坑

有时候不知道为什么，配置为环境变量后，会出现编译可以通过，运行时候却找不到main class的问题。

由于不知道是哪里出了错，所以当前只能暴力解决，就是把之前装的删除，重新安装一遍，重新配一遍。
