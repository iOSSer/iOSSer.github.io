---
layout: post
title:  "Global UITableView DataSource"
date:   2015-10-29 09:46:39
author: lipeng
categories: iOS
tags:	iOS 
cover:  "assets/instacode.png"
---

在项目中，有很多界面的UITableViewCell都很简单，Cell高度都一样，不像聊天界面的Cell高度不确定，对于处理这种高度一样、布局简单的Cell，每个界面都要重写一次`UITableViewDataSource`的2个方法:
 
<pre><code class="hljs objectivew-c">    
  - (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section;

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath;
<br><br>
</code></pre>

这样做未免有些繁琐，而我有是一个比较懒的程序员，能用1行搞定的事情绝不写10行。所以在看了相关的文章对DataSource的封装之后，自己写了一个，希望以后项目中遇到这样的界面就这一个类搞定了。

## Adding New Posts

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

### Tags and Categories

If you list one or more categories or tags in the front matter of your post, they will be included with the post on the page as links. Clicking the link will bring you to an auto-generated archive page for the category or tag, created using the [jekyll-archive][jekyll-archive] gem.

### Cover Images

To add a cover image to your post, set the "cover" property in the front matter with the relative URL of the image (i.e. <code>cover: "assets/cover_image.jpg"</code>). 

### Code Snippets

You can use [highlight.js][highlight] to add syntax highlig code snippets:

<pre><code class="hljs Objective C">function demo(string, times) {
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
