---
layout: post
title: "在Github上搭建Octopress"
date: 2013-05-05 09:19
comments: true
categories: [Octpress]
---
	    
前些天在网上看到[Octopress](http://octopress.org/)这个静态博客，它的一些特色我挺喜欢，便花了些时间在Github上搭建了个Octpress博客。搭建过程还算顺利，在这就把搭建和使用的流程以及遇到的问题及其解决方法做个简单记录，做为LZ的第一篇博文。**注意：本文介绍的内容是针对Mac系统**
	    
## 0. Outline
- “主角”介绍
- 环境准备
- 部署Octopress到Github
- Octopress的基本操作
- Octopress进阶配置
<!--more-->
## 1. “主角”介绍
首先上场的是——Octopress，Octopress是一款用Ruby语言开发的Blog框架，它的的特点LZ总结为两个字——“优雅”，当然这是废话，下面是正统的介绍：

- 通过运行生成静态页面，无数据库
- 使用Markdown标记语言撰写文章
- 系统管理和文章发布都是Shell命令的方式，Cool
- 方便的部署到Github Pages

有关Octopress的更多信息，可以移步到[官网](http://octopress.org/)。

接下来出场的是大名鼎鼎的GitHub，就不做介绍了，因为我们的Blog是要部署为GitHub Pages，所以首先你得有一个GitHub帐号，如果没有，那赶紧[注册](https://github.com)一个。

---

## 2. 环境准备
Octopress需要高于1.9.3的Ruby版本，你可以在Shell下执行`ruby --version`查看当前使用的Ruby版本号，如果已经是1.9.3以上的版本，就可以跳过下面的*2.1章节*。
### 2.1 安装Ruby
这里用RVM来安装Ruby，因此需要先安装RVM。

- 安装 RVM

	`curl -L https://get.rvm.io | bash -s stable --ruby`

- 安装 Ruby 1.9.3

		rvm install 1.9.3
		rvm use 1.9.3
		rvm rubygems latest
如果安装没有错误，现在执行`ruby --version`输出应该是`ruby 1.9.3p392`。

### 2.2 安装Octopress
		git clone git://github.com/imathis/octopress.git octopress
		cd octopress
		gem install bundler
		bundle install
		rake install
		
---
		
## 3. 部署Octopress到Github
GitHub提供了两种页面类别，一种是针对用户和组织的页面，一种是针对项目的页面。本文只介绍如何部署为用户页面。

要使GitHub的用户页面生效，需要建立一个名为`username.github.io`的Repo（假设你的用户名是：`username`）.Repo建好后，就可以开始部署Octopress了，接下来在Shell下进到Octopress所在路径。

	cd octopress
	rake setup_github_pages
	
执行上面的命令，按提示输入在GitHub上Repo的URL，形如：git@github.com:username/username.github.io.git。
进一步，执行下面的命令，生成静态页面，和将Blog部署到GitHub。

	rake generate
	rake deploy
	
需要注意的是，部署Blog到GitHub，还需要获得GitHub上你的Repo的访问权限。可以通过如下操作获取访问权限：

- 执行`ssh-keygen -t rsa -C "your_email@youremail.com"`
- 然后输入并确认密码，在`/Users/user/.ssh/`目录下会生成id_rsa.pub和id_rsa私钥和公钥文件
- 打开/Users/user/.ssh/id_rsa.pub公钥文件，复制其中的内容
- 到GitHub网址你的Repo。进到“Settings”——>"Depoly Keys"——>"Add deploy key"，将刚才复制的内容粘贴进去，并保存。

至此，Blog就成功的部署到了GitHub空间，在浏览器中打开“username.github.io”便可看到你的Blog。

别忘了把Octopress的代码也同步提交到GitHub，下面的命令将所有代码提交到GitHub上相应Repo的source分支。

	git add .
	git commit -m 'your commit message'
	git push origin source























