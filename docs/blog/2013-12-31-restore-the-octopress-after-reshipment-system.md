---
layout: post
title: "重装系统后恢复Octopress"
date: 2013-12-31 15:29
comments: true
categories: Mac
---

#restore-the-octopress-after-reshipment-system

如何你想学习如何基于github搭建一个自己的Octopress博客,请参考以下两篇文章哈

 - [http://blog.163.com/fuhaocn@126/blog/static/366650802012115103842500/](http://blog.163.com/fuhaocn@126/blog/static/366650802012115103842500/)
 - [http://blog.devtang.com/blog/2012/02/10/setup-blog-based-on-github/](http://blog.devtang.com/blog/2012/02/10/setup-blog-based-on-github/)


Mac重装了很久,一直也没有恢复Octopross的博客系统.今天是2013年最后一天啦,顺手弄弄.

这一切基于你的Mac环境什么都妥妥的了.比如xcode,git,ruby...等等

##0. 首先是把项目clone到本地,接着开始吧  

```
○ git clone git@github.com:wuyexiong/wuyexiong.github.com.git
Cloning into 'wuyexiong.github.com'...
remote: Counting objects: 5004, done.
remote: Compressing objects: 100% (1758/1758), done.
remote: Total 5004 (delta 2798), reused 5002 (delta 2797)
Receiving objects: 100% (5004/5004), 1.47 MiB | 340.00 KiB/s, done.
Resolving deltas: 100% (2798/2798), done.
Checking connectivity... done
```

##1. 切换到source分支下 

```
± git checkout source
Branch source set up to track remote branch source from origin.
Switched to a new branch 'source'
```
```
± git branch -a
  master
* source
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
  remotes/origin/source
```
<!-- more -->

##2. 打开blog文件夹,接着就会弹出rvm相关信息，写yes

```
± cd blog
You are using '.rvmrc', it requires trusting, it is slower and it is not compatible with other ruby managers,
you can switch to '.ruby-version' using 'rvm rvmrc to [.]ruby-version'
or ignore this warning with 'rvm rvmrc warning ignore /Users/wuyexiong/Blog/wuyexiong.github.com/.rvmrc',
'.rvmrc' will continue to be the default project file in RVM 1 and RVM 2,
to ignore the warning for all files run 'rvm rvmrc warning ignore all.rvmrcs'.

********************************************************************************************************************
* NOTICE                                                                                                           *
********************************************************************************************************************
* RVM has encountered a new or modified .rvmrc file in the current directory, this is a shell script and           *
* therefore may contain any shell commands.                                                                        *
*                                                                                                                  *
* Examine the contents of this file carefully to be sure the contents are safe before trusting it!                 *
* Do you wish to trust '/Users/wuyexiong/Blog/wuyexiong.github.com/.rvmrc'?                                        *
* Choose v[iew] below to view the contents                                                                         *
********************************************************************************************************************
y[es], n[o], v[iew], c[ancel]> y
Using /Users/wuyexiong/.rvm/gems/ruby-2.0.0-p247
```

##3.接下来安装OctoPress相关环境

###gem install bundler

```
± gem install bundler
Successfully installed bundler-1.5.1
Parsing documentation for bundler-1.5.1
1 gem installed
```
###bundle install
```
± bundle install
Fetching gem metadata from http://rubygems.org/.......
Fetching additional metadata from http://rubygems.org/..
Installing rake (0.9.2.2)
Installing RedCloth (4.2.9)
Installing chunky_png (1.2.5)
Installing fast-stemmer (1.0.1)
***略
***略
Installing stringex (1.4.0)
Using bundler (1.5.1)
Your bundle is complete!
Use `bundle show [gemname]` to see where a bundled gem is installed.
```
###gem install jekyll
```
± gem install jekyll
Fetching: liquid-2.5.4.gem (100%)
Successfully installed liquid-2.5.4
Fetching: rb-fsevent-0.9.4.gem (100%)
Successfully installed rb-fsevent-0.9.4
Fetching: ffi-1.9.3.gem (100%)
Building native extensions.  This could take a while...
Successfully installed ffi-1.9.3
***略
***略
Installing ri documentation for parslet-1.5.0
Parsing documentation for toml-0.1.0
Installing ri documentation for toml-0.1.0
Parsing documentation for jekyll-1.4.2
Installing ri documentation for jekyll-1.4.2
17 gems installed
```

##4.修复rake环境问题

　　执行rake install的时候弹出错误提示

```
± rake install
rake aborted!
You have already activated rake 10.1.0, but your Gemfile requires rake 0.9.2.2. Prepending `bundle exec` to your command may solve this.
/Users/wuyexiong/.rvm/gems/ruby-2.0.0-p247/gems/bundler-1.5.1/lib/bundler/runtime.rb:34:in `block in setup'
/Users/wuyexiong/.rvm/gems/ruby-2.0.0-p247/gems/bundler-1.5.1/lib/bundler/runtime.rb:19:in `setup'
/Users/wuyexiong/.rvm/gems/ruby-2.0.0-p247/gems/bundler-1.5.1/lib/bundler.rb:119:in `setup'
/Users/wuyexiong/.rvm/gems/ruby-2.0.0-p247/gems/bundler-1.5.1/lib/bundler/setup.rb:7:in `<top (required)>'
/Users/wuyexiong/Blog/wuyexiong.github.com/Rakefile:2:in `<top (required)>'
(See full trace by running task with --trace)
```
###这时候打开Octopress根目录下的Gemfile修改为如下

```
group :development do
  gem 'rake', '~> 10.1.0'  //修改这一行
  gem 'jekyll', '~> 0.12'
  gem 'rdiscount', '~> 1.6.8'
  gem 'pygments.rb', '~> 0.3.4'
  gem 'RedCloth', '~> 4.2.9'
  gem 'haml', '~> 3.1.7'
  gem 'compass', '~> 0.12.2'
  gem 'sass-globbing', '~> 1.0.0'
  gem 'rubypants', '~> 0.2.0'
  gem 'rb-fsevent', '~> 0.9'
  gem 'stringex', '~> 1.4.0'
  gem 'liquid', '~> 2.3.0'
end

gem 'sinatra', '~> 1.4.2'
```

##5. 运行部署
　　试试看rake preview,浏览器打开http://localhost:4000看看效果吧.

```
± rake preview
Starting to watch source with Jekyll and Compass. Starting Rack on port 4000
[2013-12-31 15:54:08] INFO  WEBrick 1.3.1
[2013-12-31 15:54:08] INFO  ruby 2.0.0 (2013-06-27) [x86_64-darwin12.5.0]
[2013-12-31 15:54:08] INFO  WEBrick::HTTPServer#start: pid=15479 port=4000
Configuration from /Users/wuyexiong/Blog/wuyexiong.github.com/_config.yml
Auto-regenerating enabled: source -> public
[2013-12-31 15:54:08] regeneration: 136 files changed

Dear developers making use of FSSM in your projects,
FSSM is essentially dead at this point. Further development will
be taking place in the new shared guard/listen project. Please
let us know if you need help transitioning! ^_^b
- Travis Tilley

>>> Compass is watching for changes. Press Ctrl-C to Stop.
```

##6.最后一定忘了什么…
 
  这篇文章写完了.  
  rake generate && rake deploy之后……   
  等了十几分钟,还没刷新出网页,总感觉哪里不对劲…
  执行以下命令发布Octopress到Github
  
```
± rake setup_github_pages
Enter the read/write url for your repository
(For example, 'git@github.com:your_username/your_username.github.io)
Repository url: git@github.com:wuyexiong/wuyexiong.github.com.git//这里写你的github上博客repository的ssh URL
rm -rf _deploy
mkdir _deploy
cd _deploy
Initialized empty Git repository in /Users/wuyexiong/Blog/wuyexiong.github.com/_deploy/.git/
[master (root-commit) ada2d3b] Octopress init
 1 file changed, 1 insertion(+)
 create mode 100644 index.html
cd -
---
## Now you can deploy to http://wuyexiong.github.io with `rake deploy` ##
```

这下好了,你们就可以看到这篇文章啦. 所以.方案肯定是本人验证过的...谢谢大家哈

