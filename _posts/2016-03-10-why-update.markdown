---
layout: post
title:  "这个博客好难搞啊"
date:   2016-03-10 
author: Li Peng
categories: iOS
tags:	jekyll welcome 
cover:  "assets/instacode.png"
---

🔨  `CoreData` 个人认为是 iOS 系统中最好用的数据存储框架，但是使用起来还是不够简洁。不过可以采用第三方的封装库：MagicalRecord  就是一个使用简洁代码封装CoreData的开源库。本文将介绍通过原始方法创建的CoreData项目CoreData版本升级(迁移)的过程。

## 为什么要进行升级(迁移)

⚠️ 在一个使用了CoreData的项目中，如果未做CoreData版本升级处理，而直接在entities中进行新增、删除、修改实体(Entity)或新增、删除、修改实体中的Attibute等操作，运行项目是会崩溃的，真机上直接闪退。这也是有的APP打开就闪退的直接原因！如果项目还没有上线，那就随便改吧，反正闪退之后可以将APP删掉就又可以哦，但是如果项目已经上线了，或者线上已经已经有 >= 1个版本了，这时候直接进行以上操作可就有点危险了！

###开始吧
 
 - 新建一个 CoreDataDemo 项目，默认勾选 CoreData 选项。

 - 先在CoreDataDemo.xcdatamodeld中模拟新建几张表(CoreData里叫entities)

此时，如果要进行新增、删除、修改实体(Entity)或新增、删除、修改实体中的Attibute等操作,首先需要将CoreDataDemo.xcdatamodeld升级，如何升级？

<!--You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

## Adding New Posts

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

### Tags and Categories

If you list one or more categories or tags in the front matter of your post, they will be included with the post on the page as links. Clicking the link will bring you to an auto-generated archive page for the category or tag, created using the [jekyll-archive][jekyll-archive] gem.

### Cover Images

To add a cover image to your post, set the "cover" property in the front matter with the relative URL of the image (i.e. <code>cover: "assets/cover_image.jpg"</code>). 

### Code Snippets

You can use [highlight.js][highlight] to add syntax highlig code snippets:

<pre><code class="hljs javascript">function demo(string, times) {
  for (var i = 0; i < times; i++) {
    console.log(string);
  }
}
demo("hello, world!", 10);</code></pre>

### Images

Lightbox has been enabled for images. To create the link that'll launch the lightbox, add <code>data-lightbox</code> and <code>data-title</code> attributes to an <code>&lt;a&gt;</code> tag around your <code>&lt;img&gt;</code> tag. The result is:

<a href="//bencentra.com/assets/images/falcon9_large.jpg" data-lightbox="falcon9-large" data-title="Check out the Falcon 9 from SpaceX">
  <img src="//bencentra.com/assets/images/falcon9_small.jpg" title="Check out the Falcon 9 from SpaceX">
</a>

For more information, check out the [Lightbox][lightbox] website.

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll’s dedicated Help repository][jekyll-help].

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
[highlight]:   https://highlightjs.org/
[lightbox]:    http://lokeshdhakar.com/projects/lightbox2/
[jekyll-archive]: https://github.com/jekyll/jekyll-archives
-->