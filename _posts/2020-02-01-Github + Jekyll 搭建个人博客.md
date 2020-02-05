---
layout: post
title: Github + Jekyll 搭建个人博客
subtitle: How Do I Make This Site
header-img: img/post/Github + Jekyll 搭建个人博客/bg.jpg
date: 2020.02.01 14:32:24
author: Price Wang
header-mask: 0.8
catalog: true
tags:
- 教程
- 前端
---

本文将详细介绍本站的搭建过程，包括 GitHub Pages 设置和部署，Jekyll 安装使用，功能模块整入，CDN 加速。欢迎大家 [star](https://github.com/PriceWang/blog) 本站源码改造成属于你的个人网站

本教程适用于 Window 10 平台

## GitHub Pages

搭建一个可外网访问的网站，需要将其部署到服务器上，我们可以利用 GitHub Pages 来实现。GitHub Pages 是 GitHub 提供的一个网页寄存服务，可以用于存放静态网页，免费且无限流量。一般 GitHub Pages 的网站使用 github.io 的子域名，但是也可以使用第三方域名，只要按照一定的格式要求，将网站源码上传至 GitHub 仓库，那么在任何时候任何地方就都能够访问了

#### 创建页面

首先我们要做的是新建 GitHub Pages 页面，详细步骤如下

> 在 GitHub 上新建一个仓库，仓库名称格式为：`用户名.github.io`（如：PriceWang.github.io）

![]({{ site.baseurl }}/img/post/{{ page.title }}/创建仓库.jpg "创建仓库")

浏览器里访问 https://用户名.github.io/，发现这个 url 可以被访问了，你可以把改仓库 Pull 到本地，然后新建一个 index.html 的文件，输入任意内容，再把文件推送到 GitHub 上，访问该链接，可以发现 index.html 里面的内容已经被成功部署到服务器上了

#### 自定义域名

现在，我们已经成功搭建了一个简单的网站并能够正常访问了，它的域名是 用户名.github.io，事实上，GitHub Pages 支持自定义域名，也就是说我们可以将其设置为自己的域名，你可以向各个域名服务商购买，我使用的是阿里云旗下的[万网](https://wanwang.aliyun.com/)，在国内购买的话需要备案和实名认证，完成后进行如下操作

> 在 CMD 中用命令 `ping 用户名.github.io` 找到存放你的 GitHub Pages 的主机的 IP 地址，下图中红框内的就是我们要找的 IP 地址

![]({{ site.baseurl }}/img/post/Github + Jekyll 搭建个人博客/Ping命令.jpg "Ping 命令")

> 在域名控制台选择解析并添加两条记录

![]({{ site.baseurl }}/img/post/{{ page.title }}/域名解析.jpg "域名控制台")

![]({{ site.baseurl }}/img/post/{{ page.title }}/记录.jpg "添加记录")

> 在 GitHub xxx.github.io 项目的设置页面中，滑动到下方，找到 GitHub Pages 这一栏，在 Custom Domain 填上刚刚添加解析的域名并保存

![]({{ site.baseurl }}/img/post/{{ page.title }}/自定义域名.jpg "自定义域名")

此时，已经可以使用自定义的域名访问 GitHub Pages 所提供的页面了

#### CDN 加速

由于众所周知的原因，GitHub Pages 在国内访问速度可能会非常慢，我们可以用 CDN 来加速，我使用的是 [CloudFlare CDN](https://www.cloudflare.com/) 加速页面访问

使用 CloudFlare CDN 有以下好处

* 免费且快速的DNS服务（1分钟生效）
* 免费的SSL证书
* 限制某些地区的IP访问等操作
* 防止网络攻击
* 网站缓存和加速
* 一个cloudflare账户免费绑定多个网站

## Jekyll

[Jekyll](https://jekyllrb.com/) 是一个简单的，可识别 Blog 的静态站点生成器，支持自定义地址、博客分类、页面、文章以及自定义的布局设计，使用 Markdown、Liquid 和 HTML & CSS 构建可发布的静态网站。我们可以通过 Jekyll 创建网站模板，实时修改模板里面的内容，并可以通过本地 url 预览改动后的效果。我们把这个 Blog 推送到上一步创建的代码仓库里，就可以访问到博客里面的内容了

> 下载并安装 [RubyInstaller](https://rubyinstaller.org/downloads/)

`注意`：Jekyll 暂不支持 Ruby 2.7，请下载 Ruby+Devkit 2.6.X 版本

> 下载并解压 [RubyGems](https://rubygems.org/pages/download)，CMD执行：ruby setup.rb

![]({{ site.baseurl }}/img/post/{{ page.title }}/安装ruby.jpg "安装ruby")

> CMD 执行：gem install jekyll

![]({{ site.baseurl }}/img/post/{{ page.title }}/安装jekyll.jpg "安装jekyll")

> 官网提供了大量[博客模板](http://jekyllthemes.org/)，我们可以去挑选一个自己喜欢的博客模板，然后在这个基础上修改成满足自己需求的博客，CMD 执行 jekyll server 后可以开启本地服务器

![]({{ site.baseurl }}/img/post/{{ page.title }}/本地服务器.jpg "本地服务器")

到此我们完成了 Jekyll 的安装并选定了一个博客主题模板。Jekyll 的语法规则和具体使用方法都可以在[官网](https://jekyllrb.com/)找到

## 功能模块

我们可以使用第三方应用来丰富我们的博客

#### 评论

Jekyll 可应用的评论系统有很多，在此介绍 Disqus 和 Valine

[Disqus](https://disqus.com/) 提供功能强大的第三评论系统，用户使用 Disqus，无需重复注册账号，只需使用 Disqus 账号或者第三方平台账号，即可方便的进行评论，且所有评论都会存储、保存在Disqus账号后台，方便随时查看、回顾。但由于众所周知的原因无法在国内使用

[Valine](https://valine.js.org/) 是一款基于 LeanCloud 的快速、简洁且高效的无后端评论系统。按照官网文档进行设置，我们可以轻易地在博文中添加评论功能

本站使用的是 Valine

如果遇到什么问题，欢迎留言