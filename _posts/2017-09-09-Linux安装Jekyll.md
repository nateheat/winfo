---
layout: post
title:  "Linux安装Jekyll"
date:   2017-09-09 06:25:25 +0400
categories: jekyll installation 安装 教程
---

 本文讨论在Linux环境下安装Jekyll在PC本地编辑及浏览静态网站。同时也适用在Windows 10的Linux Subsystem下使用。
 这儿说的Linux暂时对应Ubuntu 16.04，也同时包括基于Ubuntu的别的Linux。

 *在 Fedora 26下也经过了测试，仅需使用稍微不同的命令而已。（比如把`apt`换成`dnf`）*

在Windows下，进入*Bash for Windows*命令行，或在*Command Prompt* (i.e. `cmd`)下键入`bash`进入。
在Linux下，打开terminal命令行。
之后的操作，基本上在Linux和在Windows 10的Linux Subsystem下没有区别（除非特别指出的话）。

一般Ruby已经随Linux安装了，可通过以下命令检查其版本

```Bash
$ruby -v
ruby 2.3.1p112 (2016-04-26) [x86_64-linux-gnu]
```

(如果没有ruby可以通过`sudo apt install ruby`或者`sudo apt install ruby-full`安装。)

为了后面使用Bundler和Jekyll，需要安装`sudo apt install ruby-dev`。如果后面安装过程出现java runtime missing类似的出错信息，可以考虑安装nodejs包`sudo apt install nodejs`。

下一步安装Bundler,

You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
