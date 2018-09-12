---
title: Git
date: 2018-08-30 09:45:00 +0800
categories: Git 版本控制
---

> Git 是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。
Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。
Git 与常用的版本控制工具 CVS, Subversion 等不同，它采用了分布式版本库的方式，不必服务器端软件支持。

[Git 常用命令速查手册](https://github.com/ChanMenglin/NoteBook/blob/master/Git/Git%20常用命令速查手册.md)  
本文主要以查询手册为出发点，对 Git 常用命令进行整理，本文默认你已经了解 Git 版本控制，并会使用。如果你对以上所述还不了解，或是还为接触过 Git 版本控制可以去查看相关资料进一步学习，你可以阅读以下 **Git 详解** 的内容。

Git 详解  

* [安装 Git](https://github.com/ChanMenglin/NoteBook/blob/master/Git/1.%20Git%20安装.md#安装-git)
    * [从源代码安装](https://github.com/ChanMenglin/NoteBook/blob/master/Git/1.%20Git%20安装.md#1-从源代码安装)
    * [在 Linux 上安装](https://github.com/ChanMenglin/NoteBook/blob/master/Git/1.%20Git%20安装.md#2-在-linux-上安装)
    * [在 Mac 上安装](https://github.com/ChanMenglin/NoteBook/blob/master/Git/1.%20Git%20安装.md#3-在-mac-上安装)
    * [在 Windows 上安装](https://github.com/ChanMenglin/NoteBook/blob/master/Git/1.%20Git%20安装.md#4-在-windows-上安装)

* [Git 首次使用前的配置](https://github.com/ChanMenglin/NoteBook/blob/master/Git/2.%20Git%20首次使用前的配置.md#初次运行-git-前的配置)
    * [用户信息](https://github.com/ChanMenglin/NoteBook/blob/master/Git/2.%20Git%20首次使用前的配置.md#1-用户信息)
    * [文本编辑器](https://github.com/ChanMenglin/NoteBook/blob/master/Git/2.%20Git%20首次使用前的配置.md#2-文本编辑器)
    * [差异分析工具](https://github.com/ChanMenglin/NoteBook/blob/master/Git/2.%20Git%20首次使用前的配置.md#3-差异分析工具) 

* [Git 基本用法](https://github.com/ChanMenglin/NoteBook/blob/master/Git/3.%20Git%20基本用法.md#git-基本用法)
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
* [服务器上的 Git](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#服务器上的-git)
    * [协议](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#1-协议)
        <!-- * [本地协议](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#1-本地协议)
        * [SSH 协议](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#2-ssh-协议)
        * [Git 协议](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#3-git-协议)
        * [HTTP/S 协议](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#4-http/s-协议) -->
    * [在服务器上部署 Git](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#2-在服务器上部署-git)
        <!-- * [把裸仓库移到服务器上](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#1-把裸仓库移到服务器上)
        * [小型安装](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#2-小型安装) -->
    * [生成 SSH 公钥](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#3-生成-ssh-公钥)
    * [架设服务器](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#4-架设服务器)
    * [公共访问](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#5-公共访问)
    * [GitWeb](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#6-gitweb)
    * [Gitosis](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#7-gitosis)
    * [Gitolite](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#8-gitolite)
    * [Git 守护进程](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#9-git-守护进程)
    * [Git 托管服务](https://github.com/ChanMenglin/NoteBook/blob/master/Git/4.%20Git%20服务器.md#10-git-托管服务)
* [Git 在实际工作中的使用](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#分布式-git)
    * [分布式工作流程](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#1-分布式工作流程)
        <!-- * [集中式工作流](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#1-集中式工作流)
        * [集成管理员工作流](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#2-集成管理员工作流)
        * [司令官与副官工作流](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#3-司令官与副官工作流) -->
    * [为项目作贡献](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#2-为项目作贡献)
    * [项目的管理](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#3-项目的管理)
        <!-- * [使用特性分支进行工作](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#1-使用特性分支进行工作)
        * [采纳来自邮件的补丁](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#2-采纳来自邮件的补丁)
        * [检出远程分支](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#3-检出远程分支)
        * [决断代码取舍](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#4-决断代码取舍)
        * [代码集成](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#5-代码集成)
        * [给发行版签名](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#6-给发行版签名)
        * [生成内部版本号](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#7-生成内部版本号)
        * [准备发布](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#8-准备发布)
        * [制作简报](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#9-制作简报) -->
* [Git 工具](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#git-工具)
    * [修订版本（Revision）选择](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#1-修订版本revision选择)
    * [交互式暂存](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#2-交互式暂存)
    * [储藏（Stashing）](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#3-储藏stashing)
    * [重写历史](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#4-重写历史)
    * [使用 Git 调试](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#5-使用-git-调试)
    * [子模块](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#6-子模块)
    * [子树合并](https://github.com/ChanMenglin/NoteBook/blob/master/Git/5.%20Git%20在实际工作中的使用.md#7-子树合并)
* [自定义 Git](https://github.com/ChanMenglin/NoteBook/blob/master/Git/6.%20自定义%20Git.md#自定义-git)
    * [配置 Git](https://github.com/ChanMenglin/NoteBook/blob/master/Git/6.%20自定义%20Git.md#1-配置-git)
    * [Git 属性](https://github.com/ChanMenglin/NoteBook/blob/master/Git/6.%20自定义%20Git.md#2-git-属性)
    * [Git 挂钩](https://github.com/ChanMenglin/NoteBook/blob/master/Git/6.%20自定义%20Git.md#3-git-挂钩)
    * [Git 强制策略实例](https://github.com/ChanMenglin/NoteBook/blob/master/Git/6.%20自定义%20Git.md#4-git-强制策略实例)
* [Git 与其它系统](https://github.com/ChanMenglin/NoteBook/blob/master/Git/7.%20Git%20与其它系统.md#git-与其他系统)
    * [Git 与 Subversion](https://github.com/ChanMenglin/NoteBook/blob/master/Git/7.%20Git%20与其它系统.md#1-git-与-subversion)
    * [迁移到 Git](https://github.com/ChanMenglin/NoteBook/blob/master/Git/7.%20Git%20与其它系统.md#2-迁移到-git)
* [Git 内部原理](https://github.com/ChanMenglin/NoteBook/blob/master/Git/8.%20Git%20内部原理.md#git-内部原理)
    * [底层命令 (Plumbing) 和高层命令 (Porcelain)](https://github.com/ChanMenglin/NoteBook/blob/master/Git/8.%20Git%20内部原理.md#1-底层命令-plumbing-和高层命令-porcelain)
    * [Git 对象](https://github.com/ChanMenglin/NoteBook/blob/master/Git/8.%20Git%20内部原理.md#2-git-对象)
    * [Git References](https://github.com/ChanMenglin/NoteBook/blob/master/Git/8.%20Git%20内部原理.md#3-git-references)
    * [Packfiles](https://github.com/ChanMenglin/NoteBook/blob/master/Git/8.%20Git%20内部原理.md#4-packfiles)
    * [The Refspec](https://github.com/ChanMenglin/NoteBook/blob/master/Git/8.%20Git%20内部原理.md#5-the-refspec)
    * [传输协议](https://github.com/ChanMenglin/NoteBook/blob/master/Git/8.%20Git%20内部原理.md#6-传输协议)
    * [维护及数据恢复](https://github.com/ChanMenglin/NoteBook/blob/master/Git/8.%20Git%20内部原理.md#7-维护及数据恢复)

<!--

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
> [GitHub Cheat Sheet](https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf) (PDF)  |  [Visual Git Cheat Sheet](http://ndpsoftware.com/git-cheatsheet.html) (SVG | PNG)   
> 来源 [git](https://git-scm.com/docs)

---
> 参考链接  
> [Git 官网](https://git-scm.com)  
> [Git Github仓库](https://github.com/git/git)  
> [Git](https://kapeli.com/cheat_sheets/Git.docset/Contents/Resources/Documents/index)  
> [图解 Git](http://marklodato.github.io/visual-git-guide/index-zh-cn.html#basic-usage)  
> [Pro Git](http://iissnan.com/progit/)  
> [Git 教程](http://www.runoob.com/git/git-tutorial.html)  
> [git - 简易指南](http://www.bootcss.com/p/git-guide/)  
