---
layout:     post
title:      "Windows 本地 jekyll 环境配置"
subtitle:   " \"搭建 githubpages 本地预览环境\""
date:       2017-03-12 14:30:00
author:     "TechJene"
header-img: "img/2017/post-jekyll-config.jpg"
catalog: true
tags:
    - jekyll
    - 入门
---
> "但愿君心似我心。"

**说明**  
基于 Windows 8.1 系统。

### 前言

其实，按照[ githubpages ](https://pages.github.com/)的指示是完全可以完成安装的。

若需阅读官方指南，请移步：[ Learn how to set up Jekyll ](https://jekyllrb.com/docs/quickstart/)。


我只把官方指南中需要在 Windows 下配置的过程分拣出来。

### 第一步：安装 Ruby

1. 打开[ Ruby Installer for Windows ](http://rubyinstaller.org/downloads/)按需下载。

2. 点击 rubyinstaller-xxx.exe 安装包进行安装  
  有两点需要注意：
  * 安装路径，最好不要有空格
  * 勾选第二项，将 Ruby 执行加入 PATH  
  ![](/img/2017/post-jekyll-ruby.png)  
  点击 Install 完成安装  

3. 验证是否安装成功(非必要)
  打开命令行，输入 ruby -v  
  ``  ruby -v``   
  示例输出：  
  ``ruby 2.3.3p222 (2016-11-21 revision 56859) [x64-mingw32]
  ``

### 第二步：安装 RubyGems

1. 打开 https://rubygems.org/pages/download 按需下载

2. 解压到某个路径下，比如 D 盘

3. 管理员模式运行命令行，切换至解压目录(注意切换到rubygems目录内)，运行如下命令进行安装  
  ``ruby setup.rb``  

4. 命令行下输入 gem -v 验证安装  
  若返回版本号，则正常安装。

### 第三步：安装 Jekyll

1. 依然是在命令行下输入：  
  ``gem install jekyll``  
  安装完成会提示 Successfully installed jekyll-xxx......

2. 可使用 jekyll -v 进行验证，正常会返回 jekyll + 版本号。

### 第四步：启动 Jekyll 预览本地网页

1. 切换到个人博客所在的仓库目录

2. 输入 jekyll --help 查看最新的 Serve your site locally 命令  
  目前(2017.03.11)是：
  >  serve, server, s

  所以输入  
  ``jekyll s``  
  即可启动本地预览。

3. 打开浏览器，输入 http://localhost:4000/ ，然后 enjoy 。

### 我的建议

网上真的有好多教程，我也去看了好多，但是因为时间的原因，我感觉都不太适合了，所以还是选择了参考官方指南。  

同样的，我的这篇指南也是有时效性的，请您务必以官网说明为准。

---------
> 愿你我都是有态度的人，相识于有温度的文字中。

最后，感谢阅读。
