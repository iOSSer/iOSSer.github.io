---
layout: post
title: "CoreData Model Version"
date: 2015-09-22
comments: true
categories: iOS
tags: [CoreData]
keywords: CoreData Model Version
description: 
---
---
 关于CoreData`1212`
 
🔨  CoreData 个人认为是 iOS 系统中最好用的数据存储框架，但是使用起来还是不够简洁。不过可以采用第三方的封装库：MagicalRecord  就是一个使用简洁代码封装CoreData的开源库。本文将介绍通过原始方法创建的CoreData项目CoreData版本升级(迁移)的过程。

##为什么要进行升级(迁移)
⚠️ 在一个使用了CoreData的项目中，如果未做CoreData版本升级处理，而直接在entities中进行新增、删除、修改实体(Entity)或新增、删除、修改实体中的Attibute等操作，运行项目是会崩溃的，真机上直接闪退。这也是有的APP打开就闪退的直接原因！如果项目还没有上线，那就随便改吧，反正闪退之后可以将APP删掉就又可以哦，但是如果项目已经上线了，或者线上已经已经有 >= 1个版本了，这时候直接进行以上操作可就有点危险了！


 ##开始吧
 
 - 新建一个 CoreDataDemo 项目，默认勾选 CoreData 选项。

 - 先在CoreDataDemo.xcdatamodeld中模拟新建几张表(CoreData里叫entities)

此时，如果要进行新增、删除、修改实体(Entity)或新增、删除、修改实体中的Attibute等操作,首先需要将CoreDataDemo.xcdatamodeld升级，如何升级？

 - 选中CoreDataDemo.xcdatamodeld，然后点击Xcode菜单Editor,选择add Model Version,即在原版本的基础上添加一个新版本，输入新版本名称，Finish
 - 选中CoreDataDemo.xcdatamodeld，在Xcode右侧菜单栏中File InsPector中找到Model Version，将Current切换为刚刚新建的Model Version
 
如此之后，还有最有一步：

- 在 AppDelegate.m 中，找到这个方法：<pre><code class="hljs javascript"> - (NSPersistentStoreCoordinator *)persistentStoreCoordinator {</code></pre> 将:<pre><code class="hljs javascript">if (![_persistentStoreCoordinator addPersistentStoreWithType:NSSQLiteStoreType configuration:nil URL:storeURL options:nil error:&error]) { </code></pre> 改为：<pre><code class="hljs javascript">
 NSDictionary *optionsDictionary = [NSDictionary dictionaryWithObjectsAndKeys:[NSNumber numberWithBool:YES],NSMigratePersistentStoresAutomaticallyOption, [NSNumber numberWithBool:YES],NSInferMappingModelAutomaticallyOption, nil];
    
    if (![_persistentStoreCoordinator addPersistentStoreWithType:NSSQLiteStoreType configuration:nil URL:storeURL options:optionsDictionary error:&error]) { </code></pre>


##### 大功告成~



 


