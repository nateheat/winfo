---
layout: post
title:  "Linux安装Jekyll"
date:   2017-09-09 06:25:25 +0400
categories: jekyll 
---

 本文讨论在Linux环境下安装Jekyll在PC本地编辑及浏览静态网站。同时也适用在Windows 10的Linux Subsystem下使用。
 这儿说的Linux暂时对应Ubuntu 16.04，也同时包括基于Ubuntu的别的Linux。

 *在 Fedora 26下也经过了测试，仅需使用稍微不同的命令而已。（比如把`apt`换成`dnf`） 参考[here](/guide/install-jekyll)*

在Windows下，进入*Bash for Windows*命令行，或在*Command Prompt* (i.e. `cmd`)下键入`bash`进入。
在Linux下，打开terminal命令行。
之后的操作，基本上在Linux和在Windows 10的Linux Subsystem下没有区别（除非特别指出的话）。

有可能Ruby已经安装了，可通过以下命令检查其版本

```Bash
$ruby -v
ruby 2.3.1p112 (2016-04-26) [x86_64-linux-gnu]
```

(如果没有ruby可以通过`sudo apt install ruby`或者`sudo apt install ruby-full`安装。)

为了后面使用Bundler和Jekyll，需要安装`sudo apt install ruby-dev`。如果后面安装过程出现java runtime missing类似的出错信息，可以考虑安装nodejs包`sudo apt install nodejs`。

首先我们安装Bundler，在命令行输入`sudo gem install bundler`。

之后按照[Github Pages的文档][gp-set-local]的安装方式，是先建一个目录，设一个Gemfile然后使用bundle install来安装包括Github Pages和Jekyll以及他们的dependencies。

1. 新建一个目录（比如newsite）：`mkdir newsite`
2. 然后进入此目录：`cd newsite`
3. 建立一个*Gemfile*的文本文件，输入以下内容
```
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```
4. 使用`bundle install`来安装需要的gems（包括Github Pages和Jekyll以及他们的dependencies）。这一步会需要一些时间，因为可能有比较多的gems需要安装的。

这儿如果遇到关于`nokogiri`的错误，可以确保安装了`build-essential`, `patch`, `ruby-dev`, `zlib1g-dev` 和 `liblzma-dev`。此处参考[nokogiri.org的文档][nokogiri-install]。

```Bash
$sudo apt install build-essential patch
$sudo apt install ruby-dev zlib1g-dev liblzma-dev
```
成功完成上面几步，bundle install没有问题了之后，最基本的Github Pages环境就已经设置好了，

可以用最简单的Hello World来进行测试：

在之前建好的目录（newsite）下建立一个*index.html*，输入单行内容*Hello World!*。

```bash
$echo "Hello World!" > index.html
```

然后使用命令 `$bundle exec jekyll serve`，就可以打开jekyll的网站服务了。

```bash
.../newsite$ bundle exec jekyll serve
Configuration file: none
            Source: .../newsite
       Destination: .../newsite/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 1.962 seconds.
 Auto-regeneration: enabled for '.../newsite'
    Server address: http://127.0.0.1:4000
  Server running... press ctrl-c to stop.
```

根据上面的提示，在浏览器地址栏输入URL:`http://127.0.0.1:4000`，或者`localhost:4000`，

就可以访问到页面仅显示*Hello World!*的网页啦^_^



[gp-set-local]: https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/
[nokogiri-install]:http://www.nokogiri.org/tutorials/installing_nokogiri.html
