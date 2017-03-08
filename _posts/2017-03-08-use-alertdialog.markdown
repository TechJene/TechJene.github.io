---
layout:     post
title:      "AlertDialog的第一次主动使用"
#subtitle:   "Slides: Progressive Web App, in my points of view"
date:       2017-03-08
author:     "TechJene"
tags:
    - Android
    - Eclipse
---

**【学习平台：Eclipse+ADT】**

----------
昨天学到了《第一行代码》的6.4.7节。
目前为止，我感觉作者习惯用Logcat日志输出信息。
这一节也是，logcat输出查询到的数据。

之前我一直在使用Toast显示提示或信息。
但是为了能够使用AlertDialog将获取到的信息显示在手机端。

1..先是模仿第一次使用AlertDialog的程序(5.5节：强制下线功能)。
结果没有反应，返回去继续看。
因为弹出的是一个系统级别的对话框，
所以必须要声明android.permission.SYSTEM_ALERT_WINDOW 权限。
修改，增加权限代码：

```
 <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
```
因为还是对AlertDialog的用法不熟悉，以为到此就可以了，
运行程序，结果，没有结果。

2.再次比对代码。
发现没有设置AlertDialog弹出，

在Main活动中补上代码：
```
AlertDialog alertDialog = dialogBuilder.create();
alertDialog.getWindow().setType(WindowManager.LayoutParams.TYPE_SYSTEM_ALERT);
alertDialog.show();
```
3.运行程序，出现了我想要的结果。

![AlertQuery](http://img.blog.csdn.net/20161023110450724)

但是还不是我想要的结果，只是表面上看起来是而已。
这个对话框居然需要我连续点击4次OK才能消失。

去代码中找原因，发现AlertDialog定义在do-while中了，而这个在do-while需要循环4次，so~~~。

将AlertDialog代码块移出循环。
再将变量定义移至循环外。
再次运行，搞定。

下面附上AlertDialog的代码：

```
Button queryData = (Button) findViewById(R.id.query_data);
		queryData.setOnClickListener(new OnClickListener() {

			@Override
			public void onClick(View v) {
				SQLiteDatabase db = dbHelper.getWritableDatabase();
				// 查询Book表中所有数据
				Cursor cursor = db.query("Book", null, null, null, null, null,
						null);
				if (cursor.moveToFirst()) {
					String name = cursor.getString(cursor
							.getColumnIndex("name"));
					String author = cursor.getString(cursor
							.getColumnIndex("author"));
					int pages = cursor.getInt(cursor
							.getColumnIndex("pages"));
					double price = cursor.getDouble(cursor
							.getColumnIndex("price"));
					/*do {
						// 遍历Cursor对象，取出数据并打印
						Log.d("MainActivity", "book name is " + name);
						Log.d("MainActivity", "book author is " + author);
						Log.d("MainActivity", "book pages is " + pages);
						Log.d("MainActivity", "book price is " + price);
					} while (cursor.moveToNext());*/
					//如果不需要logcat输出，上面的do-while循环可以不要。
					AlertDialog.Builder dialogBuilder = new AlertDialog.Builder(
							MainActivity.this);
					dialogBuilder.setTitle("Query Data");
					CharSequence message = "book name is " + name+LINESEP+
							"book author is " + author+LINESEP+
							"book pages is " + pages+LINESEP+
							"book price is " + price;
					dialogBuilder.setMessage(message );
					dialogBuilder.setCancelable(false);
					dialogBuilder.setPositiveButton("OK",
							new DialogInterface.OnClickListener() {

								@Override
								public void onClick(DialogInterface dialog,
										int which) {
									Intent intent = new Intent(
											MainActivity.this,
											MyDatabaseHelper.class);
									intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
								}
							});
					AlertDialog alertDialog = dialogBuilder.create();
					alertDialog.getWindow().setType(WindowManager.LayoutParams.TYPE_SYSTEM_ALERT);
					alertDialog.show();
				}
				cursor.close();
				//之前我常用的信息提示
				Toast.makeText(MainActivity.this, "Query data succeeded",
						Toast.LENGTH_SHORT).show();
			}
		});
```
仍然需要提示的一点是：
**在AndroidManifest.xml中声明权限。**
**在AndroidManifest.xml中声明权限。**
**在AndroidManifest.xml中声明权限。**

以上是我的一点小尝试，只是为了方便我看到Query到的数据。
