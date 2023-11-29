---
layout: post
title: Github Pages自定义域名
categories: Other
description: Github Pages自定义域名
keywords: Github Pages,自定义域名
mermaid: false
sequence: false
flow: false
mathjax: false
mindmap: false
mindmap2: false
typora-root-url: ./..\..
---

# 1.购买域名

购买域名有很多网站，例如国内腾讯云、阿里云等，国外有 [Godady](https://www.godaddy.com/zh-sg)、[Namesilo](https://www.namesilo.com/)等

1. 先到购买域名的网站查一下想要的域名有没有被别人注册了。
2. 注意有些域名首年很便宜，之后就很贵。

# 2.DNS解析

以阿里云购买域名为例，购买完域名后，可以前往阿里云的[云解析DNS](https://wanwang.aliyun.com/domain/dns)配置DNS解析记录

- 进入云解析DNS->域名解析，添加我们购买的域名，如mwell.top
- 点击添加的域名，进入解析设置，点击添加记录

| 记录类型                  | 主机记录                                             | 记录值                          |
| ------------------------- | ---------------------------------------------------- | ------------------------------- |
| CNAME（即指向另一个域名） | 即域名前缀，如www等。你也可以选择写@，表示不带前缀。 | github地址(username.github.com) |

![](/images/other/20231128151841.png)

# 3.为Github Pages绑定域名

在Github Pages中，点击Settings->Pages->Custom domain，将我们注册的域名填进去即可。记得勾选`Enforce HTTPS`开启HTTPS。等待片刻后我们就可以使用自己的域名访问网站了。

![](/images/other/202311281510.png)

# 4.可能出现的错误

如果浏览器访问https://xxxx.com 之后发现样式出不来，控制台报错

> Mixed Content: The page at 'https://xxx.top/' was loaded over HTTPS, but requested an insecure script 'http://xxx.top/assets/vendor/jquery/dist/jquery.min.js'. This request has been blocked; the content must be served over HTTPS.

报错的的原因：查资料后发现原因是在https中请求http接口或引入http资源都会被直接blocked（阻止），浏览器默认此行为不安全，会拦截。

解决办法如下: 在 header.html文件的head中加入如下代码

````html
<meta http-equiv="Content-Security-Policy" content="upgrade-insecure-requests" />
````

