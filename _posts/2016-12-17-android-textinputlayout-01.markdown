---
layout:     post
title:      "实现 hint 浮动显示(一)"
subtitle:   " \"探讨 TextInputLayout 的使用\""
date:       2016-12-17 17:40:00
author:     "TechJene"
header-img: "img/post-2016-csdn.jpg"
catalog: true
tags:
    - Android
    - hint  
    - TextInputLayout
---
> "去年相送，余杭门外，飞雪似杨花。"

**说明**：原发布于 [CSDN 个人博客](http://blog.csdn.net/yaoyuandemeili/article/details/53710049)

- 学习平台：Android Studio 2.2.3 (基于win8.1 Pro)
- ADT：Nexus5
- API：24
- 参考书籍：《第一行代码》2th edition

### 前言

有关章节：3.2 常用控件的使用方法。

关于 hint 提示，郭老师的第一版书使用的是 EditText 的 hint，默认有浅色的文字提示，确实比没有任何提示好。

但是我也见过另一种 hint，用户输入时会自动到输入框左上角，所以看到3.2节时，我希望有我想要的改变，结果，没有变化。

我原以为新型的 hint 仍然是 EditText 的属性，所以查看[官方文档](https://developer.android.com/reference/android/widget/EditText.html)。

浏览一遍，没有找到我需要的内容，所以直接 Google：hint Android，知道了这种 hint 叫 **floating hint**，但是搜索到的是一个视频教程，所以 Google 关键词 **floating hint**。  
找到有关教程[Android Material Design Floating Labels for EditText](http://www.androidhive.info/2015/09/android-material-design-floating-labels-for-edittext/)。

原来是需要 **TextInputLayout**。

### 正文

下面是我使用 TextInputLayout 的步骤：  
#### 第一步：添加 Support Library

 1. 在 Android Studio中，File-->Project Structure-->app-->Dependencies--添加 Library dependency
 ![添加依赖库](http://img.blog.csdn.net/20161217173857826?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvWWFveXVhbmRlbWVpbGk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
 2. 搜索 design，找到 com.android.support:design:25.0.1。

#### 第二步：修改布局文件

将EditText包含于TextInputLayout内层。
如下：

```xml
<android.support.design.widget.TextInputLayout
        android:id="@+id/layout_edit_text"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <EditText
            android:id="@+id/edit_text"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Type something here" />
    </android.support.design.widget.TextInputLayout>
```
实效果如图，确实，hint 到了左上角  
![这里写图片描述](http://img.blog.csdn.net/20161217183254338?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvWWFveXVhbmRlbWVpbGk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)  
但是浮动太快，来不及看，以为运行时，hint 就直接出现于输入框左上角了呢！

不过没有关系，我又添加了一个 TextInputLayout。  
以下是效果图
![这里写图片描述](http://img.blog.csdn.net/20161217191520307?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvWWFveXVhbmRlbWVpbGk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### 后记

以上就是我对 EditText 的进一步学习。

另外，一点说明，我开始写博客，并不是单纯地记录实现某些功能或完成某个项目的步骤，我更是为了积累自己的这个过程，所以相对有些啰嗦。

昨晚添加 TextInputLayout 时，一直没有出现我想要的浮动效果，所以就以为自己的代码出了问题，又继续去参考别人的文章，确实找到一篇。

如果需要，请看下一篇--《实现 hint 浮动显示(二)》。谢谢！

---------
> 愿你我都是有态度的人，相识于有温度的文字中。

最后，感谢阅读。
