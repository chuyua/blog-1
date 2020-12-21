---
title: "Cloudflare 免费CDN配置教程"
date: 2020-12-12
published: true
license: true
slug: Cloudflare
tags: ['Cloudflare', 'CDN']
cover_image: "./images/cloudflare-free-CDN.png"
canonical_url: false
description: "Cloudflare 免费CDN配置教程"
---

# CloudFlare 免费CDN配置教程

### 一、几个简单问题

1. 免费版CloudFlare 自定义ip需要使用第三方版本cfp（就是CloudFlare partener）后文使用cfp代替。这里推荐笨牛。 
2. 很明显自定义ip要使用非dns接入方式。但是官方版只支持dns接入，所以要使用第三方版本。
3. http://cdn.bnxb.com/ 本次教程使用的网站
   https://cf.tlo.xyz/ 稳定存在了很长时间，值得使用
   http://cf.github.ci/ freenom免费域名套CF的救星

#### 技术原理

Cloudflare默认不支持自选节点,访问时的速度基本看脸。而我们的思路就是使用一个第三方服务来选择各地最优秀的节点。
举个例子,当浏览器访问接入默认CF的域名时,是先去不知道在什么地方的某个CF节点,之后再去访问真实服务器。
访问第三方接入的域名时,是先去第三方接入的域名获取访问最快的CF节点,再去访问这个CF节点。这样可以避免国内用户访问到美国西海岸节点之类的惨剧发生。

### 二、详细教程

#### 视频教程
<video src="https://dl.linik.ml/E5/%E6%96%87%E6%A1%A3/Documents/%E5%A4%96%E9%93%BE/%E5%A6%82%E4%BD%95%E9%83%A8%E7%BD%B2CFP%E8%87%AA%E9%80%89%E8%8A%82%E7%82%B9%E7%9E%8E%E6%89%AF%E7%89%88.mp4" controls="controls" width="500" height="300">您的浏览器不支持播放该视频！</video>

[在线播放/下载地址](https://dl.linik.ml/E5/文档/Documents/外链/如何部署CFP自选节点瞎扯版.mp4?preview)

#### 1.注册CloudFlare和[笨牛](http://cdn.bnxb.com/)

这个应该不用详细解释了吧，大家都会。
注意笨牛注册时需要填写你的CloudFlare账户和密码

#### 2.添加网站

本站使用宝塔面板搭建了一个网站。
![](https://s3.ax1x.com/2020/12/17/r8NljS.png)
这里代指你自己的服务器

#### 3.使用笨牛接入域名。

如果已经接入了CF,请备份解析记录之后在CF删除域名,把DNS地址换到任何一家国内可靠的DNS解析商。
之后再去笨牛网使用CNAME方式接入你的域名。

[](https://s3.ax1x.com/2020/12/17/r8Nd3V.png)![](https://s3.ax1x.com/2020/12/17/r8Ng41.png)这里回源地址填写你网站ip![](https://s3.ax1x.com/2020/12/17/r8NoHH.png)这是添加完成后的解析页面

#### 4.在DNS解析服务商添加A记录或者cname记录，接入cf。

在这里选择使用CNAME接入，记录值为cdn.linil.ml
![](https://s1.ax1x.com/2020/07/13/UJUMp4.png)

设置之后每次想要添加解析时,请先去DNS解析服务商处添加CNAME解析,值为cdn.linil.ml,再去笨牛网添加同样子域名的解析,解析到你的目标地址。
可以使用[测速网站](https://www.ce8.com/)检测一下解析出的IP地址,大于2且域名可以正常访问则说明接入成功。
cf免费版确实只提供两个节点，若是想更多只能自己添加了。

#### 5.使用https

默认免费cf提供免费的ssl证书，源站一般要求也是加密的，也使用https回源，具体是否支持http回源，我没仔细验证。这样的情况下，有一种简单办法。
1.源站不配置证书使用CF免费证书

![](https://s3.ax1x.com/2020/12/17/r8UBGt.png)

点击SSL验证查看验证状态

![](https://s1.ax1x.com/2020/07/16/UBBYZV.png)

然后返回设置为全程加密
![](https://s3.ax1x.com/2020/12/17/r8UWIs.png)

把验证方式改成txt就好然后添加对应txt解析 我这里已经添加好了就不再演示了

**文末福利**

http://cf.github.ci/ freenom免费域名套CF的救星的简单教程

1.登录http://cf.github.ci/

2.添加域名

![](https://s1.ax1x.com/2020/07/13/UJUX34.png)

3.添加解析

![](https://s1.ax1x.com/2020/07/13/UJar24.png)

4.修改解析

简单暴力删除域名重写添加即可
