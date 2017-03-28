---
layout:     post
title:      "AndroidManifest 注册问题"
subtitle:   " \"利用好 logcat \""
date:       2016-10-20 16:49:00
author:     "TechJene"
header-img: "img/post-2016-csdn.jpg"
catalog: true
tags:
    - Android
    - logcat
    - fragmeng
---
> "回首向来萧瑟处。"

**说明**：原发布于 [CSDN 个人博客](http://blog.csdn.net/yaoyuandemeili/article/details/52874573)

**【学习平台：Eclipse+ADT】**

### 前言

前两天开始读《第一行代码》，今天学习到了第四章，讲的是 Fragment。

做到本章的最后一部分--简易新闻应用时，出现问题。  

**问题描述：**
程序在平板虚拟机端运行没有问题，但是手机虚拟端在点击新闻Title时，程序崩溃。


### 正文

我无奈，对照着书又走了2遍的步骤，没有发现代码写错的问题。更无奈了~~~

下午忽然想到可以看看 logcat 的日志输出。

果然，找到了问题所在，下面是日志信息  
![Logcat输出](http://img.blog.csdn.net/20161020170103190)

说 Activity 没有找到，还提示你有没有在 AndroidManifest.xml 中声明。  

我打开自己的 AndroidManifest.xml，确实没有声明该活动。

所以补上下面的代码：
```xml
<activity android:name=".NewsContentActivity" >
</activity>
```

程序运行崩溃问题解决。

然而，还有问题没有解决。  

为什么之前在手机端崩溃，却在平板端可以运行？


**分析**  

两者的主要不同在于：  
	手机使用的是：layout 文件夹下的 activity_main.xml   
	平板使用的是：layout-sw600dp 文件夹下的 activity_main.xml


我按照作者的写法，分别定义两个布局为：单页模式和双页模式，  
以下是代码：
layout 下的 activity_main.xml【单页模式】

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent" >

    <fragment
        android:id="@+id/news_title_fragment"
        android:name="com.example.fragmentnewspractice.NewsTitleFragment"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</LinearLayout>
```
layout-sw600dp下的 activity_main.xml 【双页模式】

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent" >

	<fragment
	    android:id="@+id/news_title_fragment"
	    android:name="com.example.fragmentnewspractice.NewsTitleFragment"
	    android:layout_width="0dp"
	    android:layout_height="match_parent"
	    android:layout_weight="1" />

	<FrameLayout
	    android:id="@+id/news_content_layout"
	    android:layout_width="0dp"
	    android:layout_height="match_parent"
	    android:layout_weight="3" >

	    <fragment
	        android:id="@+id/news_content_fragment"
	        android:name="com.example.fragmentnewspractice.NewsContentFragment"
	        android:layout_width="match_parent"
	        android:layout_height="match_parent" />
	</FrameLayout>

</LinearLayout>
```
比对代码，很容易看出，双页模式下同时引入了两个碎片, 并将新闻内容的碎片放在了一个 FrameLayout 布局下。

另外的区别是 NewTitleFragment.java 的部分代码：

```java
public void onItemClick(AdapterView<?> parent, View view, int position,
		long id) {
	News news = newsList.get(position);
	if (isTwoPane) {
		//若为双页模式，则刷新NewsContentFragment中的内容
		NewsContentFragment newsContentFragment =
				(NewsContentFragment)getFragmentManager().findFragmentById(R.id.news_content_fragment);
		newsContentFragment.refresh(news.getTitle(), news.getContent());
	} else {
		//单页模式下，直接启动NewsContentActivity
		NewsContentActivity.actionStart(getActivity(), news.getTitle(), news.getContent());
	}
}

```
可以看出，如果是单页模式，需要启动 NewsContentActivity，然而因为没有在 AndroidManifest.xml 中注册该 Activity，所以导致程序在点击 Title 时崩溃。

对于应用于平板的双页模式则不同，无需启动 NewsContentActivity 即可刷新 NewsContentFragment 中的内容，所以双页模式运行没有崩溃。


### 后记
以上是我个人对问题的原因分析，由于是初学者，所以可能不太全面。  
另外，我的感受是：一定要利用好 Logcat，可以省去不少功夫。

---------
> 愿你我都是有态度的人，相识于有温度的文字中。

最后，感谢阅读。
