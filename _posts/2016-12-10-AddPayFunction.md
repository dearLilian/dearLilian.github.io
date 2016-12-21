---
layout: post
title: 在博客中添加打赏功能
date: 2016-12-10 
tag: 博客
---



## 目录

* TOC 
{:toc}



本文主要是介绍如何在你的博客中加入打赏功能（通过支付宝或者微信扫描）

### 二维码

首先获取你的微信收款码和支付宝收款码。分别命名为weipayimg.jpg和alipayimg.jpg

### 相关代码

<a href="https://github.com/dearLilian/dearLilian.github.io/blob/master/_includes/dashang.html">点击这里</a>,下载打赏的代码。像本博客，我将该代码dashang.html放在_include文件夹下，并在_layouts文件夹下的post.html中加入代码：

![](/images/posts/dse/dscode.png)

分析功能的代码，新建html文件，命名为：share.html，添加以下内容：

```html
<section>
  <div class="bdsharebuttonbox"><a href="#" class="bds_more" data-cmd="more"></a><a href="#" class="bds_qzone" data-cmd="qzone" title="分享到QQ空间"></a><a href="#" class="bds_tsina" data-cmd="tsina" title="分享到新浪微博"></a><a href="#" class="bds_tqq" data-cmd="tqq" title="分享到腾讯微博"></a><a href="#" class="bds_renren" data-cmd="renren" title="分享到人人网"></a><a href="#" class="bds_weixin" data-cmd="weixin" title="分享到微信"></a></div>
<script>window._bd_share_config={"common":{"bdSnsKey":{},"bdText":"","bdMini":"2","bdMiniList":false,"bdPic":"","bdStyle":"0","bdSize":"16"},"share":{},"image":{"viewList":["qzone","tsina","tqq","renren","weixin"],"viewText":"分享到：","viewSize":"16"},"selectShare":{"bdContainerClass":null,"bdSelectMiniList":["qzone","tsina","tqq","renren","weixin"]}};with(document)0[(getElementsByTagName('head')[0]||body).appendChild(createElement('script')).src='http://bdimg.share.baidu.com/static/api/js/share.js?v=89860593.js?cdnversion='+~(-new Date()/36e5)];</script>
</section>
```

<a href="https://github.com/dearLilian/dearLilian.github.io/blob/master/dsimg/">点击这里</a>,下载所有的图片。并将这些图片放在网站的根目录下的dsimg文件夹下。同时用你自己的微信和支付宝收款码图片替换原来的。


### 测试

最后进行测试，在每篇博客后面都有了一键分享和打赏，效果如下：


***********下面是图片*******************

![评论和打赏效果](/images/posts/dse/dse.png)

************上面是图片******************