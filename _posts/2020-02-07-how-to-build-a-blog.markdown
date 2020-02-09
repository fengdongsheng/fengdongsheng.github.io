---
layout: post
title:  "使用jekyll和github page 搭建博客"
date:   2020-02-07 16:37:36
categories:  博客
---

* content
{:toc}


## 简介

第一篇博客，刚刚搭建好jekyll，就粗略写一下。后面补充细节。


## 博客环境的搭建

整个过程前后算下来得有整整一天，看了很多帖子，走了不少弯路。建议在参考其他人的blog时注意一下别人的blog创建时间，
因为很可能他们记录的东西，在软件版本更新后，没有多少参考价值了。整个过程大致就两步：①github部分、②jekyll部分。

### github 仓库

①、github部分分为创建远程仓库、配置本地git环境、配置本地和远程的密钥、创建本地仓库。这些步骤完成后可以去jekyll主题官网下载blog模板，然后git常规操作：add、push可以在通过username.github.io访问效果。

### jekyll

②、jekyll部分最简单但是耽误了最多时间。jekyll的前置环境是ruby，大部分blog都将ruby和devkit分开装的，并且不区分ruby和devkit之间的版本匹配，这使得我尝试了多次都出现了gem本地扩展错误的问题。找到了版本匹配的，却依然出现相同问题（怀疑是版本太低了）。在[rubyinstall](https://rubyinstaller.org/downloads/)官网中有两大类，一类是不包含devkit的exe，一类是包含devkit的exe。如果选择了没有devkit的，会依然出现gem扩展问题，别想着去找单独的devkit，然后安装，因为找不到，找到的就是适配低版本的，然后发现还是同样的错误。
    最后怎么解决？直接选择rubyinstall官网上含devkit的exe，运行安装的exe，勾选所有的选项。等一会儿，会在cmd中出现三个可选项，要选第三个，完成后，运行ruby-v确保无误。然后有一步，安装rubygames，这个可以自行baidu、google，可以运行gem -v以确保完成。最后一步，安装jekyll，gem install jekyll，运行jekyll -v确保完成。

## jekyll的使用

      创建文件：jekyll new name（可能会有点久）
      在同一目录下使用 jekyll s,然后可以在浏览器输入localhost：4000，查看效果

## 其它

      可以在powershell中完成整个过程；安装ruby时尽量不要有中文路径，默认安装在c盘挺好。
      在修改了_post中的md文件后，提交到github可能会在邮箱收到有‘seo’的错误，将指定文件中的对应代码行删除即可。
      再次提交，如果出现，github page不支持主题的错误，通过注释config文件中的theme: plainwhite即可。
      可能还会在jekyll build的时候出现：future date的问题，需要在config文件中添加future：true
      win10 power shell 打开方式：win+x，选择power shell；
      在写markdown的时候注意符号都是英文才对。
      