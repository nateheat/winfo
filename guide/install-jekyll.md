---
layout: page
title:  "Install Jekyll"
---

## Fedora 26 下安装

在Fedora 26下安装Jekyll跟在Ubuntu下类似，只是有一些系统默认安装的package的区别。

*在安装前，确保Fedora系统已经安装了基本的build环境`sudo dnf install gcc make`。*

### 安装Ruby

```Bash
$ sudo dnf install ruby ruby-devel
...
$ ruby --version
ruby 2.4.1p111 (2017-03-22 revision 58053) [x86_64-linux]
```

### Gems安装Jekyll Bundler

安装Jekyll之前需要确保系统已经有`libffi-devel`和`redhat-rpm-config`两个packages，如果是Fedora 26 workstation默认是没有安装这两个的。

```Bash
$ sudo dnf install libffi-devel redhat-rpm-config
```

之后就可以顺利安装Jekyll和Bundler了。

```Bash
$ gem install jekyll bundler
```

### 使用**bundle install**安装需要的gems

类似于在Ubuntu下，新建一个目录*newsite*，进入此目录（`cd newsite`），新建*Gemfile*并输入以下内容
```
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```

运行`bundle install`之前，需要保证安装了`zlib-devel`。
```Bash
$ sudo dnf install zlib-devel
$ bundle install
```

### **Hello World**测试

在当前版本下（Fedora 26），需要在*Gemfile*添加一行`gem 'json'`，否则会出现类似`cannot load such file -- json`的错误信息。

新建只有“Hello World”的单行内容的文件*index.html*，（`$echo "Hello World" > index.html`）。

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

打开浏览器在地址栏输入URL:`http://127.0.0.1:4000`或`localhost:4000`即可访问显示*Hello World*的网页。


## FreeBSD

在FreeBSD下安装Jekyll，可以有很多灵活的方法，这儿试图用较简单的方法。

### 安装Ruby Gems

FreeBSD已经安装了Ruby，我们从安装Ruby Gems开始。

打开terminal，登入`root`，然后通过port安装`devel/ruby-gems`（此处使用`portmaster`安装）。

```bash
$ su
$ portmaster devel/ruby-gems
```

之后的操作退出root用普通用户+`sudo`也很方便，本文使用此方法。

### 安装Jekyll和Bundler

```bash
$ sudo gem install jekyll bundler
```

### 使用`bundle install`安装需要的gems

新建目录`$mkdir newsite`，进入此目录`$cd newsite`，新建*Gemfile*并输入以下内容
```
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```

运行`$bundle install`以安装需要的gems，系统会在需要的时候要求输入`sudo`的密码。

### **Hello World**测试

新建只有“Hello World”内容的文件*index.html*，（`$echo "Hello World" > index.html`）。

在Linux下，到这儿就可以直接用`$bundle exec jekyll serve`测试Hello World网页了。在FreeBSD有一些区别。

如果遇到类似于`no JavaScript runtime`的错误，可以考虑安装`Node.js`，（`$sudo pkg install node`）。

还会出现类似于`Error:  Invalid US-ASCII character "\xE2" on line 5`的错误，暂时知道有两种方法绕开此问题：

1. 提前设置`_config.yml`文件并设主题theme：`$echo "theme: minima" > _config.yml`;
2. 在`.bashrc`或别的shell初始文件设置以下内容并重启shell。（参考[此文](https://github.com/haml/haml/issues/269)里面提到的解决方法）
```
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
```

推荐方法1，方法2仅供参考。

现在，使用命令`$bundle exec jekyll serve`，就可以打开jekyll的网站服务了。

```bash
[.../newsite]$ bundle exec jekyll serve
Configuration file: /usr/home/.../newsite/_config.yml
            Source: /usr/home/.../newsite
       Destination: /usr/home/.../newsite/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
                    done in 0.151 seconds.
  Please add the following to your Gemfile to avoid polling for changes:
    require 'rbconfig'
    if RbConfig::CONFIG['target_os'] =~ /(?i-mx:bsd|dragonfly)/
      gem 'rb-kqueue', '>= 0.2'
    end
 Auto-regeneration: enabled for '/usr/home/.../newsite'
    Server address: http://127.0.0.1:4000
  Server running... press ctrl-c to stop.
```

打开浏览器在地址栏输入URL:`http://127.0.0.1:4000`或`localhost:4000`即可访问显示*Hello World*的网页。

*如提示所说，在Gemfile中增加**rbconfig**等的内容可以避免那几行提示。*
