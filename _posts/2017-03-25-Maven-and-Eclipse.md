---
layout: post
title: Eclipse 与 Maven
date: 2017-03-25
tag: 工具
---


* TOC 
{:toc}

### Maven是什么？

（以下内容摘自百度百科）

Maven项目对象模型(POM)，可以通过一小段描述信息来管理项目的构建，报告和文档的软件项目管理工具。

Maven 除了以程序构建能力为特色之外，还提供高级项目管理工具。
由于 Maven 的缺省构建规则有较高的可重用性，所以常常用两三行 Maven 构建脚本就可以构建简单的项目。
由于 Maven 的面向项目的方法，许多 Apache Jakarta 项目发文时使用 Maven，而且公司项目采用 Maven 的比例在持续增长。

Maven这个单词来自于意第绪语（犹太语），意为知识的积累，最初在Jakata Turbine项目中用来简化构建过程。
当时有一些项目（有各自Ant build文件），仅有细微的差别，而JAR文件都由CVS来维护。
于是希望有一种标准化的方式构建项目，一个清晰的方式定义项目的组成，一个容易的方式发布项目的信息，以及一种简单的方式在多个项目中共享JARs。 [1] 

### 安装Maven

- 教程：<a href="http://www.cnblogs.com/dzdwr3/p/6433563.html">Maven的安装配置以及Eclipse中Maven插件的安装和配置</a>(来自博客园)

- Maven下载地址：链接：http://pan.baidu.com/s/1bYiFwU 密码：khrm，安装方法及环境配置参考上面教程。

- Maven For Eclipse离线安装下载地址：链接：http://pan.baidu.com/s/1bYiFwU 密码：khrm，下载后解压，将features文件夹和plugins文件夹复制到eclipse安装目录下（其实是和原来的合并）。然后重启
eclipse即可。

### 如何使用Maven

- 教程：<a href="http://www.cnblogs.com/dzdwr3/p/6433903.html">Eclipse中创建Maven Project通过pom.xml自动获取第三方jar包的方法 </a>(来自博客园)

- Maven的库地址：http://mvnrepository.com/

