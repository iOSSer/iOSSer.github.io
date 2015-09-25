---
layout: post
title: "Use CocoaPods"
date: 2015-09-25
comments: true
categories: iOS
tags: [CocoaPods]
keywords: CocoaPods
description: 
---

<!--<img src="http://7xl8q7.com1.z0.glb.clouddn.com/Coredata_Create.png" width="900" height="600">-->

---
 CocoaPods的安装就不赘述了，此博文主要记录一下`CocoaPods的使用`。
  <br><br>
   
 当要使用pod下载第三方库到项目中，首先要新建一个`Podfile`文件(`Podfile主要用来记录第三方库名称及版本号`)，此文件没有.txt什么的后缀名，所以在Finder中自己创建我还没找到方法。这儿主要介绍如何通过终端创建`Podfile`文件：
 <br>
 打开终端，cd到项目主目录，依次执行下面的语句
 
 `touch Podfile`
 
 `open -e Podfile`
 
 上面第一句是创建`Podfile`文件，第二句是打开`Podfile`文件。
 打开后，输入需要添加的第三方库名称及版本号即可，一般如这种格式:
 
 `pod 'SWTableViewCell', '~> 0.3.7'`
 
 如果对第三方库名称记不清，或者版本号不清楚，可以在终端使用pod搜索，如：
 
 `pod search sdwebimage`
 
 要添加多个第三方库，直接这样写即可:
 
 `pod 'SWTableViewCell', '~> 0.3.7'`
 
`pod 'AFNetworking'`

`pod 'SDWebImage', '~> 3.7.3'`
<br>
<br>
 
 编辑好`Podfile`文件后，保证cd在项目根目录下，执行安装操作：
 
 `pod install`

####就酱紫~😐