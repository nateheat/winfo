---
layout: page
title:  "Install Jekyll"
---

# Fedora 26

在Fedora 26下安装Jekyll跟在Ubuntu下类似，只是有一些系统默认安装的package的区别。

*在安装前，确保Fedora系统已经安装了基本的build环境`sudo dnf install gcc make`。*

## 安装Ruby

```Bash
$sudo dnf install ruby ruby-devel
...
$ ruby --version
ruby 2.4.1p111 (2017-03-22 revision 58053) [x86_64-linux]
```

## Gems安装Jekyll Bundler

安装Jekyll之前需要确保系统已经有`libffi-devel`和`redhat-rpm-config`两个packages，如果是Fedora 26 workstation默认是没有安装这两个的。

```Bash
$sudo dnf install libffi-devel redhat-rpm-config
```

之后就可以顺利安装Jekyll和Bundler了。

```Bash
$gem install jekyll bundler
```

## 使用`bundle install`安装需要的gems

类似于在Ubuntu下，新建一个目录*newsite*，进入此目录（`cd newsite`），新建*Gemfile*并输入以下内容
```
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```

运行`bundle install`之前，需要保证安装了`zlib-devel`。
```Bash
$sudo dnf install zlib-devel
$bundle install
```

## *Hello World*测试

在当前版本下（Fedora 26），需要在*Gemfile*添加一行`gem 'json'`，否则会出现类似`cannot load such file -- json`的错误信息。

新建只有“Hello World”的单行内容的文件*index.html*，

然后使用命令 `$bundle exec jekyll serve`，就可以打开jekyll的网站服务了。

```bash
[...@localhost newsite]$ bundle exec jekyll serve
Configuration file: none
            Source: /.../newsite
       Destination: /.../newsite/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
                    done in 1.439 seconds.
 Auto-regeneration: enabled for '/.../newsite'
    Server address: http://127.0.0.1:4000
  Server running... press ctrl-c to stop.
```

打开浏览器在地址栏输入URL:`http://127.0.0.1:4000`或`localhost:4000`即可访问显示*Hello World!*的网页。


