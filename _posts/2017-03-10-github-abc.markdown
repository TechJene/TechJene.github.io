---
layout:     post
title:      "Github 10 分钟入门"
subtitle:   " \"hello github\""
date:       2017-03-11 10:18:00
author:     "TechJene"
header-img: "img/2017/post-github-abc/github-abc.jpg"
catalog: true
tags:
    - github
    - 译文
    - 入门
---
> "千里之行，始于足下。"


### 说明

本文主要内容翻译自 [github 官网](https://guides.github.com/activities/hello-world/)。
有些词还是用的英语，个人学识浅薄，无法用中文表达出该有的味道。  
欢迎阅读，不足之处，还请指正，谢谢！

## 前言

本文以 *Hello World* 为例讲解。  
Hello World 在计算机编程中可谓是历史悠久。当你学习一些新事物的时候，通过简单的练习，可以很快上手。  
你将会学到：
* 如何创建并使用一个仓库 ( repository )
* 如何开始并且管理一个新的分支 ( branch )
* 如何修改文件并作为提交 ( commit ) 推送 ( push ) 到 GitHub
* 如何开启( open )和合并( merge ) 一次 pull request


## 简介

GitHub 是一个版本控制与协作的代码托管平台。通过使用 GitHub， 在任何地方，你都可以和其他人一起合作一个项目。

这篇指南会教你一些 GitHub 的要点，比如仓库 (repositories)、分支 (branches)、提交 (commits) 和获取请求 (Pull Requests)。你将会创建自己的 Hello World 仓库并且学到 GitHub 获取请求的工作流程：一种创建和审阅代码的流行方式。

**无需编程**  
首先，你需要一个[ GitHub.com ](https://github.com/)账号和有效的网络连接。你(暂时)不需要知道如何去写代码、使用命令行或者安装[ Git ](https://git-scm.com/)工具(基于 GitHub 的版本控制软件)。


### 第一步 ：创建仓库

一个仓库通常用于组织一个单独的工程( project )，仓库可以包含文件夹和文件、图片、视频、电子表格( spreadsheet )，还有数据集，总之是你工程需要的任何事物。 GitHub 建议工程包含一个 README 文件，或者一个关于你的工程信息的文件。 GitHub 上，在新建仓库的同时可以添加一份说明文档。它也提供了其他公共的选项，比如证书文件( license file )。  

你新建的 hello world 仓库可以作为你存放想法、资源的地方，你甚至可以和他人分享和讨论事情。  

#### 新建仓库  
1. 在右上角，你的头像( avatar ) 或者是ID的旁边，点击 ** + ** ，然后选择新建仓库( New repository )。

 ![](/img/2017/post-github-abc/github-new01.jpg)

2. 命名仓库为 hello-world ，或者任何你喜欢的名字，我命名为 Jene-hello-world 。

3. 可以写一个简短的介绍( description )。

4. 选择初始化( Initialize )仓库的同时带有 REANME 。

 ![](/img/2017/post-github-abc/github-new02.jpg)

最后，点击创建仓库即可。

### 第二步：创建分支( branch )  

创建分支可以保证在不同版本的仓库上工作。  
默认状态下，新建的仓库会有一个名为 master 的分支，master 被认为是一个确定( definitive )的分支，作为主分支。使用其他分支来测试和编辑，最终提交到主分支。

创建一个从 master 分离下来的分支，实际上就是对 master 做了一次复制，或者可以称为快照( snapshot )。  
当你在自己的分支上工作时，即使有人改变了主分支，你仍然可以提交自己的更新。

如下图所示：
* 一个是主分支( master )
* 一个叫 feature 的分支
* 分支 feature 在合并到主分支之前的过程  

![图片来自 GitHub ](https://guides.github.com/activities/hello-world/branching.png)

你或许做过这种事，一个文件保存了不同的版本。分支在 GitHub 仓库中达到的是同样的目的。

比如，在 GitHub 工作的开发者、作者、还有设计师通过使用分支来保证 bug 的修复和特殊的工作是分离于主分支的。只有当更改就绪之后，他们才合并到主分支。

下面是创建分支的步骤：
1. 打开刚刚新建的仓库。

2. 点击 ** Branch：master ** 的下拉按钮( drop down )。

3. 在文本框中写入分支的名字，比如 readme-edits 。

4. 选择**创建分支**或者直接敲击键盘上的 Enter 键。

  ![](/img/2017/post-github-abc/github-branch.jpg)

此时，仓库里就有了两个分支，主分支 master 和 分支 readme-edits 。它们现在是完全相同的。下一步就是在新分支中添加更改的内容。

### 第三步：更改并且提交

现在我们在分支 readme-edits 的代码界面，是主分支的副本( copy )。

在 GitHub 上，保存更改称为提交( commit )。每一次提交都有相关的提交信息，提交信息解释了做出的特定更改。提交信息可以获得( capture )更改的历史，以保证其他的提交者可以理解你所做的更改。

下面是更改和提交的步骤：
1. 点击 README.md 文件。

2. 点击右上角的编辑按钮(形状是笔的那个)。

 ![](/img/2017/post-github-abc/github-commit01.jpg)

3. 编辑状态下，可以写一下关于你自己的内容。

4. 为你的更改写一条提交信息。

5. 点击 ** Commit changes ** 按钮

 ![](/img/2017/post-github-abc/github-commit02.jpg)

 只是更改了分支 readme-edits 的 README 文件，所以现在这个分支包含了不同于主分支的内容。

** 第 6 行出现语法错误。已改为 want to ，希望不会误导大家。 **
### 第四步：开启一次获取请求( pull request )  

既然已经在分离于 master 的分支上有了更改，现在可以开启一次获取请求。

在 GitHub 上，获取请求是协作( collaboration )的核心。当你开启获取请求时，你所做的就是提供自己的更改，并且请求他人复审你的更改，然后将你的更改合并到他们的分支，那么这就是你的贡献( contribution )了。获取请求( pull request )显示了所有分支的不同。更改、添加和删减通过绿色和红色标识。

只要做了一次提交，你就可以开启一次获取请求并且发起讨论，甚至在代码完成之前就可以。

在你的获取请求中，通过使用 GitHub 的 [ mention system ](https://help.github.com/articles/about-writing-and-formatting-on-github/#text-formatting-toolbar)，你可以向特定的人或者团队请求回馈( feedback )，不管他们是在楼下还是 10 个时区之外。

你甚至可以在自己的仓库开启 pull request 信息，然后自己合并。在你为一个大工程工作之前，这是一种学习 GitHub 工作流程很不错的方式。

下面练习一下。

** 为 README 的更改开启 pull request **

1. 点击 ** Pull Request ** 标签，然后点击 ** New pull request ** 按钮。

 ![](/img/2017/post-github-abc/github-pull01.jpg)

2. 点击分支 readme-edits ，

 ![](/img/2017/post-github-abc/github-pull02.jpg)

3. 仔细检查一下更改之后的不同，确保这是你想提交( submit )的。

 ![](/img/2017/post-github-abc/github-pull03.jpg)

 可以看到显示的是6个添加项，并以绿色标识。  
 下面的图片来自 GitHub 官网，可以看出，删除项以红色标识。

 ![](https://guides.github.com/activities/hello-world/diff.png)

4. 确认 submit 无误之后，点击上方的 ** Create Pull Request ** 按钮

 ![](/img/2017/post-github-abc/github-pull04.jpg)

5. 给你的 pull request 写个标题，然后对你的更改做一个简明的描述。

 ![](/img/2017/post-github-abc/github-pull05.jpg)

一切 OK 之后，点击下方的 ** Create pull request ** 。

另外，原网址提示，在评论和 Pull Request 上可以使用 [ emoji ](https://help.github.com/articles/basic-writing-and-formatting-syntax/#using-emoji) 和[动态图等](https://help.github.com/articles/file-attachments-on-issues-and-pull-requests/)。

### 第五步：合并你的 Pull Request  

在最后一步，是时候把 readme-edits 分支的更改合并到主分支 master 上了。

步骤：

1. 点击 ** Merge pull request ** 按钮来合并更改到 master 分支。

  ![](/img/2017/post-github-abc/github-pull06.jpg)

2. 点击 ** Confirm merge ** 按钮。

  ![](/img/2017/post-github-abc/github-pull07.jpg)

3. 因为更改已经被包含进了 master 分支，可以删除 readme-edits 分支了。 可以看到紫色方形后面的指示：You’re all set—the readme-edits branch can be safely deleted.

   ![](/img/2017/post-github-abc/github-del.jpg)


### 结束语  

祝贺你，完成了这篇指南教程，你已经掌握了如何在 GitHub上创建工程和做 pull request。

我们在小结一下完成的任务：

* 创建了一个开源( open source )的仓库
* 开始并管理了一个新分支
* 更改了一个文件并且把改变提交到了 GitHub
* 开启并且合并了一次 Pull Request

点击你头像旁边的下拉按钮，然后点击 ** Your profile **

   ![](/img/2017/post-github-abc/github-profile.jpg)

然后看一下你的提交历史(就是下图中的小方块)：

 ![](/img/2017/post-github-abc/github-square.jpg)

目前为止，只要咱们一步一步认真的做，那么就算是入门了。

想学习更多关于 __ Pull Requests __ 的知识，GitHub 建议阅读[ GitHub Flow Guide ](https://guides.github.com/introduction/flow/)。我应该会做一篇关于 GitHub Flow Guide 的翻译，欢迎随时关注。

另外，GitHub 提供了一个[ GitHub Explore ](https://github.com/explore)，感兴趣的可以去逛一逛。

---------
> 愿你我都是有态度的人，相识于有温度的文字中。

最后，感谢阅读。
