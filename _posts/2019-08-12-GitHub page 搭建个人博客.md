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

```flow

op1=>operation: 工作区
op2=>operation: 命令：git add 文件
op3=>operation: 暂存区
op4=>operation: 仓库
op5=>operation: 命令：git commit -m "描述"

op1(right)->op2(right)->op3

```

```flow
op3=>operation: 暂存区
op4=>operation: 仓库
op5=>operation: 命令：git commit -m "描述"
op3(right)->op5(right)->op4
```

每一步都可以使用`git -status`查看状态，最后使用`git push`提交到远程仓库

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

<img src="https://i.loli.net/2019/08/14/x5y6jCgbIpHEknO.png" >

安装Rudy

##### 

<a href="http://jekyllthemes.org" target="_blank" alt="jekyll">jekyll模板</a>