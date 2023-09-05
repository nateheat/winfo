---
layout: post
title:  "Linux安装Jekyll, Github-Pages"
date:   2023-09-04 08:25:25 -0400
categories: jekyll 
---

几年前的[短文][origin-article]讨论了在Linux下安装Jekyll的一些步骤，其中一些内容需要更新，因此以此文作为更新版本，对应的时间为2023年下半年。
 本文讨论在Linux环境下安装Jekyll在PC本地编辑及浏览静态网站。同时也适用在Windows 11的Linux Subsystem下使用。
 这儿说的Linux暂时对应Ubuntu 22.04，也同时包括基于Ubuntu的别的Linux。

在Windows下，进入*Bash for Windows*命令行，或在*Command Prompt* (i.e. `cmd`)下键入`bash`进入。
在Linux下，打开terminal命令行。
之后的操作，基本上在Linux和在Windows 11的Linux Subsystem下没有区别（除非特别指出的话）。

有可能Ruby已经安装了，可通过以下命令检查其版本

```Bash
$ruby -v
ruby 3.0.2p107 (2021-07-07 revision 0db68f0233) [x86_64-linux-gnu]
```

但即使已经安装了ruby，仍建议按[jekyll的官方安装文档][jekyll-install]的建议，安装ruby-full以及别的组件。

{% highlight bash %}
sudo apt-get install ruby-full build-essential zlib1g-dev
{% endhighlight %}

然后在`.bashrc`文件设好gems的安装路径
{% highlight bash %}
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
{% endhighlight %}

然后就可以通过*gem*安装Jekyll和Bundler了。
{% highlight bash %}
gem install jekyll bundler
{% endhighlight %}


之后按照[Github Pages的文档][gp-set-local]的安装方式，是先建一个目录，设一个Gemfile然后使用bundle install来安装包括Github Pages和Jekyll以及他们的dependencies。

1. 新建一个目录（比如newsite）：`mkdir newsite`
2. 然后进入此目录：`cd newsite`
3. 建立一个*Gemfile*的文本文件，输入以下内容
```
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
gem 'webrick'
```
4. 使用`bundle install`来安装需要的gems（包括Github Pages和Jekyll以及他们的dependencies）。这一步会需要一些时间，因为可能有比较多的gems需要安装的。


可以用最简单的Hello World来进行测试：

在之前建好的目录（newsite）下建立一个*index.html*，输入单行内容*Hello World!*。

```bash
$echo "Hello World!" > index.html
```

然后使用命令 `$bundle exec jekyll serve`，就可以打开jekyll的网站服务了。

```bash
.../newsite$ bundle exec jekyll serve
Configuration file: none
To use retry middleware with Faraday v2.0+, install `faraday-retry` gem
            Source: /home/.../newsite
       Destination: /home/.../newsite/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 1.225 seconds.
                    Auto-regeneration may not work on some Windows versions.
                    Please see: https://github.com/Microsoft/BashOnWindows/issues/216
                    If it does not work, please upgrade Bash on Windows or run Jekyll with --no-watch.
 Auto-regeneration: enabled for '/home/.../newsite'
    Server address: http://127.0.0.1:4000
  Server running... press ctrl-c to stop.
```

根据上面的提示，在浏览器地址栏输入URL:`http://127.0.0.1:4000`，或者`localhost:4000`，

就可以访问到页面仅显示*Hello World!*的网页啦^_^



[gp-set-local]: https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/
[nokogiri-install]:http://www.nokogiri.org/tutorials/installing_nokogiri.html
[origin-article]: https://nateheat.github.io/winfo/jekyll/2017/09/09/Linux%E5%AE%89%E8%A3%85Jekyll.html
[jekyll-install]: https://jekyllrb.com/docs/installation/ubuntu/