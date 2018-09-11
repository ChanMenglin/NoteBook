---
title: Git
date: 2018-08-30 09:45:00 +0800
categories: Git 版本控制
---

> Git 是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。
Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。
Git 与常用的版本控制工具 CVS, Subversion 等不同，它采用了分布式版本库的方式，不必服务器端软件支持。

1. [安装 Git](https://github.com/ChanMenglin/NoteBook/blob/master/Git/1.%20Git%20安装.md#安装-git)
    * [从源代码安装](https://github.com/ChanMenglin/NoteBook/blob/master/Git/1.%20Git%20安装.md#1-从源代码安装)
    * [在 Linux 上安装](https://github.com/ChanMenglin/NoteBook/blob/master/Git/1.%20Git%20安装.md#2-在-linux-上安装)
    * [在 Mac 上安装](https://github.com/ChanMenglin/NoteBook/blob/master/Git/1.%20Git%20安装.md#3-在-mac-上安装)
    * [在 Windows 上安装](https://github.com/ChanMenglin/NoteBook/blob/master/Git/1.%20Git%20安装.md#4-在-windows-上安装)

2. [Git 首次使用前的配置](https://github.com/ChanMenglin/NoteBook/blob/master/Git/2.%20Git%20首次使用前的配置.md#初次运行-git-前的配置)
    * [用户信息](https://github.com/ChanMenglin/NoteBook/blob/master/Git/2.%20Git%20首次使用前的配置.md#1-用户信息)
    * [文本编辑器](https://github.com/ChanMenglin/NoteBook/blob/master/Git/2.%20Git%20首次使用前的配置.md#2-文本编辑器)
    * [差异分析工具](https://github.com/ChanMenglin/NoteBook/blob/master/Git/2.%20Git%20首次使用前的配置.md#3-差异分析工具) 

3. [Git 基本用法](https://github.com/ChanMenglin/NoteBook/blob/master/Git/3.%20Git%20基本用法.md#git-基本用法)
    * [查看帮助](https://github.com/ChanMenglin/NoteBook/blob/master/Git/3.%20Git%20基本用法.md#1-查看帮助)
    * [取得项目的 Git 仓库](https://github.com/ChanMenglin/NoteBook/blob/master/Git/3.%20Git%20基本用法.md#2-取得项目的-git-仓库)
    * [记录每次更新到仓库](https://github.com/ChanMenglin/NoteBook/blob/master/Git/3.%20Git%20基本用法.md#3-记录每次更新到仓库)
    * [提交更新](https://github.com/ChanMenglin/NoteBook/blob/master/Git/3.%20Git%20基本用法.md#4-提交更新)
    * [查看提交历史](https://github.com/ChanMenglin/NoteBook/blob/master/Git/3.%20Git%20基本用法.md#5-查看提交历史)
    * [撤销操作](https://github.com/ChanMenglin/NoteBook/blob/master/Git/3.%20Git%20基本用法.md#6-撤销操作)
    * [远程仓库的使用](https://github.com/ChanMenglin/NoteBook/blob/master/Git/3.%20Git%20基本用法.md#7-远程仓库的使用)
    * [打标签](https://github.com/ChanMenglin/NoteBook/blob/master/Git/3.%20Git%20基本用法.md#8-打标签)
    * [Git 实用技巧](https://github.com/ChanMenglin/NoteBook/blob/master/Git/3.%20Git%20基本用法.md#git-实用技巧)
4. [Git 分支](https://github.com/ChanMenglin/NoteBook/blob/master/Git/3.%20Git%20基本用法.md#git-分支)
    * [分支的基本操作](https://github.com/ChanMenglin/NoteBook/blob/master/Git/3.%20Git%20基本用法.md#1-分支的基本操作)
    * [利用分支进行开发的流程](https://github.com/ChanMenglin/NoteBook/blob/master/Git/3.%20Git%20基本用法.md#2-利用分支进行开发的流程)
    * [远程分支](https://github.com/ChanMenglin/NoteBook/blob/master/Git/3.%20Git%20基本用法.md#3-远程分支)
    * [分支的衍合](https://github.com/ChanMenglin/NoteBook/blob/master/Git/3.%20Git%20基本用法.md#4-分支的衍合)
5. [服务器上的 Git](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#服务器上的-git)
    * [协议](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#1-协议)
    * [在服务器上部署 Git](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#2-在服务器上部署-git)
    * [生成 SSH 公钥](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#3-生成-ssh-公钥)
    * [架设服务器](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#4-架设服务器)
    * [公共访问](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#5-公共访问)
    * [GitWeb](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#6-gitweb)
    * [Gitosis](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#7-gitosis)
    * [Gitolite](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#8-gitolite)
    * [Git 守护进程](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#9-git-守护进程)
    * [Git 托管服务](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#10-git-托管服务)


<!--

4. 服务器上的 Git

架设一台 Git 服务器并不难。第一步是选择与服务器通讯的协议。远程仓库通常只是一个裸仓库（bare repository） — 即一个没有当前工作目录的仓库。因为该仓库只是一个合作媒介，所以不需要从硬盘上取出最新版本的快照；仓库里存放的仅仅是 Git 的数据。简单地说，裸仓库就是你工作目录中 `.git` 子目录内的内容。


5. Git 在实际工作中的使用

利用 Git 来组织和完成分布式工作流程。  


6. 自定义 Git  

7. Git 与其他系统  

Git 最为重要的特性之一是名为 `git svn` 的 Subversion 双向桥接工具。该工具把 Git 变成了 Subversion 服务的客户端，从而让你在本地享受到 Git 所有的功能，而后直接向 Subversion 服务器推送内容，仿佛在本地使用了 Subversion 客户端。也就是说，在其他人忍受古董的同时，你可以在本地享受分支合并，使暂存区域，衍合以及 单项挑拣等等。  



8. Git 内部原理  

由于这些内容对于初学者来说可能难以理解且过于复杂。你在学习过程中可以先阅读这部分，也可以晚点阅读这部分，这完全取决于你自己。  

既然已经读到这了，就让我们开始吧。首先要弄明白一点，从根本上来讲 Git 是一套内容寻址 (content-addressable) 文件系统，在此之上提供了一个 VCS 用户界面。  





# 约定


# 命令详解

## Diff

## Commit

## Checkout

## Detached HEAD(匿名分支提交)

## Reset

## Merge

## Cherry Pick

## Rebase

# 技术说明
-->

---
> 参考链接  
> [Git 官网](https://git-scm.com)  
> [Git Github仓库](https://github.com/git/git)  
> [Git](https://kapeli.com/cheat_sheets/Git.docset/Contents/Resources/Documents/index)  
> [图解 Git](http://marklodato.github.io/visual-git-guide/index-zh-cn.html#basic-usage)  
> [Pro Git](http://iissnan.com/progit/)  
> [Git 教程](http://www.runoob.com/git/git-tutorial.html)  
> [git - 简易指南](http://www.bootcss.com/p/git-guide/)  
