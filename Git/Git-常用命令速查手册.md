---
title: Git 常用命令速查手册
date: 2018-09-12 09:48:00 +0800
categories: Git 常用命令 速查手册
---

# 目录
* [写作的目的](#写作的目的)
* [针对人群](#针对人群)
* [Git 命令](#git-命令)
    * [Git 配置](#Git-配置)
    * [创建仓库](#创建仓库)
    * [本地文件操作](#本地文件操作)
    * [提交更改](#提交更改)
    * [提交历史](#提交历史)
    * [分支](#分支)
    * [标签](#标签)
    * [代码冲突](#代码冲突)
    * [暂存](#暂存)
    * [远端仓库](#远端仓库)
    * [撤销](#撤销)
    * [子模块](#子模块)
* [Git 工作流](#Git-工作流)
    * [1. 删除远程分支的一次错误提交](#1-删除远程分支的一次错误提交)
    * [2. 添加项目的部分文件（目录）到指定的分支](#2-添加项目的部分文件目录到指定的分支)
    * [3. 提交时提示本地分支晚于远程分支](#3-提交时提示本地分支晚于远程分支)
    * [4. 删除错误提交到远端仓库的文件](#4-删除错误提交到远端仓库的文件)
* [Git 常见错误](#Git%20常见错误)

# 写作的目的

在实际的工作中，可能会有相关命令查询的需求，但阅读相关文档太花时间，且不明确，本文将对 Git 相关的常用命令进行汇总整理，简要说明用途，便于查找。  

# 针对人群

本文主要以查询手册为出发点，对 Git 常用命令进行整理，本文默认你已经了解 Git 版本控制，并会使用。如果你对以上所述还不了解，或是还为接触过 Git 版本控制可以去查看相关资料进一步学习，这篇文章不适合你。  

# Git 命令
 
`git --version` 查看 Git 版本  

`git --help` 查看帮助  
`-a/--all` 显示全部 Git 命令  
`<Git 命令>` 显示相关命令的手册页  

## Git 配置

`git config`  
您可以使用此命令查询/设置/替换/取消设置选项。名称实际上是由点分隔的部分和键，值将被转义。  
`--system` 系统配置  
`--global` 当前账户配置   
`-f, --file <file>` 指定配置文件  
`--local`(默认值) 当前仓库配置

`--replace-all` 全部替换，默认只会替换一行，次命令将会替换所有匹配的项  
`--add` 新增一项，这将添加一项，而不会改变任何已有的项  
`--get` 获取给定键的值（可选地通过与值匹配的正则表达式进行过滤）。如果未找到密钥，则返回错误代码1;如果找到多个密钥值，则返回最后一个值。  
`--get-all` 返回所有值  
`--get-regexp` 将名称解释为正则表达式并写出键名。正则表达式匹配当前区分大小写，并且针对键的规范化版本完成，其中段和变量名称是小写的，但子段名称不是。  
`--remove-section` 从配置文件中删除给定的部分  
`--rename-section` 将给定部分重命名为新名称  
`--unset` 从配置文件中删除与键匹配的行  
`--unset-all` 从配置文件中删除与键匹配的所有行  
`-l/--list` 列出配置文件中设置的所有变量及其值  
`--type <type>` git config将确保任何输入或输出在给定的类型约束下有效，并将以`<type>`规范形式规范化传出值。

有效`<type>`的包括：
* `bool`：将值规范化为“true”或“false”。
* `int`：将值规范化为简单的十进制数。可选的k，m或g后缀 将使该值在输入时乘以1024,1048576或1073741824。
* `bool-or-int`：根据bool或int规范化，如上所述。
* `path`：通过添加领先。规范化~，它的值$HOME和 ~user主目录为指定的用户。设置值时，此说明符无效（但您可以git config section.variable ~/从命令行使用shell来执行扩展。）
* `expiry-date`：通过从固定或相对日期字符串转换为时间戳来进行规范化。设置值时，此说明符无效。
* `color`：获取值时，通过转换为ANSI颜色转义序列进行规范化。设置值时，将执行完整性检查以确保给定值可以作为ANSI颜色进行规范化，但它按原样编写。

`--no-type` 取消设置先前设置的类型说明符（如果之前已设置）。此选项请求git config不规范化检索到的变量。  
`-z/--null` 对于输出值和/或键的所有选项，始终使用空字符（而不是换行符）结束值。使用换行符作为键和值之间的分隔符。这允许安全地解析输出而不会例如通过包含换行符的值混淆。  
`-e/--edit` 打开编辑器以修改指定的配置文件  
 

出错时，此命令将失败并显示非零状态。一些退出代码是：
1. 部分或键无效（ret = 1），
2. 没有提供部分或名称（ret = 2），
3. 配置文件无效（ret = 3），
4. 配置文件无法写入（ret = 4），
5. 你试图取消一个不存在的选项（ret = 5），
6. 您尝试取消设置/设置多行匹配的选项（ret = 5），或
7. 您尝试使用无效的正则表达式（ret = 6）。

成功时，该命令返回退出代码0。

### Git 配置常用命令

`git config --global user.name "<name>"` 设置要附加到提交事务的名称  
`git config --global user.email "<email address>"` 设置要附加到提交事务的电子邮件  
`git config --global color.ui auto` 启用命令行输出的有用颜色  

 ## 创建仓库

`git init` 创建新本地仓库  
`git init <project-name>` 创建具有指定名称的新本地仓库  
`git clone <url>` 克隆仓库  
`git clone --recurse-submodules <url>`以递归方式克隆现有仓库及其所有子模块  

## 本地文件操作

`git status` 列出要提交的所有新文件或已修改文件  
`git diff` 显示尚未暂存的文件差异  
`git diff [first-branch]...[second-branch]` 显示两个分支之间的内容差异  
`git add <file>` 将文件中的所有当前更改添加到下一个提交  
`git add .` 将所有当前更改添加到下一个提交  
`git add -p <file>` 以交互方式将更改添加到下一个提交  
`git mv <file> <new file name>` 重命名文件并将其添加到下一个提交  
`git rm <file>` 删除文件并将其添加到下一个提交   
`git rm --cached <file>` 从版本控制中删除该文件，但在本地保留该文件   
`git ls-files --other --ignored --exclude-standard` 列出此项目中所有被忽略的文件  
 

## 提交更改

`git commit -m "<descriptive message>"` 在版本历史记录中永久记录文件快照  
`git commit -a` 提交跟踪文件中的所有本地更改,相当于运行 git add 把所有当前目录下的文件加入暂存区域再运行。git commit  
`git commit --amend` 修改最近一次提交  

## 提交历史

`git log` 显示所有提交历史  
`git log -p <file>` 显示特定文件随时间的变化  
`git log --author=<committer name>` 显示特定提交者随时间的变化  
`git log --pretty` 指定使用完全不同于默认格式的方式展示提交历史  
* `oneline` 将每个提交放在一行显示
* `format` 可以定制要显示的记录格式  

`format` 常用的格式占位符写法及其代表的意义

| 选项   | 说明
| :---- | :----------------------------- |
| %H	| 提交对象（`commit`）的完整哈希字串
| %h	| 提交对象的简短哈希字串
| %T	| 树对象（`tree`）的完整哈希字串
| %t	| 树对象的简短哈希字串
| %P	| 父对象（`parent`）的完整哈希字串
| %p	| 父对象的简短哈希字串
| %an	| 作者（`author`）的名字
| %ae	| 作者的电子邮件地址
| %ad	| 作者修订日期（可以用`-date=`定制格式）
| %ar	| 作者修订日期，按多久以前的方式显示
| %cn	| 提交者(`committer`)的名字
| %ce	| 提交者的电子邮件地址
| %cd	| 提交日期
| %cr	| 提交日期，按多久以前的方式显示
| %s	| 提交说明

`--pretty` 常用的选项及其释义

| 选项	         | 说明
| :------------ | :------------------------ |
| `-p`	        | 按补丁格式显示每个更新之间的差异
| `--word-diff`	| 按 word diff 格式显示差异
| `--stat`	    | 显示每次更新的文件修改统计信息
| `--shortstat`	| 只显示`--stat`中最后的行数修改添加移除统计
| `--name-only`	| 在提交信息后显示已修改的文件清单
| `--name-status`| 显示新增、修改、删除的文件清单
| `--abbrev-commit`| 仅显示`SHA-1`的前几个字符，而非所有的`40`个字符
| `--relative-date`| 使用较短的相对时间显示
| `--graph`	     | 显示`ASCII`图形表示的分支合并历史
| `--pretty`	 | 使用其他格式显示历史提交信息。可用的选项包括 oneline，short，full，fuller 和 format（后跟指定格式）
| `--oneline`	 | `--pretty=oneline --abbrev-commit` 的简化用法

限制输出长度

| 选项	             | 说明
| :-------------------- | :----------------- |
| `-(n)`	            | 仅显示最近的 n 条提交
| `--since, --after`    | 仅显示指定时间之后的提交
| `--until`, `--before` | 仅显示指定时间之前的提交
| `--author`	        | 仅显示指定作者相关的提交
| `--committer`	        | 仅显示指定提交者相关

`git log --grep=<string>` 搜索（grep）提交给定字符串的消息  
`git blame <file>` 谁在何时更改了文件中的那些内容  
`git show [commit]` 输出指定提交的元数据和内容更改  

 **几种不错的提交历史显示格式：**  
* `git log --pretty=format:"%h - %an, %ar : %s"`
* `git log --pretty=format:"%h %s" --graph`

 ## 分支  

`git branch` 列出当前存储库中的所有本地分支  
`git branch <branch-name>` 创建一个新分支  
`git checkout <branch-name>` 切换到指定的分支并更新工作目录  
`git checkout <branch-name>` 切换HEAD分支  
`git branch --track <new-branch> <remote-branch>` 基于远程分支创建新的跟踪分支  
`git merge <branch>` 将指定分支的历史记录合并到当前分支中  
`git merge --abort` 取消合并  
 
`git branch -d <branch-name>` 删除一个分支  
`git push origin --delete <branch>` 删除远程分支  
`git branch -m <old name> <new name>` 在本地重命名分支  
`git push <remote> :<old name>` 
`git push <remote> <new name>`
重命名远程分支  

## 标签   

`git tag <tag-name>` 标记当前提交  
`git push --tags` 发布标签  

## 代码冲突  

`git rebase <branch>` 将当前的HEAD重新定位到分支上  
`git rebase --abort` 中止一个篮板  
`git rebase --continue` 解决冲突后继续改造  
`git mergetool` 使用配置的合并工具解决冲突  
`git add <resolved-file>` 
`git rm <resolved-file>`
使用编辑器手动解决冲突并将文件标记为已解决  

## 暂存  

`git stash` 隐藏存储更改  
`git stash pop` 删除并应用隐藏的更改  
`git stash list` 列出所有隐藏的变更集  
`git stash drop` 丢弃最近隐藏的变更集  

## 远端仓库  

`git remote -v` 列出所有当前配置的远端仓库  
`git remote show <remote>` 显示远端仓库信息  
`git remote add <remote> <url>` 添加新的远端仓库  
`git remote rename <old-name> <new-name>` 重命名一个远端仓库  
`git fetch <remote>` 从远程下载所有更改，但不要合并到HEAD中  
`git fetch -p <remote>` 从远程下载所有更改，但不要合并到HEAD并从源中清除已删除的分支  
`git pull <remote> <branch>` 下载更改并直接合并到HEAD  
`git push <remote> <branch>` 在远程上发布本地更改  
`git remote add --track <remote-branch> <remote> <url>` 跟踪远程存储库  
  
## 撤销  

`git reset --hard HEAD` 放弃工作目录中的所有本地更改  
`git reset [commit]` 在[commit]之后撤消所有提交，在本地保留更改  
`git reset --hard [commit]` 丢弃所有历史记录并更改回指定的提交  
`git checkout HEAD <file>` 放弃特定文件中的本地更改  
`git revert <commit>` 通过提供具有相反更改的新提交来还原提交
`git checkout <commit> <file>` 从先前的提交中还原特定文件  

将HEAD指针重置为先前的提交
* `git reset --hard <commit>` 放弃本地更改  
* `git reset <commit>` 将所有更改保留为未分级更改  
* `git reset --keep <commit>` 保留未提交的本地更改  

## 子模块  

### 进行更改，提交和签出子模块文件  
只需转到子模块目录并像往常一样使用git  

`git submodule` / `git submodule status` 列出所有当前配置的子模块  
`git remote show <remote>` 显示子模块信息  

### 新增子模块  
请注意您选择的子模块名称：如果使用正斜杠（/），git会认为您要删除子模块并希望添加子模块目录中的所有文件。请不要在子模块名称后面使用正斜杠。  
1. 执行 `git submodule add -b <branch> --name <name> <repository-path-or-url>`
2. 将 `.gitmodule` 文件和子模块文件夹添加到上层项目索引中  
3. 提交上层项目上的两个文件  

### 删除子模块
1. 从`.gitmodules` 文件中删除相关行  
2. 从 `.git/config` 中删除相关部分
3. 执行 `git rm --cached <submodule-path> (no trailing slash)`
4. 提交上层项目
5. 删除现在未跟踪的子模块文件

### 克隆一个带有子模块的项目
`git clone --recurse-submodules ssh://user@domain.tld/repo.git`
或
1. 向往常一样克隆项目
2. 执行 `git submodule init` 初始化子模块
3. 运行 `git submodule update` 让子模块在分离的HEAD上

`git diff --submodule` 查看子模块的所有变更  
`git submodule update --remote`将子模块更新为其各自分支上的最新更改  
`git submodule update --remote <submodule-name>` 将特定子模块更新为其分支上的最新更改  
`git push --recurse-submodules=check` 仅当同时推送所有子模块时，才将更改推送到上层项目  
`git push --recurse-submodules=on-demand` 将更改推送到子模块，然后推送上层项目更改  
`git submodule foreach '<arbitrary-command-to-run>'` 在每个子模块上运行任意命令  


# Git 工作流

## 1. 删除远程分支的一次错误提交  

> 删除已经提交的内容的操作较为危险，任何时候都不推荐使用

（1）git reset commitId，(注：不要带--hard)到上个版本  
（2）git stash，暂存修改  
（3）git push --force, 强制push,远程的最新的一次commit被删除  
（4）git stash pop，释放暂存的修改，开始修改代码  
（5）git add . -> git commit -m "massage" -> git push  
或（这种操作有同时导致本地修改丢失的风险）  
（1）git reset --hard HEAD~1  
（2）git push --force 将本次变更强行推送至服务器。这样在服务器上的最后一次错误提交也彻底消失了。  

## 2. 添加项目的部分文件(目录)到指定的分支

前提条件：要添加的文件已存在并且不能被 gitignore 屏蔽  
(1) 删除相应远程分支（如果存在）:`git push origin --delete <branch>`  
(2) 将文件推送到指定的远程分支：`git subtree push --prefix=<file> origin <branch>` 

`<file>`:文件名/目录名  
`<branch>`:分支名，未建立，会在提交时自动建立,一般为 `gh-pages` (推荐)

## 3. 提交时提示本地分支晚于远程分支

`git remote add origin <远程仓库地址>`  
`git fetch origin` //获取远程更新   
`git merge origin/master` //把更新的内容合并到本地分支  

之后就可以正常提交了

## 4. 删除错误提交到远端仓库的文件
```shell
git rm --cached <file-name> 
git commit -m "delete file"  
git push
```

# Git 常见错误

[常见错误及解决方案(CSDN)](https://blog.csdn.net/u011323949/article/details/82629802)


---
> 参考链接  
>  [GIT CHEAT SHEET](https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf)  
> [图解 Git](http://marklodato.github.io/visual-git-guide/index-zh-cn.html#diff)  
> [Git](https://kapeli.com/cheat_sheets/Git.docset/Contents/Resources/Documents/index)




