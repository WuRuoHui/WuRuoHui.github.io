---
title: GitHub pages 搭建个人博客
layout: post
author: Wu
tags: 学习笔记
---


# GitHub pages 搭建个人博客

- 目录
  - [GitHub](#github)
  - [gitbash](#gitbash)
  - [本地部署](#本地部署)  
  - [写博客](#写博客)
  

## GitHub

#### 创建GitHub账号

<img src="https://i.loli.net/2019/08/13/CGB7Rm45gS1yTuz.png" >

#### 创建GitHub仓库

<img src="https://i.loli.net/2019/08/13/qa7uBrpZRMCzod2.png" >

填写信息

<img src="https://i.loli.net/2019/08/13/5Fz2rGB7lWmTakj.png" >



## gitbash

#### git基础

###### git工作区域

工作区、暂存区、仓库

```
工作区--->暂存区：git add 文件

暂存区--->仓库：git commit -m "描述"
```

每一步都可以使用`git -status`查看状态，最后使用`git push`提交到远程仓库

`git clone 仓库地址`这个命令可以克隆远程仓库到本地

#### git配置([下载地址](https://git-scm.com/))

```
git config --global user.name "username"    //GitHub用户名
git config --global user.email "email"      //GitHub邮箱
git config --list                           //可以查看配置，查看里面的键值对是否正确

cd ~/.ssh                                   //生成ssh令牌
mkdir key_backup
ssh-keygen -t rsa -C "*youremail@address*"
```

<img src="https://i.loli.net/2019/08/13/S9DGr3ct1egiw6b.png" alt="image.png">

`d_rsa.pub`这个文件是等下进行配置要用到的文件，`cat id_rsa.pub`可以显示它的内容，再复制其内容

<img src="https://i.loli.net/2019/08/14/wGnCesPvZli7qFA.png" >

<img src="https://i.loli.net/2019/08/14/bUoP6h9ekj74Iv1.png" >

`ssh -T git@github.com`测试连通状态

<img src="https://i.loli.net/2019/08/14/AlLvdOp1b8DoneQ.png" >

#### GitHub Desktop

通过GitHub Desktop clone自己的个人网站仓库到本地

<img src="https://i.loli.net/2019/08/15/8ratiRlsAPD3hXS.png" >

当本地文件与仓库文件匹配到进行修改时可以上传到远程仓库，避免了繁琐的命令行操作

<img src="https://i.loli.net/2019/08/14/x5y6jCgbIpHEknO.png" >



## 本地部署

#### 安装Rudy

jekyll依赖于Rudy，要先安装[Rudy](http://www.ruby-lang.org/en/downloads/ "下载Rudy")，官网有可能下载速度过慢，可以通过[百度网盘下载](https://pan.baidu.com/s/13t7Nwe3rnRBxI3TNfmU7fg )，提取码：atdu，安装后用`gem`命令查看有没有gem，没有的话需要到[官网](https://rubygems.org/pages/download)下载

<img src="https://i.loli.net/2019/08/15/Qt73HFZkOoESNuW.png" >



##### 安装Jekyll

`使用gem install jekyll-paginate命令安装Jekyll`

<a href="http://jekyllthemes.org" target="_blank" alt="jekyll">jekyll模板</a>这个网站提供了很多模板，可以下载后放在自己克隆到本地仓库的文件夹中，在`cmd`进入该文件夹，执行`bundle exec jekyll s`

<img src="https://i.loli.net/2019/08/15/CcplQufYs7M4B82.png" >

启动成功就可以在浏览器输入`http://localhost:4000/`预览自己下载的模板

#### 配置

要将`_config.yml`配置文件的URL改成自己的个人网站URL，再将本地文件上传到远程仓库，稍等片刻后输入个人网站URL即可看到自己的网站了

<img src="https://i.loli.net/2019/08/15/mM3iXaIlb8ckTDB.png" >

## 写博客

#### MarkDown工具

[Typora](https://typora.io/ "Typora官网")：集写和预览于一身，写的同时可以有预览的效果，不需要分屏查看，所见即所得，支持多种流程图、数学公式等

<img src="https://i.loli.net/2019/08/17/lmIUeXwk2pPbLzT.png" >