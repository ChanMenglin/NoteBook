---
title: Git
date: 2018-08-30 09:45:00 +0800
categories: Git 版本控制
---

> Git是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。
Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。
Git 与常用的版本控制工具 CVS, Subversion 等不同，它采用了分布式版本库的方式，不必服务器端软件支持。

# 安装 Git

要使用 Git 就要先安装它，以下我们使用多种方式进行安装，你只需要选择最适合你的方式即可。

## 1. 从源代码安装

若是条件允许，从源代码安装有很多好处，至少可以安装最新的版本。Git 的每个版本都在不断尝试改进用户体验，所以能通过源代码自己编译安装最新版本就再好不过了。有些 Linux 版本自带的安装包更新起来并不及时，所以除非你在用最新的 distro 或者 backports，那么从源代码安装其实该算是最佳选择。

Git 的工作需要调用 curl，zlib，openssl，expat，libiconv 等库的代码，所以需要先安装这些依赖工具。在有 yum 的系统上（比如 Fedora）或者有 apt-get 的系统上（比如 Debian 体系），可以用下面的命令安装：
```sh
$ yum install curl-devel expat-devel gettext-devel \ openssl-devel zlib-devel

$ apt-get install libcurl4-gnutls-dev libexpat1-dev gettext \ libz-dev libssl-dev
```
从下面的 Git 官方站点下载最新版本源代码：  
http://git-scm.com/download

然后编译并安装
```shell
$ tar -zxf git-1.7.2.2.tar.gz
$ cd git-1.7.2.2
$ make prefix=/usr/local all
$ sudo make prefix=/usr/local install
```
现在已经可以用 `git` 命令了.

## 2. 在 Linux 上安装

要在 Linux 上安装预编译好的 Git 安装包，可以直接用系统提供的包管理工具。在 Fedora 上用 yum 安装：
```shell
$ yum install git-core
```
在 Ubuntu 这类 Debian 体系的系统上，可以用 apt-get 安装：
```
$ apt-get install git
```

## 3. 在 Mac 上安装

在 Mac 上安装 Git 有两种方式：
1. 图形化 Git 安装工具  
http://sourceforge.net/projects/git-osx-installer/
2. 命令行安装
    1. [MacPorts](http://www.macports.org) 安装，安装 MacPorts 后，使用 `$ sudo port install git-core +svn +doc +bash_completion +gitweb` 命令安装 Git
    2. [homebrew](https://github.com/mxcl/homebrew) 安装，安装 homebrew 后，使用 `brew install git` 安装 Git  

    使用命令行安装的方法有很多，大家可以根据自己所使用的工具进行安装。
> 目前 Mac 已自带 Git

## 4. 在 Windows 上安装

 Windows 上可以使用 [git for windows](https://gitforwindows.org) 安装 Git 
 > 给 Windows 用户的敬告：你应该在 msysGit 提供的 Unix 风格的 shell 来运行 Git。在 Unix 风格的 shell 中，可以使用本书中提及的复杂多行的命令。对于那些需要在 Windows 命令行中使用 Git 的用户，必须注意：在参数中间有空格的时候，必须使用双引号将参数括起来（在 Linux 中是单引号）；另外，如果扬抑符（^）作为参数的结尾，并且作为这一行的最后一个字符，则这个参数也需要用双引号括起来。因为扬抑符在 Windows 命令行中表示续行（译注：即下一行为这一行命令的继续）。

# 初次运行 Git 前的配置

一般在新的系统上，我们都需要先配置下自己的 Git 工作环境。配置工作只需一次，以后升级时还会沿用现在的配置。当然，如果需要，你随时可以用相同的命令修改已有的配置。

Git 提供了一个叫做 `git config` 的工具,专门用来配置或读取相应的工作环境变量。而正是由这些环境变量，决定了 Git 在各个环节的具体工作方式和行为。这些变量可以存放在以下三个不同的地方：
* `/etc/gitconfig` 文件：系统中对所有用户都普遍适用的配置。若使用 `git config` 时用 `--system` 选项，读写的就是这个文件。
* `~/.gitconfig` 文件：用户目录下的配置文件只适用于该用户。若使用 `git config` 时用 `--global` 选项，读写的就是这个文件。
* 当前项目的 Git 目录中的配置文件（也就是工作目录中的 `.git/config` 文件）：这里的配置仅仅针对当前项目有效。每一个级别的配置都会覆盖上层的相同配置，所以 `.git/config` 里的配置会覆盖 `/etc/gitconfig` 中的同名变量。

## 1. 用户信息

个人的用户名称和电子邮件地址，每次 Git 提交时都会引用这两条信息，说明是谁提交了更新，会随更新内容一起被永久纳入历史记录：
```shell
$ git config --global user.name "<姓名>"
$ git config --global user.email <邮件地址>
```
> 如果不使用 `--global` 则只对当前项目有效

## 2. 文本编辑器

设置默认使用的文本编辑器。Git 需要你输入一些额外消息的时候，会自动调用一个外部文本编辑器给你用，默认会使用操作系统指定的默认编辑器。
```shell
$ git config --global core.editor <文本编辑器>
```
## 3. 差异分析工具

设置差异分析工具，在解决合并冲突时使用哪种差异分析工具。
```shell
$ git config --global merge.tool <差异分析工具>
```
> Git 可以理解 kdiff3，tkdiff，meld，xxdiff，emerge，vimdiff，gvimdiff，ecmerge，和 opendiff 等合并工具的输出信息。当然，你也可以自己开发一套合并工具。

查看配置信息可以使用 `git config --list` 命令
```shell
$ git config --list
```
有时候会看到重复的变量名，那就说明它们来自不同的配置文件，不过最终 Git 实际采用的是最后一个。

也可以直接查阅某个环境变量的设定，只要把特定的名字跟在后面即可，像这样：
```shell
$ git config user.name
```

# Git 基本用法

## 1. 查看帮助

```shell
$ git help <verb>
$ git <verb> --help
$ man git-<verb>
```

## 2. 取得项目的 Git 仓库

1. 新建仓库 `git init`  
要对现有的某个项目开始用 Git 管理，只需到此项目所在的目录执行：`git init`
2. 从现有仓库克隆 `git clone <url>`  
克隆仓库的命令格式为 `git clone <url>`，`url` 为要克隆的项目地址
> Git 支持许多数据传输协议。你可以用 git://，http(s):// 或者 user@server:/path.git 表示的 SSH 传输协议。

## 3. 记录每次更新到仓库

1. 检查当前文件状态 `git status`  
Git 不会自动将之纳入跟踪范围，除非你使用命令添加，以下为一次查看状态时的输出：
```shell
$ git status
On branch master # 当前分支（master）
Changes to be committed: # 缓存区文件
  (use "git reset HEAD <file>..." to unstage)

        new file:   README
        modified:   benchmarks.rb

Changes not staged for commit: # 未跟踪文件
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   benchmarks.rb
```
2. 跟踪新文件 `git add <file>...` `<file>` 为文件名/目录名，为目录名时表示递归跟踪该目录下所有的文件

3. 忽略某些文件  
我们总会有些文件无需纳入 Git 的管理，也不希望它们总出现在未跟踪文件列表。通常都是些自动生成的文件，比如日志文件，或者编译过程中创建的临时文件等。可以创建一个名为 `.gitignore` 的文件，列出要忽略的文件模式。  

**文件 `.gitignore` 的格式规范如下：**
* 所有空行或者以注释符号 ＃ 开头的行都会被 Git 忽略。
* 可以使用标准的 `glob 模式` 匹配。
* 匹配模式最后跟反斜杠（/）说明要忽略的是目录。
* 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。 

** `glob 模式`（ shell 所使用的简化了的正则表达式）：**  
* 星号（`*`）匹配零个或多个任意字符
* `[<要匹配的字符>]` 匹配任何一个列在方括号中的字符（`[abc]` 表示a\b\c任意一个均可）
* 问号（`?`）只匹配一个任意字符
* 如果在方括号中使用短划线（`-`）分隔两个字符，表示所有在这两个字符范围内的都可以匹配（比如 [0-9] 表示匹配所有 0 到 9 的数字）
```
# 此为注释 – 将被 Git 忽略
# 忽略所有 .a 结尾的文件
*.a
# 但 lib.a 除外
!lib.a
# 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
/TODO
# 忽略 build/ 目录下的所有文件
build/
# 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
doc/*.txt
# ignore all .txt files in the doc/ directory
doc/**/*.txt
```

4. 查看已暂存和未暂存的更新 `git diff`  
此命令比较的是 **工作目录中当前文件和暂存区域快照之间的差异**，也就是 **修改之后还没有暂存起来的变化内容**。若要看 **已经暂存起来的文件和上次提交时的快照之间的差异**，可以用 `git diff --cached` 命令。（Git 1.6.1 及更高版本还允许使用 `git diff --staged`，效果是相同的，但更好记些。）

## 4. 提交更新
1. 提交更新 `git commit`  
在此之前，请一定要确认还有什么修改过的或新建的文件还没有 `git add` 过，否则提交的时候不会记录这些还没暂存起来的变化。所以，每次准备提交前，先用 `git status` 看下，是不是都已暂存起来了，然后再运行提交命令 `git commit`
```shell
$ git commit
```
这种方式会启动文本编辑器以便输入本次提交的说明。
编辑器会显示类似下面的文本信息：  
```
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch master
# Changes to be committed:
#       new file:   README
#       modified:   benchmarks.rb
#
~
~
~
".git/COMMIT_EDITMSG" 10L, 283C
```
默认的提交消息包含最后一次运行 `git status` 的输出，放在注释行里，另外开头还有一空行，供你输入提交说明。你完全可以去掉这些注释行，不过留着也没关系，多少能帮你回想起这次更新的内容有哪些。（如果觉得这还不够，可以用 `-v` 选项将修改差异的每一行都包含到注释中来。）退出编辑器时，Git 会丢掉注释行，将说明内容和本次更新提交到仓库。
```shell
$ git commit -m "Story 182: Fix benchmarks for speed"
[master 463dc4f] Story 182: Fix benchmarks for speed
 2 files changed, 3 insertions(+)
 create mode 100644 README
```
现在你已经创建了第一个提交！可以看到，提交后它会告诉你，当前是在哪个分支（`master`）提交的，本次提交的完整 SHA-1 校验和是什么（`463dc4f`），以及在本次提交中，有多少文件修订过，多少行添改和删改过。  

提交时记录的是放在暂存区域的快照，任何还未暂存的仍然保持已修改状态，可以在下次提交时纳入版本管理。每一次运行提交操作，都是对你项目作一次快照，以后可以回到这个状态，或者进行比较。

2. 跳过使用暂存区域 `git commit -a`  
Git 提供了一个跳过使用暂存区域的方式，只要在提交的时候，给 `git commit` 加上 `-a` 选项，Git 就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 `git add` 步骤

3. 移除文件 `git rm`  
要从 Git 中移除某个文件，就必须要从已跟踪文件清单中移除（确切地说，是从暂存区域移除），然后提交。可以用 `git rm` 命令完成此项工作，并连带 **从工作目录中删除指定的文件**，这样以后就不会出现在未跟踪文件清单中了。

如果只是简单地从工作目录中手工删除文件，运行 `git status` 时就会在 “Changes not staged for commit” 部分（也就是未暂存清单）
然后再运行 `git rm` 记录此次移除文件的操作
最后提交的时候，该文件就不再纳入版本管理了。如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 `-f`（译注：即 force 的首字母），以防误删除文件后丢失修改的内容。  

把文件从 Git 仓库中删除（亦即从暂存区域移除），但仍然希望保留在当前工作目录中。用 `--cached` 选项即可：
```shell
# <file> 文件名/目录，也可使用 glob 模式
$ git rm --cached <file>
# 删除所有 log/ 目录下扩展名为 .log 的文件。
$ git rm log/\*.log
# 递归删除当前目录及其子目录中所有 ~ 结尾的文件
$ git rm \*~
```
4. 移动文件 `git mv file_from file_to`  
运行 `git mv` 就相当于运行了下面三条命令：
```shell
# 如此分开操作，Git 也会意识到这是一次改名
$ mv README.txt README
$ git rm README.txt
$ git add README
```

## 5. 查看提交历史
`git log`  
会按提交时间列出所有的更新，最近的更新排在最上面。每次更新都有一个 SHA-1 校验和、作者的名字和电子邮件地址、提交时间，最后缩进一个段落显示提交说明。  
1. `-p` 展开显示每次提交的内容差异  
        * `--word-diff` 单词层面的对比  

        ```shell
        $ git log -U1 --word-diff
        commit ca82a6dff817ec66f44342007202690a93763949
        Author: Scott Chacon <schacon@gee-mail.com>
        Date:   Mon Mar 17 21:52:11 2008 -0700

            changed the version number

        diff --git a/Rakefile b/Rakefile
        index a874b73..8f94139 100644
        --- a/Rakefile
        +++ b/Rakefile
        @@ -7,3 +7,3 @@ spec = Gem::Specification.new do |s|
            s.name      =   "simplegit"
            s.version   =   [-"0.1.0"-]{+"0.1.1"+}
            s.author    =   "Scott Chacon"
        ```
        
        这里并没有平常看到的添加行或者删除行的信息。这里的对比显示在行间。新增加的单词被 `{+ +}` 括起来，被删除的单词被 `[- -]` 括起来。在进行单词层面的对比的时候，你可能希望上下文（ context ）行数从默认的 3 行，减为 1 行，那么可以使用 `-U1` 选项。上面的例子中，我们就使用了这个选项。
        * `-2` 仅显示最近的两次更新  
        * `--stat` 仅显示简要的增改行数统计，每个提交都列出了修改过的文件，以及其中添加和移除的行数，并在最后列出所有增减行数小计  

2. `--pretty` 指定使用完全不同于默认格式的方式展示提交历史
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

```shell
$ git log --pretty=format:"%h - %an, %ar : %s"
ca82a6d - Scott Chacon, 11 months ago : changed the version number
085bb3b - Scott Chacon, 11 months ago : removed unnecessary test code
a11bef0 - Scott Chacon, 11 months ago : first commit
```
用 `oneline` 或 `format` 时结合 `--graph` 选项，可以看到开头多出一些 ASCII 字符串表示的简单图形，形象地展示了每个提交所在的分支及其分化衍合情况。在我们之前提到的 Grit 项目仓库中可以看到：
```
$ git log --pretty=format:"%h %s" --graph
* 2d3acf9 ignore errors from SIGCHLD on trap
*  5e3ee11 Merge branch 'master' of git://github.com/dustin/grit
|\
| * 420eac9 Added a method for getting the current branch.
* | 30e367c timeout code and tests
* | 5a09431 add timeout protection to grit
* | e1193f8 support for heads with slashes in them
|/
* d6016bc require time for xmlschema
*  11d191e Merge branch 'defunkt' into local
```

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

2. 限制输出长度

| 选项	             | 说明
| :-------------------- | :----------------- |
| `-(n)`	            | 仅显示最近的 n 条提交
| `--since, --after`    | 仅显示指定时间之后的提交
| `--until`, `--before` | 仅显示指定时间之前的提交
| `--author`	        | 仅显示指定作者相关的提交
| `--committer`	        | 仅显示指定提交者相关的提交
```shell
# 如果要查看 Git 仓库中，2008 年 10 月期间，Junio Hamano 提交的但未合并的测试脚本（位于项目的 t/ 目录下的文件），可以用下面的查询命令：
$ git log --pretty="%h - %s" --author=gitster --since="2008-10-01" \
   --before="2008-11-01" --no-merges -- t/
5610e3b - Fix testcase failure when extended attribute
acd3b9e - Enhance hold_lock_file_for_{update,append}()
f563754 - demonstrate breakage of detached checkout wi
d1a43f2 - reset --hard/read-tree --reset -u: remove un
51a94af - Fix "checkout --track -b newbranch" on detac
b0ad11e - pull: allow "git pull origin $something:$cur
```

## 6. 撤销操作  

1. 修改最后一次提交  
` git commit --amend` 重新提交，此命令将使用当前的暂存区域快照提交。如果刚才提交完没有作任何改动，直接运行此命令的话，相当于有机会重新编辑提交说明，但将要提交的文件快照和之前的一样。如果刚才提交时忘了暂存某些修改，可以先补上暂存操作，然后再运行 `--amend` 提交。

2. 取消已经暂存的文件  
`git reset HEAD <file>...` 取消暂存

3. 取消对文件的修改  
`git checkout -- <file>...` 回到之前的状态（也就是修改之前的版本）,这条命令有些危险，所有对文件的修改都没有了，因为我们把之前版本的文件复制过来重写了此文件。所以在用这条命令前，请务必确定真的不再需要保留刚才的修改。
> 任何已经提交到 Git 的都可以被恢复，即使文件已经被删除。没有提交过的，对 Git 来说它们就像从未存在过一样不可恢复。

## 7. 远程仓库的使用

要参与任何一个 Git 项目的协作，必须要了解该如何管理远程仓库。远程仓库是指托管在网络上的项目仓库，可能会有好多个，其中有些你只能读，另外有些可以写。同他人协作开发某个项目时，需要管理这些远程仓库，以便推送或拉取数据，分享各自的工作进展。 管理远程仓库的工作，包括添加远程库，移除废弃的远程库，管理各式远程库分支，定义是否跟踪这些分支，等等。

1. 查看当前的远程库  
`git remote` 列出每个远程库的简短名字，在克隆完某个项目后，至少可以看到一个名为 origin 的远程库，Git 默认使用这个名字来标识你所克隆的原始仓库。  
`-v` 选项（`--verbose` 的简写），显示对应的克隆地址

2. 添加远程仓库  
`git remote add [shortname] [url]` 添加一个新的远程仓库，可以指定一个简单的名字，以便将来引用。  

3. 从远程仓库抓取数据  
`git fetch [shortname]/[url]` 抓取数据，此命令会到远程仓库中拉取所有你本地仓库中还没有的数据。如果是克隆了一个仓库，此命令会自动将远程仓库归于 `origin` 名下。所以，`git fetch origin` 会抓取从你上次克隆以来别人上传到此远程仓库中的所有更新（或是上次 fetch 以来别人提交的更新）。有一点很重要，fetch 命令只是将远端的数据拉到本地仓库，并不自动合并到当前工作分支，只有当你确实准备好了，才能手工合并。  
`git pull` 从原始克隆的远端仓库中抓取数据后，合并到工作目录中的当前分支。如果设置了某个分支用于跟踪某个远端仓库的分支，可以使用 `git pull` 命令自动抓取数据下来，然后将远端分支自动合并到本地仓库中当前分支。  

4. 推送数据到远程仓库  
`git push [remote-name] [branch-name]` 将本地仓库中的数据推送到远程仓库。只有在所克隆的服务器上有写权限，或者同一时刻没有其他人在推数据，这条命令才会如期完成任务。如果在你推数据前，已经有其他人推送了若干更新，那你的推送操作就会被驳回。你必须先把他们的更新抓取到本地，合并到自己的项目中，然后才可以再次推送。

5. 查看远程仓库信息  
`git remote show [remote-name]` 查看某个远程仓库的详细信息。  
```shell
$ git remote show origin
* remote origin
  URL: git@github.com:defunkt/github.git
  Remote branch merged with 'git pull' while on branch issues # 运行 git pull 时将自动合并的分支
    issues
  Remote branch merged with 'git pull' while on branch master # 运行 git pull 时将自动合并的分支
    master
  New remote branches (next fetch will store in remotes/origin) # 未同步到本地的远端分支
    caching 
  Stale tracking branches (use 'git remote prune') # 已同步到本地但在远端服务器上已被删除的分支
    libwalker
    walker2
  Tracked remote branches # 处于跟踪状态中的远端分支
    acl
    apiv2
    dashboard2
    issues
    master
    postgres
  Local branch pushed with 'git push' # 运行 git push 时缺省推送的分支是什么
    master:master
```

6. 远程仓库的删除和重命名  
`git remote rename` 修改某个 **远程仓库在本地的简称**   
> 注意，对远程仓库的重命名，也会使对应的分支名称发生变化，
碰到远端仓库服务器迁移，或者原来的克隆镜像不再使用，又或者某个参与者不再贡献代码，那么需要移除对应的远端仓库，可以运行 `git remote rm` 命令。  

## 8. 打标签

Git 也可以对某一时间点上的版本打上标签。我们一起来学习如何列出所有可用的标签，如何新建标签，以及各种不同类型标签之间的差别。

1. 列出已有的标签  
`git tag` 列出现有标签，显示的标签按字母顺序排列，所以标签的先后并不表示重要程度的轻重。可以用特定的搜索模式列出符合条件的标签。

2. 新建标签  
Git 使用的标签有两种类型：轻量级的（lightweight）和含附注的（annotated）。轻量级标签就像是个不会变化的分支，实际上它就是个指向特定提交对象的引用。而含附注标签，实际上是存储在仓库中的一个独立对象，它有自身的校验和信息，包含着标签的名字，电子邮件地址和日期，以及标签说明，标签本身也允许使用 GNU Privacy Guard (GPG) 来签署或验证。一般我们都建议使用含附注型的标签，以便保留相关信息；当然，如果只是临时性加注标签，或者不需要旁注额外信息，用轻量级标签也没问题。
    * 含附注的标签  
    `-a [tag-name]` 创建一个含附注类型的标签，（ annotated 的首字母）  
    `-m` 指定对应的标签说明，Git 会将此说明一同保存在标签对象中。如果没有给出该选项，Git 会启动文本编辑软件供你输入标签说明。  
    `git show [tag-name]` 查看相应标签的版本信息，并连同显示打标签时的提交对象。
    * 签署标签  
    `-s` 如果有自己的私钥，可以用 GPG 来签署标签（signed 的首字母） 
    * 轻量级标签  
    轻量级标签实际上就是一个保存着对应提交对象的校验和信息的文件。  
    `git tag [tag-name]` 新建轻量级标签

3. 验证标签  
`git tag -v [tag-name]` （verify 的首字母）验证已经签署的标签。此命令会调用 GPG 来验证签名，所以你需要有签署者的公钥，存放在 keyring 中才能验证。
```shell
# 若是没有签署者的公钥，会报告类似下面这样的错误：
gpg: Signature made Wed Sep 13 02:08:25 2006 PDT using DSA key ID F3119B9A
gpg: Can't check signature: public key not found
error: could not verify the tag 'v1.4.2.1'
```

4. 后期加注标签  
 `git tag -a [tag-name] [对应提交对象的校验（或前几位字符）]` 在后期对早先的某次提交加注标签

5. 分享标签  
`git push [shortname]/[url] [tagname]`  默认情况下 `git push` 并不会把标签传送到远端服务器上，只有通过显式命令才能分享标签到远端仓库。其命令格式如同推送分支。其他人克隆共享仓库或拉取数据同步后，也会看到这些标签。如果要一次推送所有本地新增的标签上去，可以使用 `--tags` 选项。

## Git 实用技巧

1. 自动补全
如果你用的是 `Bash shel`l，可以试试看 Git 提供的自动补全脚本。下载 Git 的源代码，进入 `contrib/completion` 目录，会看到一个 `git-completion.bash` 文件。将此文件复制到你自己的用户主目录中（译注：按照下面的示例，还应改名加上点：`cp git-completion.bash` `~/.git-completion.bash`），并把下面一行内容添加到你的 `.bashrc` 文件中：
```shell
source ~/.git-completion.bash
```
也可以为系统上所有用户都设置默认使用此脚本。Mac 上将此脚本复制到 `/opt/local/etc/bash_completion.d` 目录中，Linux 上则复制到 `/etc/bash_completion.d/` 目录中。这两处目录中的脚本，都会在 Bash 启动时自动加载。如果在 Windows 上安装了 msysGit，默认使用的 Git Bash 就已经配好了这个自动补全脚本，可以直接使用。

在输入 Git 命令的时候可以敲两次跳格键（`Tab`），就会看到列出所有匹配的可用命令建议

2. Git 命令别名
Git 并不会推断你输入的几个字符将会是哪条命令，不过如果想偷懒，少敲几个命令的字符，可以用 git config 为命令设置别名。
```shell
$ git config --global alias.co checkout
$ git config --global alias.br branch
$ git config --global alias.ci commit
$ git config --global alias.st status
```
```shell
# 使用这种技术还可以创造出新的命令，比方说取消暂存文件时的输入比较繁琐，可以自己设置一下：
$ git config --global alias.unstage 'reset HEAD --'
# 这样一来，下面的两条命令完全等同：
$ git unstage fileA
$ git reset HEAD fileA

# last 命令：
$ git config --global alias.last 'log -1 HEAD'
# 然后要看最后一次的提交信息，就变得简单多了：
$ git last
commit 66938dae3329c7aebe598c2246a8e6af90d04646
Author: Josh Goebel <dreamer3@example.com>
Date:   Tue Aug 26 19:48:51 2008 +0800

    test for current head

    Signed-off-by: Scott Chacon <schacon@example.com>
```
Git 只是简单地在命令中替换了你设置的别名。  
有时候我们希望运行某个外部命令，而非 Git 的子命令，这个好办，只需要在命令前加上 `!` 就行。如果你自己写了些处理 Git 仓库信息的脚本的话，就可以用这种技术包装起来。
```shell
# 我们可以设置用 git visual 启动 gitk：
$ git config --global alias.visual '!gitk'
```
---
到目前为止，你已经学会了最基本的 Git 本地操作：创建和克隆仓库，做出修改，暂存并提交这些修改，以及查看所有历史修改记录。

# Git 分支

> Git 保存的不是文件差异或者变化量，而只是一系列文件快照。  
> 在 Git 中提交时，会保存一个提交（commit）对象，该对象包含一个指向暂存内容快照的指针，包含本次提交的作者等相关附属信息，包含零个或多个指向该提交对象的父对象指针：首次提交是没有直接祖先的，普通提交有一个祖先，由两个或多个分支合并产生的提交则有多个祖先。  
> 
> 当使用 `git commit` 新建一个提交对象前，Git 会先计算每一个子目录的校验和，然后在 Git 仓库中将这些目录保存为树（`tree`）对象。之后 Git 创建的提交对象，除了包含相关提交信息以外，还包含着指向这个树对象（项目根目录）的指针，如此它就可以在将来需要的时候，重现此次快照的内容了。  
> 
> 作些修改后再次提交，那么这次的提交对象会包含一个指向上次提交对象的指针。  
> 
> **Git 中的分支**，其实本质上仅仅是个指向 commit 对象的可变指针。Git 会使用 master 作为分支的默认名字。在若干次提交后，你其实已经有了一个指向最后一次提交对象的 master 分支，它在每次提交的时候都会自动向前移动。  
> 
> Git 又是如何创建一个新的分支的呢？答案很简单，创建一个新的分支指针。
> 
> Git 是如何知道你当前在哪个分支上工作的呢？其实答案也很简单，它保存着一个名为 `HEAD` 的特别指针。请注意它和你熟知的许多其他版本控制系统（比如 Subversion 或 CVS）里的 HEAD 概念大不相同。在 Git 中，它是一个指向你正在工作中的本地分支的指针（译注：将 `HEAD` 想象为当前分支的别名。）。运行 `git branch` 命令，仅仅是建立了一个新的分支，但不会自动切换到这个分支中去，要切换到其他分支，可以执行 `git checkout` 命令。  
> 
> 由于 Git 中的分支实际上仅是一个包含所指对象校验和（40 个字符长度 SHA-1 字串）的文件，所以创建和销毁一个分支就变得非常廉价。说白了，新建一个分支就是向一个文件写入 41 个字节（外加一个换行符）那么简单，当然也就很快了。
> 
> 这和大多数版本控制系统形成了鲜明对比，它们管理分支大多采取备份所有项目文件到特定目录的方式，所以根据项目文件数量和大小不同，可能花费的时间也会有相当大的差别，快则几秒，慢则数分钟。而 Git 的实现与项目复杂度无关，它永远可以在几毫秒的时间内完成分支的创建和切换。同时，因为每次提交时都记录了祖先信息（译注：即 `parent` 对象），将来要合并分支时，寻找恰当的合并基础（译注：即共同祖先）的工作其实已经自然而然地摆在那里了，所以实现起来非常容易。Git 鼓励开发者频繁使用分支，正是因为有着这些特性作保障。

## 1. 分支的基本操作

1. 查看分支  
`git branch` 给出当前所有分支的清单  
```shell
# 前面的 * 代表当前所在分支
$ git branch
  iss53
* master
  testing
```
`-v` 查看各个分支最后一个提交对象的信息  
`--merged` 查看哪些分支已被并入当前分支（哪些分支是当前分支的直接上游）  
`--no-merged`(1.5.6+) 尚未与当前分支合并的分支  

2. 新建分支  
`git branch [branch-name]` 新建分支

3. 切换分支  
`git checkout [branch-name]` 切换分支

4. 新建并切换到该分支   
`git checkout -b [branch-name]` 新建并切换到该分支，相当于同时执行 `git branch [branch-name]`、
`git checkout [branch-name]` 两条命令

5. 删除分支  
`git branch -d [branch-name]` 删除分支，如果要删除的分支包含未合并的内容，Git 会阻止删除，并会报错：
```shell
error: The branch 'testing' is not fully merged.
If you are sure you want to delete it, run 'git branch -D testing'.
```
此时可以使用 `git branch -D [branch-name]` 强制删除（`-D` 大写）

6. 合并分支  
`git merge [branch-name]` 合并分支，合并时会将指定分支（`[branch-name]` 所代表的分支）合并到当前所在的分支，所以在合并之前最好先确定当前所在的分支。  
有时候合并操作并不会如此顺利。如果在不同的分支中都修改了同一个文件的同一部分，Git 就无法干净地把两者合到一起（译注：逻辑上说，这种问题只能由人来裁决。）。  
Git 作了合并，但没有提交，它会停下来等你解决冲突。要看看哪些文件在合并时发生冲突，可以用 `git status` 查阅。任何包含未解决冲突的文件都会以未合并（unmerged）的状态列出。Git 会在有冲突的文件里加入标准的冲突解决标记，可以通过它们来手工定位并解决这些冲突。  

> 如果顺着一个分支走下去可以到达另一个分支的话，那么 Git 在合并两者时，只会简单地把指针右移，因为这种单线的历史分支不存在任何需要解决的分歧，所以这种合并过程可以称为快进（Fast forward）。  
> 值得一提的是 Git 可以自己裁决哪个共同祖先才是最佳合并基础；这和 CVS 或 Subversion（1.5 以后的版本）不同，它们需要开发者手工指定合并基础。所以此特性让 Git 的合并操作比其他系统都要简单不少。

## 2. 利用分支进行开发的流程

1. 长期分支
由于 Git 使用简单的三方合并，你可以同时拥有多个开放的分支，每个分支用于完成特定的任务，随着开发的推进，你可以随时把某个特性分支的成果并到其他分支中。  
许多使用 Git 的开发者都喜欢用这种方式来开展工作，比如仅在 `master` 分支中保留完全稳定的代码，即已经发布或即将发布的代码。与此同时，他们还有一个名为 `develop` 或 `next` 的平行分支，专门用于后续的开发，或仅用于稳定性测试 — 当然并不是说一定要绝对稳定，不过一旦进入某种稳定状态，便可以把它合并到 `master` 里。这样，在确保这些已完成的特性分支能够通过所有测试，并且不会引入更多错误之后，就可以并到主干分支中，等待下一次的发布。  
本质上我们刚才谈论的，是随着提交对象不断右移的指针。稳定分支的指针总是在提交历史中落后一大截，而前沿分支总是比较靠前。  

![稳定分支总是比较老旧](./img/稳定分支总是比较老旧.png)  

你可以用这招维护不同层次的稳定性。某些大项目还会有个 `proposed`（建议）或 `pu`（`proposed updates`，建议更新）分支，它包含着那些可能还没有成熟到进入 next 或 `master` 的内容。这么做的目的是拥有不同层次的稳定性：当这些分支进入到更稳定的水平时，再把它们合并到更高层分支中去。再次说明下，使用多个长期分支的做法并非必需，不过一般来说，对于特大型项目或特复杂的项目，这么做确实更容易管理。

2. 特性分支
在任何规模的项目中都可以使用特性（Topic）分支。一个特性分支是指一个短期的，用来实现单一特性或与其相关工作的分支。可能你在以前的版本控制系统里从未做过类似这样的事情，因为通常创建与合并分支消耗太大。然而在 Git 中，一天之内建立、使用、合并再删除多个分支是常见的事。  
该技术允许你迅速且完全的进行语境切换 — 因为你的工作分散在不同的流水线里，每个分支里的改变都和它的目标特性相关，浏览代码之类的事情因而变得更简单了。你可以把作出的改变保持在特性分支中几分钟，几天甚至几个月，等它们成熟以后再合并，而不用在乎它们建立的顺序或者进度。  
我们来看一个实际的例子。请看图 3-20，由下往上，起先我们在 master 工作到 C1，然后开始一个新分支 iss91 尝试修复 91 号缺陷，提交到 C6 的时候，又冒出一个解决该问题的新办法，于是从之前 C4 的地方又分出一个分支 iss91v2，干到 C8 的时候，又回到主干 master 中提交了 C9 和 C10，再回到 iss91v2 继续工作，提交 C11，接着，又冒出个不太确定的想法，从 master 的最新提交 C10 处开了个新的分支 dumbidea 做些试验。  

![拥有多个特性分支的提交历史](./img/拥有多个特性分支的提交历史.png)  

现在，假定两件事情：我们最终决定使用第二个解决方案，即 iss91v2 中的办法；另外，我们把 dumbidea 分支拿给同事们看了以后，发现它竟然是个天才之作。所以接下来，我们准备抛弃原来的 iss91 分支（实际上会丢弃 C5 和 C6），直接在主干中并入另外两个分支。  

![合并了 dumbidea 和 iss91v2 后的分支历史](./img/合并了dumbidea和iss91v2后的分支历史.png)  

> 这些分支全部都是本地分支，这一点很重要。当你在使用分支及合并的时候，一切都是在你自己的 Git 仓库中进行的 — 完全不涉及与服务器的交互。

## 3. 远程分支

远程分支（remote branch）是对远程仓库中的分支的索引。它们是一些无法移动的本地分支；只有在 Git 进行网络交互时才会更新。远程分支就像是书签，提醒着你上次连接远程仓库时上面各分支的位置。用 `(远程仓库名)/(分支名)` 这样的形式表示远程分支。  

1. 推送本地分支
`git push (远程仓库名) (分支名)`
```shell
# 上传我本地的 serverfix 分支到远程仓库中去，仍旧称它为 serverfix 分支
git push origin serverfix
# 或（两者效果相同，冒号后面为该分支在远程服务器上的名称，可根据需要命名）
git push origin serverfix:serverfix
```

2. 跟踪远程分支
从远程分支 `checkout` 出来的本地分支，称为 跟踪分支 (`tracking branch`)。跟踪分支是一种和某个远程分支有直接联系的本地分支。在跟踪分支里输入 `git push`，Git 会自行推断应该向哪个服务器的哪个分支推送数据。同样，在这些分支里运行 `git pull` 会获取所有远程索引，并把它们的数据都合并到本地分支中来。  
在克隆仓库时，Git 通常会自动创建一个名为 master 的分支来跟踪 origin/master。这正是 git push 和 git pull 一开始就能正常工作的原因。当然，你可以随心所欲地设定为其它跟踪分支，
`git checkout -b [本地分支名] [远程名]/[分支名]`  
或  
`git checkout --track [远程名]/[分支名]`(1.6.2+)

3. 删除远程分支  
`git push [远程名] :[分支名]` 有种方便记忆这条命令的方法：记住我们不久前见过的 `git push [远程名] [本地分支]:[远程分支]` 语法，如果省略 `[本地分支]`，那就等于是在说“在这里提取空白然后把它变成`[远程分支]`”。

## 4. 分支的衍合

把一个分支中的修改整合到另一个分支的办法有两种：`merge` 和 `rebase`（`rebase` 的翻译暂定为“衍合”）  
之前介绍过，最容易的整合分支的方法是 `merge` 命令，它会把两个分支最新的快照（以及二者最新的共同祖先）进行三方合并，合并的结果是产生一个新的提交对象。  
有了 `rebase` 命令，就可以把在一个分支里提交的改变移到另一个分支里重放一遍。你可以把在 分支1 里产生的变化补丁在 分支2 的基础上重新打一遍。在 Git 里，这种操作叫做衍合（rebase）。  
虽然最后整合得到的结果没有任何区别，但衍合能产生一个更为整洁的提交历史。如果视察一个衍合过的分支的历史记录，看起来会更清楚：仿佛所有修改都是在一根线上先后进行的，尽管实际上它们原本是同时并行发生的。  
一般我们使用衍合的目的，是想要得到一个能在远程分支上干净应用的补丁 — 比如某些项目你不是维护者，但想帮点忙的话，最好用衍合：先在自己的一个分支里进行开发，当准备向主项目提交补丁的时候，根据最新的 `origin/master` 进行一次衍合操作然后再提交，这样维护者就不需要做任何整合工作（译注：实际上是把解决分支补丁同最新主干代码之间冲突的责任，化转为由提交补丁的人来解决。），只需根据你提供的仓库地址作一次快进合并，或者直接采纳你提交的补丁。
> 合并结果中最后一次提交所指向的快照，无论是通过衍合，还是三方合并，都会得到相同的快照内容，只不过提交历史不同罢了。衍合是按照每行的修改次序重演一遍修改，而合并是把最终结果合在一起。

> 衍合的风险  
> **一旦分支中的提交对象发布到公共仓库，就千万不要对该分支进行衍合操作**。  
> 如果你遵循这条金科玉律，就不会出差错。  
> 在进行衍合的时候，实际上抛弃了一些现存的提交对象而创造了一些类似但不同的新的提交对象。如果你把原来分支中的提交对象发布出去，并且其他人更新下载后在其基础上开展工作，而稍后你又用 git rebase 抛弃这些提交对象，把新的重演后的提交对象发布出去的话，你的合作者就不得不重新合并他们的工作，这样当你再次从他们那里获取内容时，提交历史就会变得一团糟。  
> 如果把衍合当成一种在推送之前清理提交历史的手段，而且仅仅衍合那些尚未公开的提交对象，就没问题。如果衍合那些已经公开的提交对象，并且已经有人基于这些提交对象开展了后续开发工作的话，就会出现叫人沮丧的麻烦。

# 服务器上的 Git

架设一台 Git 服务器并不难。第一步是选择与服务器通讯的协议。远程仓库通常只是一个裸仓库（bare repository） — 即一个没有当前工作目录的仓库。因为该仓库只是一个合作媒介，所以不需要从硬盘上取出最新版本的快照；仓库里存放的仅仅是 Git 的数据。简单地说，裸仓库就是你工作目录中 `.git` 子目录内的内容。

## 1. 协议

Git 可以使用四种主要的协议来传输数据：本地传输，SSH 协议，Git 协议和 HTTP 协议。除了 HTTP 协议外，其他所有协议都要求在服务器端安装并运行 Git。

### 1. 本地协议  

最基本的就是 *本地协议*（Local protocol），所谓的远程仓库在该协议中的表示，就是硬盘上的另一个目录。这常见于团队每一个成员都对一个共享的文件系统（例如 NFS）拥有访问权，或者比较少见的多人共用同一台电脑的情况。后面一种情况并不安全，因为所有代码仓库实例都储存在同一台电脑里，增加了灾难性数据损失的可能性。

如果你使用一个共享的文件系统，就可以在一个本地文件系统中克隆仓库，推送和获取。克隆的时候只需要将远程仓库的路径作为 URL 使用，
```shell
$ git clone /opt/git/project.git
$ git clone file:///opt/git/project.git
```
如果在 URL 开头明确使用 `file://` ，那么 Git 会以一种略微不同的方式运行。如果你只给出路径，Git 会尝试使用硬链接或直接复制它所需要的文件。如果使用了 `file://` ，Git 会调用它平时通过网络来传输数据的工序，而这种方式的效率相对较低。使用 `file://` 前缀的主要原因是当你需要一个不包含无关引用或对象的干净仓库副本的时候 — 一般指从其他版本控制系统导入的，或类似情形。  

要添加一个本地仓库作为现有 Git 项目的远程仓库，可以这样做：
```shell
git remote add local_proj /opt/git/project.git
```
然后就可以像在网络上一样向这个远程仓库推送和获取数据了。

**优点**  
基于文件仓库的优点在于它的简单，同时保留了现存文件的权限和网络访问权限。如果你的团队已经有一个全体共享的文件系统，建立仓库就十分容易了。你只需把一份裸仓库的副本放在大家都能访问的地方，然后像对其他共享目录一样设置读写权限就可以了。  
从别人工作目录中获取工作成果的快捷方法。假如你和你的同事在一个项目中合作，他们想让你检出一些东西的时候，运行类似 `git pull /home/john/project` 通常会比他们推送到服务器，而你再从服务器获取简单得多。  

**缺点**  
与基本的网络连接访问相比，难以控制从不同位置来的访问权限。  
该方法不一定就是最快的，尤其是对于共享挂载的文件系统。本地仓库只有在你对数据访问速度快的时候才快。在同一个服务器上，如果二者同时允许 Git 访问本地硬盘，通过 NFS 访问仓库通常会比 SSH 慢。

### 2. SSH 协议

Git 使用的传输协议中最常见的可能就是 SSH 了。这是因为大多数环境已经支持通过 SSH 对服务器的访问 — 即便还没有，架设起来也很容易。SSH 也是唯一一个同时支持读写操作的网络协议。另外两个网络协议（HTTP 和 Git）通常都是只读的，所以虽然二者对大多数人都可用，但执行写操作时还是需要 SSH。SSH 同时也是一个验证授权的网络协议；而因为其普遍性，一般架设和使用都很容易。
```shell
# 通过 SSH 克隆一个 Git 仓库
$ git clone ssh://user@server/project.git
# 或者不指明某个协议 — 这时 Git 会默认使用 SSH ：
$ git clone user@server:project.git
# 如果不指明用户，Git 会默认使用当前登录的用户名连接服务器。
```
**优点**  
如果你想拥有对网络仓库的写权限，基本上不可能不使用 SSH。  
SSH 架设相对比较简单 — SSH 守护进程很常见，很多网络管理员都有一些使用经验，而且很多操作系统都自带了它或者相关的管理工具。  
通过 SSH 进行访问是安全的 — 所有数据传输都是加密和授权的。  
和 Git 及本地协议一样，SSH 也很高效，会在传输之前尽可能压缩数据。  

**缺点**  
不能通过它实现仓库的匿名访问。即使仅为读取数据，人们也必须在能通过 SSH 访问主机的前提下才能访问仓库，这使得 SSH 不利于开源的项目。  
如果你仅仅在公司网络里使用，SSH 可能是你唯一需要使用的协议。如果想允许对项目的匿名只读访问，那么除了为自己推送而架设 SSH 协议之外，还需要支持其他协议以便他人访问读取。  

### 3. Git 协议

这是一个包含在 Git 软件包中的特殊守护进程； 它会监听一个提供类似于 SSH 服务的特定端口（9418），而无需任何授权。打算支持 Git 协议的仓库，需要先创建 git-daemon-export-ok 文件 — 它是协议进程提供仓库服务的必要条件 — 但除此之外该服务没有什么安全措施。要么所有人都能克隆 Git 仓库，要么谁也不能。这也意味着该协议通常不能用来进行推送。你可以允许推送操作；然而由于没有授权机制，一旦允许该操作，网络上任何一个知道项目 URL 的人将都有推送权限。  

**优点**  
Git 协议是现存最快的传输协议。如果你在提供一个有很大访问量的公共项目，或者一个不需要对读操作进行授权的庞大项目，架设一个 Git 守护进程来供应仓库是个不错的选择。它使用与 SSH 协议相同的数据传输机制，但省去了加密和授权的开销。  

**缺点**  
Git 协议消极的一面是缺少授权机制。用 Git 协议作为访问项目的唯一方法通常是不可取的。一般的做法是，同时提供 SSH 接口，让几个开发者拥有推送（写）权限，其他人通过 `git://` 拥有只读权限。  
Git 协议可能也是最难架设的协议。它要求有单独的守护进程，需要定制 — 我们将在本章的 “Gitosis” 一节详细介绍它的架设 — 需要设定 xinetd 或类似的程序，而这些工作就没那么轻松了。该协议还要求防火墙开放 9418 端口，而企业级防火墙一般不允许对这个非标准端口的访问。大型企业级防火墙通常会封锁这个少见的端口。

### 4. HTTP/S 协议

HTTP 或 HTTPS 协议的优美之处在于架设的简便性。基本上，只需要把 Git 的裸仓库文件放在 HTTP 的根目录下，配置一个特定的 post-update 挂钩（hook）就可以搞定（Git 挂钩的细节见第 7 章）。此后，每个能访问 Git 仓库所在服务器上 web 服务的人都可以进行克隆操作。  
```shell
# 下面的操作可以允许通过 HTTP 对仓库进行读取：
$ cd /var/www/htdocs/
$ git clone --bare /path/to/git_project gitproject.git
$ cd gitproject.git
$ mv hooks/post-update.sample hooks/post-update
$ chmod a+x hooks/post-update
# Git 附带的 post-update 挂钩会默认运行合适的命令（git update-server-info）来确保通过 HTTP 的获取和克隆正常工作。这条命令在你用 SSH 向仓库推送内容时运行；之后，其他人就可以用下面的命令来克隆仓库：
$ git clone http://example.com/gitproject.git
# 在本例中，我们使用了 Apache 设定中常用的 /var/www/htdocs 路径，不过你可以使用任何静态 web 服务 — 把裸仓库放在它的目录里就行。 Git 的数据是以最基本的静态文件的形式提供的。
```
通过 HTTP 进行推送操作也是可能的，不过这种做法不太常见，并且牵扯到复杂的 WebDAV 设定。如果对 HTTP 推送协议感兴趣，不妨打开这个地址看一下操作方法：[http://www.kernel.org/pub/software/scm/git/docs/howto/setup-git-server-over-http.txt]()
通过 HTTP 推送的好处之一是你可以使用任何 WebDAV 服务器，不需要为 Git 设定特殊环境；所以如果主机提供商支持通过 WebDAV 更新网站内容，你也可以使用这项功能。

**优点**  
使用 HTTP 协议：  
易于架设。几条必要的命令就可以让全世界读取到仓库的内容。花费不过几分钟。  
HTTP 协议不会占用过多服务器资源。因为它一般只用到静态的 HTTP 服务提供所有数据，普通的 Apache 服务器平均每秒能支撑数千个文件的并发访问 — 哪怕让一个小型服务器超载都很难。 
使用 HTTPS 协议：  
提供只读的仓库，这意味着你可以加密传输内容；你甚至可以要求客户端使用特定签名的 SSL 证书。一般情况下，如果到了这一步，使用 SSH 公共密钥可能是更简单的方案；不过也存在一些特殊情况，这时通过 HTTPS 使用带签名的 SSL 证书或者其他基于 HTTP 的只读连接授权方式是更好的解决方案。  
HTTP 还有个额外的好处：HTTP 是一个如此常见的协议，以至于企业级防火墙通常都允许其端口的通信。  

**缺点**
相对来说客户端效率更低。克隆或者下载仓库内容可能会花费更多时间。  
HTTP 传输的体积和网络开销比其他任何一个协议都大。  
它没有按需供应的能力 — 传输过程中没有服务端的动态计算 — 因而 HTTP 协议经常会被称为傻瓜（dumb）协议。  

## 2. 在服务器上部署 Git

开始架设 Git 服务器前，需要先把现有仓库导出为裸仓库 — 即一个不包含当前工作目录的仓库。克隆时用 `--bare` 选项即可。裸仓库的目录名一般以 `.git` 结尾，像这样：
```shell
$ git clone --bare my_project my_project.git
Cloning into bare repository 'my_project.git'...
done.
```
其实 clone 操作基本上相当于 `git init` 加 `git fetch`，所以这里出现的其实是 `git init` 的输出，先由它建立一个空目录，而之后传输数据对象的操作并无任何输出，只是悄悄在幕后执行。  

### 1. 把裸仓库移到服务器上

有了裸仓库的副本后，剩下的就是把它放到服务器上并设定相关协议。
```shell
# 假设一个域名为 git.example.com 的服务器已经架设好，并可以通过 SSH 访问，我们打算把所有 Git 仓库储存在 /opt/git 目录下。只要把裸仓库复制过
$ scp -r my_project.git user@git.example.com:/opt/git
# 所有对该服务器有 SSH 访问权限，并可读取 /opt/git 目录的用户都可以用下面的命令克隆该项目：
$ git clone user@git.example.com:/opt/git/my_project.git
# 如果某个 SSH 用户对 /opt/git/my_project.git 目录有写权限，那他就有推送权限。如果到该项目目录中运行 git init 命令，并加上 --shared 选项，那么 Git 会自动修改该仓库目录的组权限为可写（译注：实际上 --shared 可以指定其他行为，只是默认为将组权限改为可写并执行 g+sx，所以最后会得到 rws。）。
$ ssh user@git.example.com
$ cd /opt/git/my_project.git
$ git init --bare --shared
# 这是架设一个少数人具有连接权的 Git 服务的全部 — 只要在服务器上加入可以用 SSH 登录的帐号，然后把裸仓库放在大家都有读写权限的地方。一切都准备停当，无需更多。
```
### 3. 小型安装

如果设备较少或者你只想在小型开发团队里尝试 Git ，那么一切都很简单。架设 Git 服务最复杂的地方在于账户管理。如果需要仓库对特定的用户可读，而给另一部分用户读写权限，那么访问和许可的安排就比较困难。  

1. SSH 连接
如果已经有了一个所有开发成员都可以用 SSH 访问的服务器，架设第一个服务器将变得异常简单，几乎什么都不用做（正如上节中介绍的那样）。如果需要对仓库进行更复杂的访问控制，只要使用服务器操作系统的本地文件访问许可机制就行了。  
如果需要团队里的每个人都对仓库有写权限，又不能给每个人在服务器上建立账户，那么提供 SSH 连接就是唯一的选择了。我们假设用来共享仓库的服务器已经安装了 SSH 服务，而且你通过它访问服务器。  
一个办法是给每个人建立一个账户，直截了当但略过繁琐。反复运行 `adduser` 并给所有人设定临时密码可不是好玩的。  
第二个办法是在主机上建立一个 `git` 账户，让每个需要写权限的人发送一个 `SSH` 公钥，然后将其加入 `git` 账户的 `~/.ssh/authorized_keys` 文件。这样一来，所有人都将通过 `git` 账户访问主机。这丝毫不会影响提交的数据 — 访问主机用的身份不会影响提交对象的提交者信息。  
另一个办法是让 SSH 服务器通过某个 LDAP 服务，或者其他已经设定好的集中授权机制，来进行授权。只要每个人都能获得主机的 shell 访问权，任何可用的 SSH 授权机制都能达到相同效果。

## 3. 生成 SSH 公钥
生成公钥的过程在所有操作系统上都差不多。 首先先确认一下是否已经有一个公钥了。SSH 公钥默认储存在账户的主目录下的 `~/.ssh` 目录。  
```shell
# 查看有没有 SSH 公钥
$ cd ~/.ssh
$ ls
authorized_keys2  id_dsa       known_hosts
config            id_dsa.pub
# 关键是看有没有用 something 和 something.pub 来命名的一对文件，这个 something 通常就是 id_dsa 或 id_rsa。有 .pub 后缀的文件就是公钥，另一个文件则是密钥。假如没有这些文件，或者干脆连 .ssh 目录都没有，可以用 ssh-keygen 来创建。该程序在 Linux/Mac 系统上由 SSH 包提供，而在 Windows 上则包含在 MSysGit 包里：
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/schacon/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/schacon/.ssh/id_rsa.
Your public key has been saved in /Users/schacon/.ssh/id_rsa.pub.
The key fingerprint is:
43:c5:5b:5f:b1:f1:50:43:ad:20:a6:92:6a:1f:9a:3a schacon@agadorlaptop.local
# 它先要求你确认保存公钥的位置（.ssh/id_rsa），然后它会让你重复一个密码两次，如果不想在使用公钥的时候输入密码，可以留空。

```
所有做过这一步的用户都得把它们的公钥给你或者 Git 服务器的管理员（假设 SSH 服务被设定为使用公钥机制）。他们只需要复制 .pub 文件的内容然后发邮件给管理员。公钥的样子大致如下：  
```
$ cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAklOUpkDHrfHY17SbrmTIpNLTGK9Tjom/BWDSU
GPl+nafzlHDTYW7hdI4yZ5ew18JH4JW9jbhUFrviQzM7xlELEVf4h9lFX5QVkbPppSwg0cda3
Pbv7kOdJ/MTyBlWXFCR+HAo3FXRitBqxiX1nKhXpHAZsMciLq8V6RjsNAQwdsdMFvSlVK/7XA
t3FaoJoAsncM1Q9x5+3V0Ww68/eIFmb1zuUFljQJKprrX88XypNDvjYNby6vw/Pb0rwert/En
mZ+AW4OZPnTPI89ZPmVMLuayrD2cE86Z/il8b+gw3r3+1nKatmIkjn2so1d01QraTlMqVSsbx
NrRFi9wrf+M7Q== schacon@agadorlaptop.local
```
> 关于在多个操作系统上设立相同 SSH 公钥的教程，可以查阅 GitHub 上有关 SSH 公钥的向导：[http://github.com/guides/providing-your-ssh-key]()。

## 4. 架设服务器

现在我们过一边服务器端架设 SSH 访问的流程。本例将使用 `authorized_keys` 方法来给用户授权。我们还将假定使用类似 Ubuntu 这样的标准 Linux 发行版。
```shell
# 首先，创建一个名为 `git` 的用户，并为其创建一个 `.ssh` 目录
$ sudo adduser git
$ su git
$ cd
$ mkdir .ssh
# 把开发者的 SSH 公钥添加到这个用户的 authorized_keys 文件中。只要把它们逐个追加到 authorized_keys 文件尾部即可：
$ cat /tmp/id_rsa.john.pub >> ~/.ssh/authorized_keys
# 现在可以用 --bare 选项运行 git init 来建立一个裸仓库，这会初始化一个不包含工作目录的仓库。
$ cd /opt/git
$ mkdir project.git
$ cd project.git
$ git --bare init
# 这时，Join 就可以把它加为远程仓库，推送一个分支，从而把第一个版本的项目文件上传到仓库里了。
```
```shell
# 每次添加一个新项目都需要通过 shell 登入主机并创建一个裸仓库目录。我们不妨以 gitserver 作为 git 用户及项目仓库所在的主机名。如果在网络内部运行该主机，并在 DNS 中设定 gitserver 指向该主机，那么以下这些命令都是可用的：
# 在 John 的电脑上
$ cd myproject
$ git init
$ git add .
$ git commit -m 'initial commit'
$ git remote add origin git@gitserver:/opt/git/project.git
$ git push origin master
# 其他人的克隆和推送也一样变得很简单：
$ git clone git@gitserver:/opt/git/project.git
$ cd project
$ vim README
$ git commit -am 'fix for the README file'
$ git push origin master
```
用这个方法可以很快捷地为少数几个开发者架设一个可读写的 Git 服务。  
```shell
# 作为一个额外的防范措施，你可以用 Git 自带的 git-shell 工具限制 git 用户的活动范围。只要把它设为 git 用户登入的 shell，那么该用户就无法使用普通的 bash 或者 csh 什么的 shell 程序。编辑 /etc/passwd 文件：
$ sudo vim /etc/passwd
# 在文件末尾，你应该能找到类似这样的行：
git:x:1000:1000::/home/git:/bin/sh
# 把 bin/sh 改为 /usr/bin/git-shell （或者用 which git-shell 查看它的实际安装路径）。该行修改后的样子如下：
git:x:1000:1000::/home/git:/usr/bin/git-shell
# 现在 git 用户只能用 SSH 连接来推送和获取 Git 仓库，而不能直接使用主机 shell。尝试普通 SSH 登录的话，会看到下面这样的拒绝信息：
$ ssh git@gitserver
fatal: What do you think I am? A shell?
Connection to gitserver closed.
```

## 5. 公共访问

或许对小型的配置来说最简单的办法就是运行一个静态 web 服务，把它的根目录设定为 Git 仓库所在的位置，然后开启 `post-update` 挂钩。假设仓库处于 `/opt/git` 目录，主机上运行着 Apache 服务。任何 web 服务程序都可以达到相同效果；作为范例，我们将用一些基本的 Apache 设定来展示大体需要的步骤。
```shell
# 首先，开启挂钩：
$ cd project.git
$ mv hooks/post-update.sample hooks/post-update
$ chmod a+x hooks/post-update
# post-update 挂钩内容大致如下：
$ cat .git/hooks/post-update
#!/bin/sh
#
# An example hook script to prepare a packed repository for use over
# dumb transports.
#
# To enable this hook, rename this file to "post-update".
#

exec git-update-server-info
# 意思是当通过 SSH 向服务器推送时，Git 将运行这个 git-update-server-info 命令来更新匿名 HTTP 访问获取数据时所需要的文件。
# 接下来，在 Apache 配置文件中添加一个 VirtualHost 条目，把文档根目录设为 Git 项目所在的根目录。这里我们假定 DNS 服务已经配置好，会把对 .gitserver 的请求发送到这台主机：
<VirtualHost *:80>
    ServerName git.gitserver
    DocumentRoot /opt/git
    <Directory /opt/git/>
        Order allow, deny
        allow from all
    </Directory>
</VirtualHost>
# 另外，需要把 /opt/git 目录的 Unix 用户组设定为 www-data ，这样 web 服务才可以读取仓库内容，因为运行 CGI 脚本的 Apache 实例进程默认就是以该用户的身份起来的：
$ chgrp -R www-data /opt/git
# 重启 Apache 之后，就可以通过项目的 URL 来克隆该目录下的仓库了。
$ git clone http://git.gitserver/project.git
```
这一招可以让你在几分钟内为相当数量的用户架设好基于 HTTP 的读取权限。另一个提供非授权访问的简单方法是开启一个 Git 守护进程，不过这将要求该进程作为后台进程常驻 — 接下来就要讨论这方面的细节。 

## 6. GitWeb

Git 自带一个叫做 GitWeb 的 CGI 脚本，运行效果可以到 [http://git.kernel.org]() 这样的站点体验下  

如果想看看自己项目的效果，不妨用 Git 自带的一个命令，可以使用类似 `lighttpd` 或 `webrick` 这样轻量级的服务器启动一个临时进程。如果是在 Linux 主机上，通常都预装了 `lighttpd` ，可以到项目目录中键入 `git instaweb` 来启动。如果用的是 Mac ，`Leopard` 预装了 Ruby，所以 `webrick` 应该是最好的选择。如果要用 `lighttpd` 以外的程序来启动 `git instaweb`，可以通过 `--httpd` 选项指定：  
```shell
$ git instaweb --httpd=webrick
[2009-02-21 10:02:21] INFO  WEBrick 1.3.1
[2009-02-21 10:02:21] INFO  ruby 1.8.6 (2008-03-03) [universal-darwin9.0]
```
这会在 1234 端口开启一个 HTTPD 服务，随之在浏览器中显示该页，十分简单。关闭服务时，只需在原来的命令后面加上 --stop 选项就可以了：  
```shell
$ git instaweb --httpd=webrick --stop
```

如果需要为团队或者某个开源项目长期运行 GitWeb，那么 CGI 脚本就要由正常的网页服务来运行。一些 Linux 发行版可以通过 apt 或 yum 安装一个叫做 gitweb 的软件包，不妨首先尝试一下。  
以下介绍手动安装：  
```shell
# 手动安装 GitWeb 的流程
# 首先，你需要 Git 的源码，其中带有 GitWeb，并能生成定制的 CGI 脚本：
$ git clone git://git.kernel.org/pub/scm/git/git.git
$ cd git/
$ make GITWEB_PROJECTROOT="/opt/git" \
        prefix=/usr gitweb
$ sudo cp -Rf gitweb /var/www/
# 注意，通过指定 GITWEB_PROJECTROOT 变量告诉编译命令 Git 仓库的位置。
# 然后，设置 Apache 以 CGI 方式运行该脚本，添加一个 VirtualHost 配置：
<VirtualHost *:80>
    ServerName gitserver
    DocumentRoot /var/www/gitweb
    <Directory /var/www/gitweb>
        Options ExecCGI +FollowSymLinks +SymLinksIfOwnerMatch
        AllowOverride All
        order allow,deny
        Allow from all
        AddHandler cgi-script cgi
        DirectoryIndex gitweb.cgi
    </Directory>
</VirtualHost>
# GitWeb 可以使用任何兼容 CGI 的网页服务来运行；如果偏向使用其他 web 服务器，配置也不会很麻烦。
# 通过 http://gitserver 就可以在线访问仓库了，在 http://git.server 上还可以通过 HTTP 克隆和获取仓库的内容。
```

## 7. Gitosis

把所有用户的公钥保存在 `authorized_keys` 文件的做法，只能凑和一阵子，当用户数量达到几百人的规模时，管理起来就会十分痛苦。每次改删用户都必须登录服务器不去说，这种做法还缺少必要的权限管理 — 每个人都对所有项目拥有完整的读写权限。  
Gitosis 就是一套用来管理 `authorized_keys` 文件和实现简单连接限制的脚本。有趣的是，用来添加用户和设定权限的并非通过网页程序，而只是管理一个特殊的 Git 仓库。你只需要在这个特殊仓库内做好相应的设定，然后推送到服务器上，Gitosis 就会随之改变运行策略。  

```shell
# 用 Linux 服务器架设起来最简单 — 以下例子中，我们使用装有 Ubuntu 8.10 系统的服务器。  
# Gitosis 的工作依赖于某些 Python 工具，所以首先要安装 Python 的 setuptools 包，在 Ubuntu 上称为 python-setuptools：
$ apt-get install python-setuptools
# 接下来，从 Gitosis 项目主页克隆并安装：
$ git clone https://github.com/tv42/gitosis.git
$ cd gitosis
$ sudo python setup.py install
# 这会安装几个供 Gitosis 使用的工具。默认 Gitosis 会把 /home/git 作为存储所有 Git 仓库的根目录，这没什么不好，不过我们之前已经把项目仓库都放在 /opt/git 里面了，所以为方便起见，我们可以做一个符号连接，直接划转过去，而不必重新配置：
$ ln -s /opt/git /home/git/repositories
# Gitosis 将会帮我们管理用户公钥，所以先把当前控制文件改名备份，以便稍后重新添加，准备好让 Gitosis 自动管理 authorized_keys 文件：
$ mv /home/git/.ssh/authorized_keys /home/git/.ssh/ak.bak
# 接下来，如果之前把 git 用户的登录 shell 改为 git-shell 命令的话，先恢复 'git' 用户的登录 shell。改过之后，大家仍然无法通过该帐号登录（译注：因为 authorized_keys 文件已经没有了。），不过不用担心，这会交给 Gitosis 来实现。所以现在先打开 /etc/passwd 文件，把这行：
git:x:1000:1000::/home/git:/usr/bin/git-shell
# 改回:
git:x:1000:1000::/home/git:/bin/sh
# 好了，现在可以初始化 Gitosis 了。你可以用自己的公钥执行 gitosis-init 命令，要是公钥不在服务器上，先临时复制一份：
$ sudo -H -u git gitosis-init < /tmp/id_dsa.pub
Initialized empty Git repository in /opt/git/gitosis-admin.git/
Reinitialized existing Git repository in /opt/git/gitosis-admin.git/
# 这样该公钥的拥有者就能修改用于配置 Gitosis 的那个特殊 Git 仓库了。接下来，需要手工对该仓库中的 post-update 脚本加上可执行权限：
$ sudo chmod 755 /opt/git/gitosis-admin.git/hooks/post-update
# 如果设定过程没出什么差错，现在可以试一下用初始化 Gitosis 的公钥的拥有者身份 SSH 登录服务器，应该会看到类似下面这样：
$ ssh git@gitserver
PTY allocation request failed on channel 0
ERROR:gitosis.serve.main:Need SSH_ORIGINAL_COMMAND in environment.
  Connection to gitserver closed.
# 说明 Gitosis 认出了该用户的身份，但由于没有运行任何 Git 命令，所以它切断了连接。那么，现在运行一个实际的 Git 命令 — 克隆 Gitosis 的控制仓库：
# 在你本地计算机上
$ git clone git@gitserver:gitosis-admin.git
# 这会得到一个名为 gitosis-admin 的工作目录，主要由两部分组成：
$ cd gitosis-admin
$ find .
./gitosis.conf # 设置用户、仓库和权限的控制文件
./keydir # 存所有具有访问权限用户公钥的地方—每人一个
./keydir/scott.pub

# gitosis.conf 文件的内容，它应该只包含与刚刚克隆的 gitosis-admin 相关的信息：
$ cat gitosis.conf
[gitosis]

[group gitosis-admin]
members = scott
writable = gitosis-admin
# 它显示用户 scott — 初始化 Gitosis 公钥的拥有者 — 是唯一能管理 gitosis-admin 项目的人。

# 现在我们来添加一个新项目。为此我们要建立一个名为 mobile 的新段落，在其中罗列手机开发团队的开发者，以及他们拥有写权限的项目。由于 'scott' 是系统中的唯一用户，我们把他设为唯一用户，并允许他读写名为 iphone_project 的新项目：
[group mobile]
members = scott
writable = iphone_project
# 修改完之后，提交 gitosis-admin 里的改动，并推送到服务器使其生效：
$ git commit -am 'add iphone_project and mobile group'
[master 8962da8] add iphone_project and mobile group
 1 file changed, 4 insertions(+)
$ git push origin master
Counting objects: 5, done.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 272 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@gitserver:gitosis-admin.git
   fb27aec..8962da8  master -> master

# 在新工程 iphone_project 里首次推送数据到服务器前，得先设定该服务器地址为远程仓库。但你不用事先到服务器上手工创建该项目的裸仓库— Gitosis 会在第一次遇到推送时自动创建：
$ git remote add origin git@gitserver:iphone_project.git
$ git push origin master
Initialized empty Git repository in /opt/git/iphone_project.git/
Counting objects: 3, done.
Writing objects: 100% (3/3), 230 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@gitserver:iphone_project.git
 * [new branch]      master -> master
# 请注意，这里不用指明完整路径（实际上，如果加上反而没用），只需要一个冒号加项目名字即可 — Gitosis 会自动帮你映射到实际位置。

# 要和朋友们在一个项目上协同工作，就得重新添加他们的公钥。不过这次不用在服务器上一个一个手工添加到 ~/.ssh/authorized_keys 文件末端，而只需管理 keydir 目录中的公钥文件。文件的命名将决定在 gitosis.conf 中对用户的标识。现在我们为 John，Josie 和 Jessica 添加公钥：
$ cp /tmp/id_rsa.john.pub keydir/john.pub
$ cp /tmp/id_rsa.josie.pub keydir/josie.pub
$ cp /tmp/id_rsa.jessica.pub keydir/jessica.pub
# 然后把他们都加进 'mobile' 团队，让他们对 iphone_project 具有读写权限：
[group mobile]
members = scott john josie jessica
writable = iphone_project
# 如果你提交并推送这个修改，四个用户将同时具有该项目的读写权限。
# Gitosis 也具有简单的访问控制功能。如果想让 John 只有读权限，可以这样做：
[group mobile]
members = scott josie jessica
writable = iphone_project

[group mobile_ro]
members = john
readonly = iphone_project
# 现在 John 可以克隆和获取更新，但 Gitosis 不会允许他向项目推送任何内容。像这样的组可以随意创建，多少不限，每个都可以包含若干不同的用户和项目。甚至还可以指定某个组为成员之一（在组名前加上 @ 前缀），自动继承该组的成员：
[group mobile_committers]
members = scott josie jessica

[group mobile]
members   = @mobile_committers
writable  = iphone_project

[group mobile_2]
members   = @mobile_committers john
writable  = another_iphone_project

# 如果遇到意外问题，试试看把 loglevel=DEBUG 加到 [gitosis] 的段落（译注：把日志设置为调试级别，记录更详细的运行信息。）。如果一不小心搞错了配置，失去了推送权限，也可以手工修改服务器上的 /home/git/.gitosis.conf 文件 — Gitosis 实际是从该文件读取信息的。它在得到推送数据时，会把新的 gitosis.conf 存到该路径上。所以如果你手工编辑该文件的话，它会一直保持到下次向 gitosis-admin 推送新版本的配置内容为止。
```
## 8. Gitolite

最新的[版本](http://sitaramc.github.com/gitolite/progit.html)

Gitolite 是在Git之上的一个授权层，依托 `sshd` 或者 `httpd` 来进行认证。（概括：认证是确定用户是谁，授权是决定该用户是否被允许做他想做的事情）。  
Gitolite允许你定义访问许可而不只作用于仓库，而同样于仓库中的每个branch和tag name。你可以定义确切的人(或一组人)只能push特定的"refs"(或者branches或者tags)而不是其他人。  

**安装**
假设git，perl，和一个openssh兼容的ssh服务器已经装好了。在下面的例子里，我们会用git账户在gitserver进行。  
Gitolite是不同于“服务”的软件 -- 其通过ssh访问, 而且每个在服务器上的userid都是一个潜在的“gitolite主机”。我们在这里描述最简单的安装方法，对于其他方法，请参考其文档。  
```shell
# Gitolite 安装
# 开始，在你的服务器上创建一个名为git的用户，然后以这个用户登录。从你的工作站拷贝你的SSH公钥（也就是你用ssh-keygen默认生成的~/.ssh/id_dsa.pub文件），重命名为<yourname>.pub（我们这里使用scott.pub作为例子）。然后执行下面的命令：
$ git clone git://github.com/sitaramc/gitolite
$ gitolite/install -ln
    # assumes $HOME/bin exists and is in your $PATH
$ gitolite setup -pk $HOME/scott.pub
# 最后一个命令在服务器上创建了一个名为gitolite-admin的Git仓库。

# 最后，回到你的工作站，执行git clone git@gitserver:gitolite-admin。然后你就完成了！Gitolite现在已经安装在了服务器上，在你的工作站上，你也有一个名为gitolite-admin的新仓库。你可用通过更改这个仓库以及推送到服务器上来管理你的Gitolite配置。
```

**定制安装**
有一些定制安装方法如果你用的上的话。一些设置可以通过编辑rc文件来简单地改变，但是如果这个不够，有关于定制Gitolite的文档供参考。  

1. 配置文件和访问规则  

安装结束后，你切换到gitolite-admin仓库（放在你的HOME目录）然后看看都有啥：
```shell
$ cd ~/gitolite-admin/
$ ls
conf/  keydir/
$ find conf keydir -type f
conf/gitolite.conf
keydir/scott.pub
$ cat conf/gitolite.conf

repo gitolite-admin
    RW+                 = scott

repo testing
    RW+                 = @all
```
注意 "scott" ( 之前用 `gl-setup` 命令时候的 `pubkey` 名稱) 有读写权限而且在 `gitolite-admin` 仓库里有一个同名的公钥文件。  

添加用户很简单。为了添加一个名为 `alice` 的用户，获取她的公钥，命名为 `alice.pub`，然后放到在你工作站上的 `gitolite-admin` 克隆的 `keydir` 目录。添加，提交，然后推送更改。这样用户就被添加了。  
`gitolite` 配置文件的语法在 `conf/example.conf` 里，我们只会提到一些主要的。  
你可以给用户或者仓库分组。分组名就像一些宏；定义的时候，无所谓他们是工程还是用户；区别在于你使用“宏”的时候  
```
@oss_repos      = linux perl rakudo git gitolite
@secret_repos   = fenestra pear

@admins         = scott
@interns        = ashok
@engineers      = sitaram dilbert wally alice
@staff          = @admins @engineers @interns
```
你可以控制许可在”ref“级别。在下面的例子里，实习生可以push ”int“分支。工程师可以push任何有"eng-"开头的branch，还有refs/tags下面用"rc"开头的后面跟数字的。而且管理员可以随便更改(包括rewind)对任何参考名。  
```
repo @oss_repos
    RW  int$                = @interns
    RW  eng-                = @engineers
    RW  refs/tags/rc[0-9]   = @engineers
    RW+                     = @admins
```
在 `RW` or `RW+` 之后的表达式是正则表达式(regex)对应着后面的 push 用的参考名字(ref)。所以我们叫它”参考正则“（refex）！当然，一个 refex 可以比这里表现的更强大，所以如果你对 perl 的正则表达式不熟的话就不要改过头。  

同样，你可能猜到了，Gitolite 字头 `refs/heads/` 是一个便捷句法如果参考正则没有用 `refs/` 开头。  

一个这个配置文件语法的重要功能是，所有的仓库的规则不需要在同一个位置。你能报所有普通的东西放在一起，就像上面的对所有 oss_repos 的规则那样，然后建一个特殊的规则对后面的特殊案例，就像：  
```
repo gitolite
    RW+                     = sitaram
```
那条规则刚刚加入规则集的 gitolite 仓库.  

这次你可能会想要知道访问控制规则是如何应用的，我们简要介绍一下。  
在gitolite里有两级访问控制。第一是在仓库级别；如果你已经读或者写访问过了任何在仓库里的参考，那么你已经读或者写访问仓库了。  
第二级，应用只能写访问，通过在仓库里的 branch 或者 tag。用户名如果尝试过访问 (`W`或`+`)，参考名被更新为已知。访问规则检查是否出现在配置文件里，为这个联合寻找匹配 (但是记得参考名是正则匹配的，不是字符串匹配的)。如果匹配被找到了，push 就成功了。不匹配的访问会被拒绝。  

2. 带'拒绝'的高级访问控制  

目前，我们只看过了许可是 `R` , `RW`, 或者RW+这样子的。但是 gitolite 还允许另外一种许可：`-`，代表 ”拒绝“。这个给了你更多的能力，当然也有一点复杂，因为不匹配并不是唯一的拒绝访问的方法，因此规则的顺序变得无关了！  
在前面的情况中，我们想要工程师可以 rewind 任意 branch 除了 master 和 integ 。 这里是如何做到的
```
    RW  master integ    = @engineers
    -   master integ    = @engineers
    RW+                 = @engineers
```
你再一次简单跟随规则从上至下知道你找到一个匹配你的访问模式的，或者拒绝。非rewind push到master或者integ 被第一条规则允许。一个rewind push到那些refs不匹配第一条规则，掉到第二条，因此被拒绝。任何push(rewind或非rewind)到参考或者其他master或者integ不会被前两条规则匹配，即被第三条规则允许。  

3. 通过改变文件限制 push  

此外限制用户push改变到哪条branch的，你也可以限制哪个文件他们可以碰的到。  
可能 Makefile (或者其他哪些程序) 真的不能被任何人做任何改动，你可以告诉 gitolite:  
```
repo foo
    RW                      =   @junior_devs @senior_devs

    -   VREF/NAME/Makefile  =   @junior_devs
```
4. 个人分支  

Gitolite也支持一个叫”个人分支“的功能 (或者叫, ”个人分支命名空间“) 在合作环境里非常有用。  
在 git世界里许多代码交换通过”pull“请求发生。然而在合作环境里，委任制的访问是‘绝不’，一个开发者工作站不能认证，你必须push到中心服务器并且叫其他人从那里pull。  
这个通常会引起一些branch名称簇变成像 VCS里一样集中化，加上设置许可变成管理员的苦差事。  
Gitolite让你定义一个”个人的“或者”乱七八糟的”命名空间字首给每个开发人员(比如， `refs/personal/<devname>/*`)；


5. "通配符" 仓库  

Gitolite 允许你定义带通配符的仓库(其实还是perl正则式), 比如 `assignments/s[0-9][0-9]/a[0-9][0-9]`。 这是一个非常有用的功能，需要通过设置`$GL_WILDREPOS = 1`; 在 rc 文件中启用。允许你安排一个新许可模式("C")允许用户创建仓库基于通配符，自动分配拥有权对特定用户 - 创建者，允许他交出 R和 RW许可给其他合作用户等等。这个功能在`doc/4-wildcard-repositories.mkd` 文档里  

6. 其他功能  

**记录**: Gitolite 记录所有成功的访问。如果你太放松给了别人 rewind 许可 (RW+) 和其他人弄没了 "master"， 记录文件会救你的命，如果其他简单快速的找到 SHA 都不管用。  

**访问权报告**: 另一个方便的功能是你尝试用 ssh 连接到服务器的时候发生了什么。Gitolite 告诉你哪个 repos你访问过，那个访问可能是什么。这里是例子：
```
   hello scott, this is git@git running gitolite3 v3.01-18-g9609868 on git 1.7.4.4

         R     anu-wsd
         R     entrans
         R  W  git-notes
         R  W  gitolite
         R  W  gitolite-admin
         R     indic_web_input
         R     shreelipi_converter
```
**委托**：真正的大安装，你可以把责任委托给一组仓库给不同的人然后让他们独立管理那些部分。这个减少了主管理者的负担，让他瓶颈更小。这个功能在他自己的文档目录里的 doc/下面。

**镜像**: Gitolite 可以帮助你维护多个镜像，如果主服务器挂掉的话在他们之间很容易切换。

## 9. Git 守护进程  

对于提供公共的，非授权的只读访问，我们可以抛弃 HTTP 协议，改用 Git 自己的协议，这主要是出于性能和速度的考虑。Git 协议远比 HTTP 协议高效，因而访问速度也快，所以它能节省很多用户的时间。  
这一点只适用于非授权的只读访问。如果建在防火墙之外的服务器上，那么它所提供的服务应该只是那些公开的只读项目。如果是在防火墙之内的服务器上，可用于支撑大量参与人员或自动系统（用于持续集成或编译的主机）只读访问的项目，这样可以省去逐一配置 SSH 公钥的麻烦。  

但不管哪种情形，Git 协议的配置设定都很简单。基本上，只要以守护进程的形式运行该命令即可：  
```shell
git daemon --reuseaddr --base-path=/opt/git/ /opt/git/
# 这里的 --reuseaddr 选项表示在重启服务前，不等之前的连接超时就立即重启。而 --base-path 选项则允许克隆项目时不必给出完整路径。最后面的路径告诉 Git 守护进程允许开放给用户访问的仓库目录。假如有防火墙，则需要为该主机的 9418 端口设置为允许通信。
```
以守护进程的形式运行该进程的方法有很多，但主要还得看用的是什么操作系统。在 Ubuntu 主机上，可以用 Upstart 脚本达成。编辑该文件：  
```shell
/etc/event.d/local-git-daemon
# 加以下内容
start on startup
stop on shutdown
exec /usr/bin/git daemon \
    --user=git --group=git \
    --reuseaddr \
    --base-path=/opt/git/ \
    /opt/git/
respawn
```
出于安全考虑，强烈建议用一个对仓库只有读取权限的用户身份来运行该进程 — 只需要简单地新建一个名为 `git-ro` 的用户（译注：新建用户默认对仓库文件不具备写权限，但这取决于仓库目录的权限设定。务必确认  `git-ro` 对仓库只能读不能写。），并用它的身份来启动进程。  

这样一来，当你重启计算机时，Git 进程也会自动启动。要是进程意外退出或者被杀掉，也会自行重启。在设置完成后，不重启计算机就启动该守护进程，可以运行：  
```shell
initctl start local-git-daemon
```
而在其他操作系统上，可以用 xinetd，或者 sysvinit 系统的脚本，或者其他类似的脚本 — 只要能让那个命令变为守护进程并可监控。  

我们必须告诉 Gitosis 哪些仓库允许通过 Git 协议进行匿名只读访问。如果每个仓库都设有各自的段落，可以分别指定是否允许 Git 进程开放给用户匿名读取。比如允许通过 Git 协议访问 iphone_project，可以把下面两行加到 gitosis.conf 文件的末尾：  
```
[repo iphone_project]
daemon = yes
```
在提交和推送完成后，运行中的 Git 守护进程就会响应来自 9418 端口对该项目的访问请求。  

如果不考虑 Gitosis，单单起了 Git 守护进程的话，就必须到每一个允许匿名只读访问的仓库目录内，创建一个特殊名称的空文件作为标志：  
```shell
$ cd /path/to/project.git
$ touch git-daemon-export-ok
```
该文件的存在，表明允许 Git 守护进程开放对该项目的匿名只读访问。  

Gitosis 还能设定哪些项目允许放在 `GitWeb` 上显示。先打开 `GitWeb` 的配置文件 `/etc/gitweb.conf`，添加以下四行：  
```
$projects_list = "/home/git/gitosis/projects.list";
$projectroot = "/home/git/repositories";
$export_ok = "git-daemon-export-ok";
@git_base_url_list = ('git://gitserver');
```

接下来，只要配置各个项目在 Gitosis 中的 `gitweb` 参数，便能达成是否允许 GitWeb 用户浏览该项目。比如，要让 iphone_project 项目在 `GitWeb` 里出现，把 repo 的设定改成下面的样子：  
```
[repo iphone_project]
daemon = yes
gitweb = yes
```
在提交并推送过之后，GitWeb 就会自动开始显示 iphone_project 项目的细节和历史。  

## 10. Git 托管服务  

托管服务列表：[https://git.wiki.kernel.org/index.php/GitHosting]()

# 分布式 Git  

接下来，我们要学习下如何利用 Git 来组织和完成分布式工作流程。  

## 1. 分布式工作流程  

在 Git 网络中，每个开发者同时扮演着节点和集线器的角色，这就是说，每一个开发者都可以将自己的代码贡献到另外一个开发者的仓库中，或者建立自己的公共仓库，让其他开发者基于自己的工作开始，为自己的仓库贡献代码。于是，Git 的分布式协作便可以衍生出种种不同的工作流程。

### 1. 集中式工作流  

集中式工作流程使用的都是单点协作模型。一个存放代码仓库的中心服务器，可以接受所有开发者提交的代码。所有的开发者都是普通的节点，作为中心集线器的消费者，平时的工作就是和中心仓库同步数据。  

如果两个开发者从中心仓库克隆代码下来，同时作了一些修订，那么只有第一个开发者可以顺利地把数据推送到共享服务器。第二个开发者在提交他的修订之前，必须先下载合并服务器上的数据，解决冲突之后才能推送数据到共享服务器上。在 Git 中这么用也决无问题，这就好比是在用 Subversion（或其他 CVCS）一样，可以很好地工作。

如果你的团队不是很大，或者大家都已经习惯了使用集中式工作流程，完全可以采用这种简单的模式。只需要配置好一台中心服务器，并给每个人推送数据的权限，就可以开展工作了。但如果提交代码时有冲突， Git 根本就不会让用户覆盖他人代码，它直接驳回第二个人的提交操作。这就等于告诉提交者，你所作的修订无法通过快进（fast-forward）来合并，你必须先拉取最新数据下来，手工解决冲突合并后，才能继续推送新的提交。 绝大多数人都熟悉和了解这种模式的工作方式，所以使用也非常广泛。 

### 2. 集成管理员工作流

由于 Git 允许使用多个远程仓库，开发者便可以建立自己的公共仓库，往里面写数据并共享给他人，而同时又可以从别人的仓库中提取他们的更新过来。这种情形通常都会有个代表着官方发布的项目仓库（blessed repository），开发者们由此仓库克隆出一个自己的公共仓库（developer public），然后将自己的提交推送上去，请求官方仓库的维护者拉取更新合并到主项目。维护者在自己的本地也有个克隆仓库（integration manager），他可以将你的公共仓库作为远程仓库添加进来，经过测试无误后合并到主干分支，然后再推送到官方仓库。 

1. 项目维护者可以推送数据到公共仓库 blessed repository
2. 贡献者克隆此仓库，修订或编写新代码。
3. 贡献者推送数据到自己的公共仓库 developer public
4. 贡献者给维护者发送邮件，请求拉取自己的最新修订
5. 维护者在自己本地的 integration manger 仓库中 将贡献者的仓库加为远程仓库，合并更新并做测试
6. 维护者将合并后的更新推送到主仓库 blessed repository  

在 GitHub 网站上使用得最多的就是这种工作流。人们可以复制（fork 亦即克隆）某个项目到自己的列表中，成为自己的公共仓库。随后将自己的更新提交到这个仓库，所有人都可以看到你的每次更新。这么做最主要的优点在于，你可以按照自己的节奏继续工作，而不必等待维护者处理你提交的更新；而维护者也可以按照自己的节奏，任何时候都可以过来处理接纳你的贡献。

### 3. 司令官与副官工作流  

这其实是上一种工作流的变体。一般超大型的项目才会用到这样的工作方式，像是拥有数百协作开发者的 Linux 内核项目就是如此。各个集成管理员分别负责集成项目中的特定部分，所以称为副官（lieutenant）。而所有这些集成管理员头上还有一位负责统筹的总集成管理员，称为司令官（dictator）。司令官维护的仓库用于提供所有协作者拉取最新集成的项目代码。  

1. 一般的开发者在自己的特性分支上工作，并不定期地根据主干分支（dictator 上的 master）衍合。
2. 副官（lieutenant）将普通开发者的特性分支合并到自己的 master 分支中。
3. 司令官（dictator）将所有副官的 master 分支并入自己的 master 分支。
4. 司令官（dictator）将集成后的 master 分支推送到共享仓库 blessed repository 中，以便所有其他开发者以此为基础进行衍合。  

这种工作流程并不常用，只有当项目极为庞杂，或者需要多级别管理时，才会体现出优势。利用这种方式，项目总负责人（即司令官）可以把大量分散的集成工作委托给不同的小组负责人分别处理，最后再统筹起来，如此各人的职责清晰明确，也不易出错（译注：此乃分而治之）。  

## 2. 为项目作贡献  

作为项目贡献者，有哪些常见的工作模式。  
Git 如此灵活，人们的协作方式便可以各式各样，没有固定不变的范式可循，而每个项目的具体情况又多少会有些不同，比如说参与者的规模，所选择的工作流程，每个人的提交权限，以及 Git 以外贡献等等，都会影响到具体操作的细节。  
1. 提交指南  

开始分析特定用例之前，先来了解下如何撰写提交说明。一份好的提交指南可以帮助协作者更轻松更有效地配合。Git 项目本身就提供了一份文档（Git 项目源代码目录中  [Documentation/SubmittingPatches](https://github.com/git/git/blob/master/Documentation/SubmittingPatches)），列数了大量提示，从如何编撰提交说明到提交补丁，不一而足。

1. 请不要在更新中提交多余的白字符（whitespace）。Git 有种检查此类问题的方法，在提交之前，先运行 `git diff --check`，会把可能的多余白字符修正列出来。下面的示例，我已经把终端中显示为红色的白字符用 X 替换掉：
```shell
$ git diff --check
lib/simplegit.rb:5: trailing whitespace.
+    @git_dir = File.expand_path(git_dir)XX
lib/simplegit.rb:7: trailing whitespace.
+ XXXXXXXXXXX
lib/simplegit.rb:26: trailing whitespace.
+    def command(git_cmd)XXXX
```
2. 请将每次提交限定于完成一次逻辑功能。并且可能的话，适当地分解为多次小更新，以便每次小型提交都更易于理解。
请不要在周末穷追猛打一次性解决五个问题，而最后拖到周一再提交。就算是这样也请尽可能利用暂存区域，将之前的改动分解为每次修复一个问题，再分别提交和加注说明。如果针对两个问题改动的是同一个文件，可以试试看 `git add --patch` 的方式将部分内容置入暂存区域。无论是五次小提交还是混杂在一起的大提交，最终分支末端的项目快照应该还是一样的，但分解开来之后，更便于其他开发者复阅。这么做也方便自己将来取消某个特定问题的修复。
3. 提交说明的撰写。写得好可以让大家协作起来更轻松。一般来说，提交说明最好限制在一行以内，50 个字符以下，简明扼要地描述更新内容，空开一行后，再展开详细注解。Git 项目本身需要开发者撰写详尽注解，包括本次修订的因由，以及前后不同实现之间的比较，我们也该借鉴这种做法。另外，提交说明应该用祈使现在式语态，比如，不要说成 “I added tests for” 或 “Adding tests for” 而应该用 “Add tests for”。 下面是来自 tpope.net 的 Tim Pope 原创的提交说明格式模版，供参考：
```
本次更新的简要描述（50 个字符以内）

如果必要，此处展开详尽阐述。段落宽度限定在 72 个字符以内。
某些情况下，第一行的简要描述将用作邮件标题，其余部分作为邮件正文。
其间的空行是必要的，以区分两者（当然没有正文另当别论）。
如果并在一起，rebase 这样的工具就可能会迷惑。

另起空行后，再进一步补充其他说明。

 - 可以使用这样的条目列举式。

 - 一般以单个空格紧跟短划线或者星号作为每项条目的起始符。每个条目间用一空行隔开。
   不过这里按自己项目的约定，可以略作变化。
```

2. 私有的小型团队  

一个私有项目，与你一起协作的还有另外一到两位开发者。这里说私有，是指源代码不公开，其他人无法访问项目仓库。而你和其他开发者则都具有推送数据到仓库的权限。这种情况下，你们可以用 Subversion 或其他集中式版本控制系统类似的工作流来协作。你仍然可以得到 Git 带来的其他好处：离线提交，快速分支与合并等等，但工作流程还是差不多的。主要区别在于，合并操作发生在客户端而非服务器上。  
3. 私有团队间协作  

如果有几个小组分头负责若干特性的开发和集成，那他们之间的协作过程是怎样的。使用典型的集成管理员式工作流，每个组都有一名管理员负责集成本组代码，及更新项目主仓库的 master 分支。所有开发都在代表小组的分支上进行。

4. 公开的小型项目  

要给公开项目作贡献，情况就有些不同了。因为你没有直接更新主仓库分支的权限，得寻求其它方式把工作成果交给项目维护人。下面会介绍两种方法，第一种使用 git 托管服务商提供的仓库复制功能，一般称作 fork，比如 repo.or.cz 和 GitHub 都支持这样的操作，而且许多项目管理员都希望大家使用这样的方式。另一种方法是通过电子邮件寄送文件补丁。但不管哪种方式，起先我们总需要克隆原始仓库，而后创建特性分支开展工作。

5. 公开的大型项目  

许多大型项目都会立有一套自己的接受补丁流程，你应该注意下其中细节。但多数项目都允许通过开发者邮件列表接受补丁。整个工作流程类似上面的情形：为每个补丁创建独立的特性分支，而不同之处在于如何提交这些补丁。不需要创建自己可写的公共仓库，也不用将自己的更新推送到自己的服务器，你只需将每次提交的差异内容以电子邮件的方式依次发送到邮件列表中即可。

## 3. 项目的管理

### 1. 使用特性分支进行工作  

如果想要集成新的代码进来，最好局限在特性分支上做。临时的特性分支可以让你随意尝试，进退自如。比如碰上无法正常工作的补丁，可以先搁在那边，直到有时间仔细核查修复为止。创建的分支可以用相关的主题关键字命名，比如 `ruby_client` 或者其它类似的描述性词语，以帮助将来回忆。Git 项目本身还时常把分支名称分置于不同命名空间下，比如 `sc/ruby_client` 就说明这是 `sc` 这个人贡献的。  
```shell
# 新建临时分支：
$ git branch sc/ruby_client master
# 如果你希望立即转到分支上去工作，可以用 checkout -b：
$ git checkout -b sc/ruby_client master
```
### 2. 采纳来自邮件的补丁  

如果收到一个通过电邮发来的补丁，你应该先把它应用到特性分支上进行评估。有两种应用补丁的方法：`git apply` 或者 `git am`。  

使用 apply 命令应用补丁  

如果收到的补丁文件是用 git diff 或由其它 Unix 的 diff 命令生成，就该用 git apply 命令来应用补丁。假设补丁文件存在 /tmp/patch-ruby-client.patch，可以这样运行：  
```shell
$ git apply /tmp/patch-ruby-client.patch
```
这会修改当前工作目录下的文件，效果基本与运行 `patch -p1` 打补丁一样，但它更为严格，且不会出现混乱。如果是 `git diff` 格式描述的补丁，此命令还会相应地添加，删除，重命名文件。当然，普通的 `patch` 命令是不会这么做的。另外请注意，`git apply` 是一个事务性操作的命令，也就是说，要么所有补丁都打上去，要么全部放弃。所以不会出现 `patch` 命令那样，一部分文件打上了补丁而另一部分却没有，这样一种不上不下的修订状态。所以总的来说，`git apply` 要比 `patch` 严谨许多。因为仅仅是更新当前的文件，所以此命令不会自动生成提交对象，你得手工缓存相应文件的更新状态并执行提交命令。  

在实际打补丁之前，可以先用 `git apply --check` 查看补丁是否能够干净顺利地应用到当前分支中：
```shell
$ git apply --check 0001-seeing-if-this-helps-the-gem.patch
error: patch failed: ticgit.gemspec:1
error: ticgit.gemspec: patch does not apply
```
如果没有任何输出，表示我们可以顺利采纳该补丁。如果有问题，除了报告错误信息之外，该命令还会返回一个非零的状态，所以在 shell 脚本里可用于检测状态。  

使用 am 命令应用补丁  
如果贡献者也用 Git，且擅于制作 `format-patch` 补丁，那你的合并工作将会非常轻松。因为这些补丁中除了文件内容差异外，还包含了作者信息和提交消息。所以请鼓励贡献者用 `format-patch` 生成补丁。对于传统的 `diff` 命令生成的补丁，则只能用 `git apply` 处理。  

对于 `format-patch` 制作的新式补丁，应当使用 `git am` 命令。从技术上来说，`git am` 能够读取 mbox 格式的文件。这是种简单的纯文本文件，可以包含多封电邮，格式上用 `From` 加空格以及随便什么辅助信息所组成的行作为分隔行，以区分每封邮件，就像这样：  
```
From 330090432754092d704da8e76ca5c05c198e71a8 Mon Sep 17 00:00:00 2001
From: Jessica Smith <jessica@example.com>
Date: Sun, 6 Apr 2008 10:17:23 -0700
Subject: [PATCH 1/2] add limit to log function

Limit log functionality to the first 20
```

这是 `format-patch` 命令输出的开头几行，也是一个有效的 `mbox` 文件格式。如果有人用 `git send-email` 给你发了一个补丁，你可以将此邮件下载到本地，然后运行 `git am` 命令来应用这个补丁。如果你的邮件客户端能将多封电邮导出为 `mbox` 格式的文件，就可以用 `git am` 一次性应用所有导出的补丁。  

如果贡献者将 `format-patch` 生成的补丁文件上传到类似 Request Ticket 一样的任务处理系统，那么可以先下载到本地，继而使用 `git am` 应用该补丁：  
```shell
$ git am 0001-limit-log-function.patch
Applying: add limit to log function
```
你会看到它被干净地应用到本地分支，并自动创建了新的提交对象。作者信息取自邮件头 `From` 和 `Date`，提交消息则取自 `Subject` 以及正文中补丁之前的内容  

有时，我们也会遇到打不上补丁的情况。这多半是因为主干分支和补丁的基础分支相差太远，但也可能是因为某些依赖补丁还未应用。这种情况下，`git am` 会报错并询问该怎么做：  
```shell
$ git am 0001-seeing-if-this-helps-the-gem.patch
Applying: seeing if this helps the gem
error: patch failed: ticgit.gemspec:1
error: ticgit.gemspec: patch does not apply
Patch failed at 0001.
When you have resolved this problem run "git am --resolved".
If you would prefer to skip this patch, instead run "git am --skip".
To restore the original branch and stop patching run "git am --abort".
```
Git 会在有冲突的文件里加入冲突解决标记，这同合并或衍合操作一样。解决的办法也一样，先编辑文件消除冲突，然后暂存文件，最后运行 `git am --resolved` 提交修正结果：  
```shell
$ (fix the file)
$ git add ticgit.gemspec
$ git am --resolved
Applying: seeing if this helps the gem
```
如果想让 Git 更智能地处理冲突，可以用 `-3` 选项进行三方合并。如果当前分支未包含该补丁的基础代码或其祖先，那么三方合并就会失败，所以该选项默认为关闭状态。一般来说，如果该补丁是基于某个公开的提交制作而成的话，你总是可以通过同步来获取这个共同祖先，所以用三方合并选项可以解决很多麻烦：  
```shell
$ git am -3 0001-seeing-if-this-helps-the-gem.patch
Applying: seeing if this helps the gem
error: patch failed: ticgit.gemspec:1
error: ticgit.gemspec: patch does not apply
Using index info to reconstruct a base tree...
Falling back to patching base and 3-way merge...
No changes -- Patch already applied.
```
像上面的例子，对于打过的补丁我又再打一遍，自然会产生冲突，但因为加上了 `-3` 选项，所以它很聪明地告诉我，无需更新，原有的补丁已经应用。  

对于一次应用多个补丁时所用的 `mbox` 格式文件，可以用 `am` 命令的交互模式选项 `-i`，这样就会在打每个补丁前停住，询问该如何操作  
```shell
$ git am -3 -i mbox
Commit Body is:
--------------------------
seeing if this helps the gem
--------------------------
Apply? [y]es/[n]o/[e]dit/[v]iew patch/[a]ccept all
```
在多个补丁要打的情况下，这是个非常好的办法，一方面可以预览下补丁内容，同时也可以有选择性的接纳或跳过某些补丁。  

打完所有补丁后，如果测试下来新特性可以正常工作，那就可以安心地将当前特性分支合并到长期分支中去了。  

### 3. 检出远程分支  

如果贡献者有自己的 Git 仓库，并将修改推送到此仓库中，那么当你拿到仓库的访问地址和对应分支的名称后，就可以加为远程分支，然后在本地进行合并。  

比如，Jessica 发来一封邮件，说在她代码库中的 `ruby-client` 分支上已经实现了某个非常棒的新功能，希望我们能帮忙测试一下。我们可以先把她的仓库加为远程仓库，然后抓取数据，完了再将她所说的分支检出到本地来测试：  
```shell
$ git remote add jessica git://github.com/jessica/myproject.git
$ git fetch jessica
$ git checkout -b rubyclient jessica/ruby-client
```
这种做法便于同别人保持长期的合作关系。但前提是要求贡献者有自己的服务器，而我们也需要为每个人建一个远程分支。有些贡献者提交代码补丁并不是很频繁，所以通过邮件接收补丁效率会更高。同时我们自己也不会希望建上百来个分支，却只从每个分支取一两个补丁。但若是用脚本程序来管理，或直接使用代码仓库托管服务，就可以简化此过程。  

使用远程分支的另外一个好处是能够得到提交历史。不管代码合并是不是会有问题，至少我们知道该分支的历史分叉点，所以默认会从共同祖先开始自动进行三方合并，无需 `-3` 选项，也不用像打补丁那样祈祷存在共同的基准点。  

如果只是临时合作，只需用 `git pull` 命令抓取远程仓库上的数据，合并到本地临时分支就可以了。一次性的抓取动作自然不会把该仓库地址加为远程仓库。  
```shell
$ git pull git://github.com/onetimeguy/project.git
From git://github.com/onetimeguy/project
 * branch            HEAD       -> FETCH_HEAD
Merge made by recursive.
```

### 4. 决断代码取舍  

现在特性分支上已合并好了贡献者的代码，是时候决断取舍了。  
一般我们会先看下，特性分支上都有哪些新增的提交。比如在 `contrib` 特性分支上打了两个补丁，仅查看这两个补丁的提交信息，可以用 `--not` 选项指定要屏蔽的分支 `master`，这样就会剔除重复的提交历史：  
```shell
$ git log contrib --not master
commit 5b6235bd297351589efc4d73316f0a68d484f118
Author: Scott Chacon <schacon@gmail.com>
Date:   Fri Oct 24 09:53:59 2008 -0700

    seeing if this helps the gem

commit 7482e0d16d04bea79d0dba8988cc78df655f16a0
Author: Scott Chacon <schacon@gmail.com>
Date:   Mon Oct 22 19:38:36 2008 -0700

    updated the gemspec to hopefully work better
```
还可以查看每次提交的具体修改。请牢记，在 `git log` 后加 `-p` 选项将展示每次提交的内容差异。
看当前分支同其他分支合并时的完整内容差异，
```shell
$ git diff master
```
虽然能得到差异内容，但请记住，结果有可能和我们的预期不同。一旦主干 `master` 在特性分支创建之后有所修改，那么通过 `diff` 命令来比较的，是最新主干上的提交快照。  
比方在 `master` 分支中某个文件里添了一行，然后运行上面的命令，简单的比较最新快照所得到的结论只能是，特性分支中删除了这一行。这个很好理解：如果 `master` 是特性分支的直接祖先，不会产生任何问题；如果它们的提交历史在不同的分叉上，那么产生的内容差异，看起来就像是增加了特性分支上的新代码，同时删除了 `master` 分支上的新代码。实际上我们真正想要看的，是新加入到特性分支的代码，也就是合并时会并入主干的代码。所以，准确地讲，我们应该比较特性分支和它同 `master` 分支的共同祖先之间的差异。  
我们可以手工定位它们的共同祖先，然后与之比较：  
```shell
$ git merge-base contrib master
36c7dba2c95e6bbb78dfa822519ecfec6e1ca649
$ git diff 36c7db
```
但这么做很麻烦，所以 Git 提供了便捷的 `...` 语法。对于 `diff` 命令，可以把 `...` 加在原始分支（拥有共同祖先）和当前分支之间：  
```shell
$ git diff master...contrib
```
现在看到的，就是实际将要引入的新代码。

### 5. 代码集成  

一旦特性分支准备停当，接下来的问题就是如何集成到更靠近主线的分支中。此外还要考虑维护项目的总体步骤是什么。  

**合并流程**  
一般最简单的情形，是在 `master` 分支中维护稳定代码，然后在特性分支上开发新功能，或是审核测试别人贡献的代码，接着将它并入主干，最后删除这个特性分支，如此反复。  
这是最简单的流程，所以在处理大一些的项目时可能会有问题。  

对于大型项目，至少需要维护两个长期分支 `master` 和 `develop`。新代码（`ruby_client`）将首先并入 `develop` 分支（`C8`），经过一个阶段，确认 `develop` 中的代码已稳定到可发行时，再将 `master` 分支快进到稳定点（`C8`）。而平时这两个分支都会被推送到公开的代码库。  

特性分支合并前  
![特性分支合并前](./img/特性分支合并前.png)  
特性分支合并后  
![特性分支合并后](./img/特性分支合并后.png)  
特性分支发布后   
![特性分支发布后](./img/特性分支发布后.png)  

这样，在人们克隆仓库时就有两种选择：既可检出最新稳定版本，确保正常使用；也能检出开发版本，试用最前沿的新特性。 你也可以扩展这个概念，先将所有新代码合并到临时特性分支，等到该分支稳定下来并通过测试后，再并入 `develop` 分支。然后，让时间检验一切，如果这些代码确实可以正常工作相当长一段时间，那就有理由相信它已经足够稳定，可以放心并入主干分支发布。  

**大项目的合并流程**  
Git 项目本身有四个长期分支：用于发布的 `master` 分支、用于合并基本稳定特性的 `next` 分支、用于合并仍需改进特性的 `pu` 分支（`pu` 是 `proposed updates` 的缩写），以及用于除错维护的 `maint` 分支（`maint` 取自 `maintenance`）。维护者可以按照之前介绍的方法，将贡献者的代码引入为不同的特性分支，然后测试评估，看哪些特性能稳定工作，哪些还需改进。稳定的特性可以并入 `next` 分支，然后再推送到公共仓库，以供其他人试用。  

管理复杂的并行贡献  
![管理复杂的并行贡献](./img/管理复杂的并行贡献.png)  

仍需改进的特性可以先并入 `pu` 分支。直到它们完全稳定后再并入 `master`。同时一并检查下 `next` 分支，将足够稳定的特性也并入 `master`。所以一般来说，`master` 始终是在快进，`next` 偶尔做下衍合，而 `pu` 则是频繁衍合，  

将特性并入长期分支  
![将特性并入长期分支](./img/将特性并入长期分支.png)  

并入 `master` 后的特性分支，已经无需保留分支索引，放心删除好了。Git 项目还有一个 `maint` 分支，它是以最近一次发行版为基础分化而来的，用于维护除错补丁。所以克隆 Git 项目仓库后会得到这四个分支，通过检出不同分支可以了解各自进展，或是试用前沿特性，或是贡献代码。而维护者则通过管理这些分支，逐步有序地并入第三方贡献。  

**衍合与挑拣（cherry-pick）的流程**  
一些维护者更喜欢衍合或者挑拣贡献者的代码，而不是简单的合并，因为这样能够保持线性的提交历史。如果你完成了一个特性的开发，并决定将它引入到主干代码中，你可以转到那个特性分支然后执行衍合命令，好在你的主干分支上（也可能是 `develop` 分支之类的）重新提交这些修改。如果这些代码工作得很好，你就可以快进 `master` 分支，得到一个线性的提交历史。  

另一个引入代码的方法是挑拣。挑拣类似于针对某次特定提交的衍合。它首先提取某次提交的补丁，然后试着应用在当前分支上。如果某个特性分支上有多个 commits，但你只想引入其中之一就可以使用这种方法。也可能仅仅是因为你喜欢用挑拣，讨厌衍合。  

挑拣（cherry-pick）之前的历史  
![挑拣（cherry-pick）之前的历史](./img/挑拣（cherry-pick）之前的历史.png)  

如果你希望拉取 `e43a6` 到你的主干分支，可以这样：
```shell
$ git cherry-pick e43a6fd3e94888d76779ad79fb568ed180e5fcdf
Finished one cherry-pick.
[master]: created a0a41a9: "More friendly message when locking the index fails."
 3 files changed, 17 insertions(+), 3 deletions(-)
```
这将会引入 `e43a6` 的代码，但是会得到不同的SHA-1值，因为应用日期不同。  

挑拣（cherry-pick）之后的历史  
![挑拣（cherry-pick）之后的历史](./img/挑拣（cherry-pick）之后的历史.png)  

现在，你可以删除这个特性分支并丢弃你不想引入的那些 commit。  

### 6. 给发行版签名   
你可以删除上次发布的版本并重新打标签，也可以建立一个新的标签。如果你决定以维护者的身份给发行版签名，应该这样做：  
```shell
$ git tag -s v1.5 -m 'my signed 1.5 tag'
You need a passphrase to unlock the secret key for
user: "Scott Chacon <schacon@gmail.com>"
1024-bit DSA key, ID F721C45A, created 2009-02-09
```
完成签名之后，如何分发PGP公钥（`public key`）是个问题。（译者注：分发公钥是为了验证标签）。还好，Git 的设计者想到了解决办法：可以把 `key`（即公钥）作为 `blob` 变量写入 Git 库，然后把它的内容直接写在标签里。`gpg --list-keys` 命令可以显示出你所拥有的 `key` ：  
```shell
$ gpg --list-keys
/Users/schacon/.gnupg/pubring.gpg
---------------------------------
pub   1024D/F721C45A 2009-02-09 [expires: 2010-02-09]
uid                  Scott Chacon <schacon@gmail.com>
sub   2048g/45D02282 2009-02-09 [expires: 2010-02-09]
```
然后，导出 `key` 的内容并经由管道符传递给 `git hash-object` ，之后钥匙会以 `blob` 类型写入 Git 中，最后返回这个 `blob` 量的 SHA-1 值：  
```shell
$ gpg -a --export F721C45A | git hash-object -w --stdin
659ef797d181633c87ec71ac3f9ba29fe5775b92
```
现在你的 Git 已经包含了这个 `key` 的内容了，可以通过不同的 SHA-1 值指定不同的 `key` 来创建标签。  
```shell
$ git tag -a maintainer-pgp-pub 659ef797d181633c87ec71ac3f9ba29fe5775b92
```
在运行 `git push --tags` 命令之后， `maintainer-pgp-pub` 标签就会公布给所有人。如果有人想要校验标签，他可以使用如下命令导入你的 `key`：  
```shell
$ git show maintainer-pgp-pub | gpg --import
```
人们可以用这个 `key` 校验你签名的所有标签。另外，你也可以在标签信息里写入一个操作向导，用户只需要运行 `git show <tag>` 查看标签信息，然后按照你的向导就能完成校验。  

### 7. 生成内部版本号  

因为 Git 不会为每次提交自动附加类似 'v123' 的递增序列，所以如果你想要得到一个便于理解的提交号可以运行 `git describe` 命令。Git 将会返回一个字符串，由三部分组成：最近一次标定的版本号，加上自那次标定之后的提交次数，再加上一段所描述的提交的 SHA-1 值：  
```shell
$ git describe master
v1.6.2-rc1-20-g8c5b85c
```
这个字符串可以作为快照的名字，方便人们理解。如果你的 Git 是你自己下载源码然后编译安装的，你会发现 `git --version` 命令的输出和这个字符串差不多。如果在一个刚刚打完标签的提交上运行 `describe` 命令，只会得到这次标定的版本号，而没有后面两项信息。

`git describe` 命令只适用于有标注的标签（通过-a或者-s选项创建的标签），所以发行版的标签都应该是带有标注的，以保证 `git describe` 能够正确的执行。你也可以把这个字符串作为 `checkout` 或者 `show` 命令的目标，因为他们最终都依赖于一个简短的 SHA-1 值，当然如果这个 SHA-1 值失效他们也跟着失效。  

### 8. 准备发布  

现在可以发布一个新的版本了。首先要将代码的压缩包归档，方便那些可怜的还没有使用 Git 的人们。可以使用 `git archive`：  
```shell
$ git archive master --prefix='project/' | gzip > `git describe master`.tar.gz
$ ls *.tar.gz
v1.6.2-rc1-20-g8c5b85c.tar.gz
```
这个压缩包解压出来的是一个文件夹，里面是你项目的最新代码快照。你也可以用类似的方法建立一个 zip 压缩包，在 `git archive加上--format=zip` 选项：
```shell
$ git archive master --prefix='project/' --format=zip > `git describe master`.zip
```
现在你有了一个tar.gz压缩包和一个zip压缩包，可以把他们上传到你网站上或者用e-mail发给别人。  

### 9. 制作简报  

是时候通知邮件列表里的朋友们来检验你的成果了。使用 `git shortlog` 命令可以方便快捷的制作一份修改日志（`changelog`），告诉大家上次发布之后又增加了哪些特性和修复了哪些bug。实际上这个命令能够统计给定范围内的所有提交;假如你上一次发布的版本是 v1.0.1，下面的命令将给出自从上次发布之后的所有提交的简介：
```shell
$ git shortlog --no-merges master --not v1.0.1
Chris Wanstrath (8):
      Add support for annotated tags to Grit::Tag
      Add packed-refs annotated tag support.
      Add Grit::Commit#to_patch
      Update version and History.txt
      Remove stray `puts`
      Make ls_tree ignore nils

Tom Preston-Werner (4):
      fix dates in history
      dynamic version method
      Version bump to 1.0.2
      Regenerated gemspec for version 1.0.2
```
这就是自从 v1.0.1 版本以来的所有提交的简介，内容按照作者分组，以便你能快速的发 e-mail 给他们。  

# Git 工具  

## 1. 修订版本（Revision）选择  

Git 允许你通过几种方法来指明特定的或者一定范围内的提交。  

### 1. 单个修订版本  

显然你可以使用给出的 SHA-1 值来指明一次提交，不过也有更加人性化的方法来做同样的事。本节概述了指明单个提交的诸多方法。  

**简短的SHA**  
Git 很聪明，它能够通过你提供的前几个字符来识别你想要的那次提交，只要你提供的那部分 SHA-1 不短于四个字符，并且没有歧义——也就是说，当前仓库中只有一个对象以这段 SHA-1 开头。  
想要查看一次指定的提交，假设你运行 `git log` 命令并找到你增加了功能的那次提交：  
```shell
$ git log
commit 734713bc047d87bf7eac9674765ae793478c50d3
Author: Scott Chacon <schacon@gmail.com>
Date:   Fri Jan 2 18:32:33 2009 -0800

    fixed refs handling, added gc auto, updated tests

commit d921970aadf03b3cf0e71becdaab3147ba71cdef
Merge: 1c002dd... 35cfb2b...
Author: Scott Chacon <schacon@gmail.com>
Date:   Thu Dec 11 15:08:43 2008 -0800

    Merge commit 'phedders/rdocs'

commit 1c002dd4b536e7479fe34593e72e6c6c1819e53b
Author: Scott Chacon <schacon@gmail.com>
Date:   Thu Dec 11 14:58:32 2008 -0800

    added some blame and merge stuff
```
假设是 1c002dd.... 。如果你想 `git show `这次提交，下面的命令是等价的（假设简短的版本没有歧义）：  
```shell
$ git show 1c002dd4b536e7479fe34593e72e6c6c1819e53b
$ git show 1c002dd4b536e7479f
$ git show 1c002d
```
Git 可以为你的 SHA-1 值生成出简短且唯一的缩写。如果你传递 `--abbrev-commit` 给 `git log` 命令，输出结果里就会使用简短且唯一的值；它默认使用七个字符来表示，不过必要时为了避免 SHA-1 的歧义，会增加字符数：  
```shell
$ git log --abbrev-commit --pretty=oneline
ca82a6d changed the version number
085bb3b removed unnecessary test code
a11bef0 first commit
```
通常在一个项目中，使用八到十个字符来避免 SHA-1 歧义已经足够了。  

**关于 SHA-1 的简短说明**  
许多人可能会担心一个问题：在随机的偶然情况下，在他们的仓库里会出现两个具有相同 SHA-1 值的对象。那会怎么样呢？  
如果你真的向仓库里提交了一个跟之前的某个对象具有相同 SHA-1 值的对象，Git 将会发现之前的那个对象已经存在在 Git 数据库中，并认为它已经被写入了。如果什么时候你想再次检出那个对象时，你会总是得到先前的那个对象的数据。  
不过，你应该了解到，这种情况发生的概率是多么微小。SHA-1 摘要长度是 20 字节，也就是 160 位。为了保证有 50% 的概率出现一次冲突，需要 2^80 个随机哈希的对象（计算冲突机率的公式是 `p = (n(n-1)/2) * (1/2^160))`。2^80 是 1.2 x 10^24，也就是一亿亿亿，那是地球上沙粒总数的 1200 倍  

### 2. 分支引用

指明一次提交的最直接的方法要求有一个指向它的分支引用。这样，你就可以在任何需要一个提交对象或者 SHA-1 值的 Git 命令中使用该分支名称了。如果你想要显示一个分支的最后一次提交的对象，例如假设 `topic1` 分支指向 ca82a6d，那么下面的命令是等价的：  
```shell
$ git show ca82a6dff817ec66f44342007202690a93763949
$ git show topic1
```
如果你想知道某个分支指向哪个特定的 SHA，或者想看任何一个例子中被简写的 SHA-1，你可以使用一个叫做 `rev-parse` 的 Git 探测工具，简单来说，`rev-parse` 是为了底层操作而不是日常操作设计的。有时你想看 Git 现在到底处于什么状态时，它可能会很有用。这里你可以对你的分支运执行  `rev-parse`。  
```shell
$ git rev-parse topic1
ca82a6dff817ec66f44342007202690a93763949
```

**引用日志里的简称**  
在你工作的同时，Git 在后台的工作之一就是保存一份引用日志——一份记录最近几个月你的 HEAD 和分支引用的日志。  
你可以使用 `git reflog` 来查看引用日志：  
```shell
$ git reflog
734713b HEAD@{0}: commit: fixed refs handling, added gc auto, updated
d921970 HEAD@{1}: merge phedders/rdocs: Merge made by recursive.
1c002dd HEAD@{2}: commit: added some blame and merge stuff
1c36188 HEAD@{3}: rebase -i (squash): updating HEAD
95df984 HEAD@{4}: commit: # This is a combination of two commits.
1c36188 HEAD@{5}: rebase -i (squash): updating HEAD
7e05da5 HEAD@{6}: rebase -i (pick): updating HEAD
```
每次你的分支顶端因为某些原因被修改时，Git 就会为你将信息保存在这个临时历史记录里面。你也可以使用这份数据来指明更早的分支。如果你想查看仓库中 HEAD 在五次前的值，你可以使用引用日志的输出中的 `@{n}` 引用：  
```shell
$ git show HEAD@{5}
```
你也可以使用这个语法来查看某个分支在一定时间前的位置。例如，想看你的 `master` 分支昨天在哪，你可以输入  
```shell
$ git show master@{yesterday}
```
它就会显示昨天分支的顶端在哪。这项技术只对还在你引用日志里的数据有用，所以不能用来查看比几个月前还早的提交。  

想要看类似于 git log 输出格式的引用日志信息，你可以运行 git log -g：  
```shell
$ git log -g master
commit 734713bc047d87bf7eac9674765ae793478c50d3
Reflog: master@{0} (Scott Chacon <schacon@gmail.com>)
Reflog message: commit: fixed refs handling, added gc auto, updated
Author: Scott Chacon <schacon@gmail.com>
Date:   Fri Jan 2 18:32:33 2009 -0800

    fixed refs handling, added gc auto, updated tests

commit d921970aadf03b3cf0e71becdaab3147ba71cdef
Reflog: master@{1} (Scott Chacon <schacon@gmail.com>)
Reflog message: merge phedders/rdocs: Merge made by recursive.
Author: Scott Chacon <schacon@gmail.com>
Date:   Thu Dec 11 15:08:43 2008 -0800

    Merge commit 'phedders/rdocs'
```
需要注意的是，引用日志信息只存在于本地——这是一个记录你在你自己的仓库里做过什么的日志。其他人拷贝的仓库里的引用日志不会和你的相同；而你新克隆一个仓库的时候，引用日志是空的，因为你在仓库里还没有操作。`git show HEAD@{2.months.ago}` 这条命令只有在你克隆了一个项目至少两个月时才会有用——如果你是五分钟前克隆的仓库，那么它将不会有结果返回。  

**祖先引用**
另一种指明某次提交的常用方法是通过它的祖先。如果你在引用最后加上一个 `^`，Git 将其理解为此次提交的父提交。 假设你的工程历史是这样的：  
```shell
$ git log --pretty=format:'%h %s' --graph
* 734713b fixed refs handling, added gc auto, updated tests
*   d921970 Merge commit 'phedders/rdocs'
|\
| * 35cfb2b Some rdoc changes
* | 1c002dd added some blame and merge stuff
|/
* 1c36188 ignore *.gem
* 9b29157 add open3_detach to gemspec file list
```
那么，想看上一次提交，你可以使用 `HEAD^`，意思是“HEAD 的父提交”：
```shell
$ git show HEAD^
commit d921970aadf03b3cf0e71becdaab3147ba71cdef
Merge: 1c002dd... 35cfb2b...
Author: Scott Chacon <schacon@gmail.com>
Date:   Thu Dec 11 15:08:43 2008 -0800

    Merge commit 'phedders/rdocs'
```
你也可以在 `^` 后添加一个数字——例如，`d921970^2` 意思是 `d921970` 的第二父提交”。这种语法只在合并提交时有用，因为合并提交可能有多个父提交。第一父提交是你合并时所在分支，而第二父提交是你所合并的分支：  
```shell
$ git show d921970^
commit 1c002dd4b536e7479fe34593e72e6c6c1819e53b
Author: Scott Chacon <schacon@gmail.com>
Date:   Thu Dec 11 14:58:32 2008 -0800

    added some blame and merge stuff

$ git show d921970^2
commit 35cfb2b795a55793d7cc56a6cc2060b4bb732548
Author: Paul Hedderly <paul+git@mjr.org>
Date:   Wed Dec 10 22:22:03 2008 +0000

    Some rdoc changes
```
另外一个指明祖先提交的方法是 `~`。这也是指向第一父提交，所以 `HEAD~` 和 `HEAD^` 是等价的。当你指定数字的时候就明显不一样了。`HEAD~2` 是指“第一父提交的第一父提交”，也就是“祖父提交”——它会根据你指定的次数检索第一父提交。例如，在上面列出的历史记录里面，`HEAD~3` 会是  
```shell
$ git show HEAD~3
commit 1c3618887afb5fbcbea25b7c013f4e2114448b8d
Author: Tom Preston-Werner <tom@mojombo.com>
Date:   Fri Nov 7 13:47:59 2008 -0500

    ignore *.gem
```
也可以写成 `HEAD^^^`，同样是第一父提交的第一父提交的第一父提交：  
```shell
$ git show HEAD^^^
commit 1c3618887afb5fbcbea25b7c013f4e2114448b8d
Author: Tom Preston-Werner <tom@mojombo.com>
Date:   Fri Nov 7 13:47:59 2008 -0500

    ignore *.gem
```
你也可以混合使用这些语法——你可以通过 `HEAD~3^2` 指明先前引用的第二父提交（假设它是一个合并提交）。

### 3. 提交范围  

现在你已经可以指明单次的提交，让我们来看看怎样指明一定范围的提交。这在你管理分支的时候尤显重要——如果你有很多分支，你可以指明范围来圈定一些问题的答案。  

1. 双点  

最常用的指明范围的方法是双点的语法。这种语法主要是让 Git 区分出可从一个分支中获得而不能从另一个分支中获得的提交。  

范围选择的提交历史实例  
![范围选择的提交历史实例](./img/范围选择的提交历史实例.png)  

你想要查看你的试验分支上哪些没有被提交到主分支，那么你就可以使用 `master..experiment` 来让 Git 显示这些提交的日志——这句话的意思是“所有可从 `experiment` 分支中获得而不能从 `master` 分支中获得的提交”。为了使例子简单明了，我使用了图标中提交对象的字母来代替真实日志的输出，  
```shell
$ git log master..experiment
D
C
```
另一方面，如果你想看相反的——所有在 `master` 而不在 `experiment` 中的分支——你可以交换分支的名字。`experiment..master` 显示所有可在 `master` 获得而在 `experiment` 中不能的提交：  
```shell
$ git log experiment..master
F
E
```
这在你想保持 `experiment` 分支最新和预览你将合并的提交的时候特别有用。  
这个语法的另一种常见用途是查看你将把什么推送到远程：  
```shell
$ git log origin/master..HEAD
```
这条命令显示任何在你当前分支上而不在远程 `origin` 上的提交。如果你运行 `git push` 并且的你的当前分支正在跟踪 `origin/master`，被 `git log origin/master..HEAD` 列出的提交就是将被传输到服务器上的提交。 你也可以留空语法中的一边来让 Git 来假定它是 HEAD。例如，输入 `git log origin/master..` 将得到和上面的例子一样的结果—— Git 使用 `HEAD` 来代替不存在的一边。  

2. 多点  

双点语法就像速记一样有用；但是你也许会想针对两个以上的分支来指明修订版本，比如查看哪些提交被包含在某些分支中的一个，但是不在你当前的分支上。Git 允许你在引用前使用 `^` 字符或者 `--not` 指明你不希望提交被包含其中的分支。因此下面三个命令是等同的：  
```shell
$ git log refA..refB
$ git log ^refA refB
$ git log refB --not refA
```
它允许你在查询中指定多于两个的引用，而这是双点语法所做不到的。例如，如果你想查找所有从 `refA` 或` refB` 包含的但是不被 `refC` 包含的提交，你可以输入下面中的一个  
```shell
$ git log refA refB ^refC
$ git log refA refB --not refC
```
3. 三点  

最后一种主要的范围选择语法是三点语法，这个可以指定被两个引用中的一个包含但又不被两者同时包含的分支。  
如果你想查看master或者experiment中包含的但不是两者共有的引用，你可以运行  
```shell
$ git log master...experiment
F
E
D
C
```
这个再次给出你普通的log输出但是只显示那四次提交的信息，按照传统的提交日期排列。  
这种情形下，log命令的一个常用参数是--left-right，它会显示每个提交到底处于哪一侧的分支。这使得数据更加有用。  
```shell
$ git log --left-right master...experiment
< F
< E
> D
> C
```
有了以上工具，让Git知道你要察看哪些提交就容易得多了。  

## 2. 交互式暂存

Git 提供了很多脚本来辅助某些命令行任务。这里，你将看到一些交互式命令，它们帮助你方便地构建只包含特定组合和部分文件的提交。在你修改了一大批文件然后决定将这些变更分布在几个各有侧重的提交而不是单个又大又乱的提交时，这些工具非常有用。用这种方法，你可以确保你的提交在逻辑上划分为相应的变更集，以便于供和你一起工作的开发者审阅。如果你运行 `git add` 时加上 `-i` 或者 `--interactive` 选项，Git 就进入了一个交互式的 shell 模式，显示一些类似于下面的信息：  
```shell
$ git add -i
           staged     unstaged path
  1:    unchanged        +0/-1 TODO
  2:    unchanged        +1/-1 index.html
  3:    unchanged        +5/-1 lib/simplegit.rb

*** Commands ***
  1: status     2: update      3: revert     4: add untracked
  5: patch      6: diff        7: quit       8: help
What now>
```
你会看到这个命令以一个完全不同的视图显示了你的暂存区——主要是你通过 `git status` 得到的那些信息但是稍微简洁但信息更加丰富一些。它在左侧列出了你暂存的变更，在右侧列出了未被暂存的变更。  

在这之后是一个命令区。这里你可以做很多事情，包括暂存文件，撤回文件，暂存部分文件，加入未被追踪的文件，查看暂存文件的差别。  

### 1. 暂存和撤回文件  

如果你在 `What now>` 的提示后输入 `2` 或者 `u` ，这个脚本会提示你那些文件你想要暂存：  
```shell
What now> 2
           staged     unstaged path
  1:    unchanged        +0/-1 TODO
  2:    unchanged        +1/-1 index.html
  3:    unchanged        +5/-1 lib/simplegit.rb
Update>>
```
如果想暂存 TODO 和 index.html ，你可以输入相应的编号：  
```shell
Update>> 1,2
           staged     unstaged path
* 1:    unchanged        +0/-1 TODO
* 2:    unchanged        +1/-1 index.html
  3:    unchanged        +5/-1 lib/simplegit.rb
Update>>
```
每个文件旁边的 `*` 表示选中的文件将被暂存。如果你在 `update>>` 提示后直接敲入回车，Git 会替你把所有选中的内容暂存：  
```shell
Update>>
updated 2 paths

*** Commands ***
  1: status     2: update      3: revert     4: add untracked
  5: patch      6: diff        7: quit       8: help
What now> 1
           staged     unstaged path
  1:        +0/-1      nothing TODO
  2:        +1/-1      nothing index.html
  3:    unchanged        +5/-1 lib/simplegit.rb
```
现在你可以看到 TODO 和 index.html 文件被暂存了同时simplegit.rb 文件仍然未被暂存。如果这时你想要撤回 TODO 文件，就使用3或者 `r`（代表`revert`，恢复）选项：  
```shell
*** Commands ***
  1: status     2: update      3: revert     4: add untracked
  5: patch      6: diff        7: quit       8: help
What now> 3
           staged     unstaged path
  1:        +0/-1      nothing TODO
  2:        +1/-1      nothing index.html
  3:    unchanged        +5/-1 lib/simplegit.rb
Revert>> 1
           staged     unstaged path
* 1:        +0/-1      nothing TODO
  2:        +1/-1      nothing index.html
  3:    unchanged        +5/-1 lib/simplegit.rb
Revert>> [enter]
reverted one path
```
再次查看 Git 的状态，你会看到你已经撤回了 TODO 文件  

要查看你暂存内容的差异，你可以使用6或者d（表示 `diff`）命令。它会显示你暂存文件的列表，你可以选择其中的几个，显示其被暂存的差异。这跟你在命令行下指定 `git diff --cached` 非常相似：
```shell
*** Commands ***
  1: status     2: update      3: revert     4: add untracked
  5: patch      6: diff        7: quit       8: help
What now> 6
           staged     unstaged path
  1:        +1/-1      nothing index.html
Review diff>> 1
diff --git a/index.html b/index.html
index 4d07108..4335f49 100644
--- a/index.html
+++ b/index.html
@@ -16,7 +16,7 @@ Date Finder

 <p id="out">...</p>

-<div id="footer">contact : support@github.com</div>
+<div id="footer">contact : email.support@github.com</div>

 <script type="text/javascript">
```

### 2. 暂存补丁  

只让 Git 暂存文件的某些部分而忽略其他也是有可能的。例如，你对 simplegit.rb 文件作了两处修改但是只想暂存其中一个而忽略另一个，在 Git 中实现这一点非常容易。在交互式的提示符下，输入 `5` 或者 `p` （表示 `patch`，补丁）。Git 会询问哪些文件你希望部分暂存；然后对于被选中文件的每一节，他会逐个显示文件的差异区块并询问你是否希望暂存他们：  
```shell
diff --git a/lib/simplegit.rb b/lib/simplegit.rb
index dd5ecc4..57399e0 100644
--- a/lib/simplegit.rb
+++ b/lib/simplegit.rb
@@ -22,7 +22,7 @@ class SimpleGit
   end

   def log(treeish = 'master')
-    command("git log -n 25 #{treeish}")
+    command("git log -n 30 #{treeish}")
   end

   def blame(path)
Stage this hunk [y,n,a,d,/,j,J,g,e,?]?
```
此处你有很多选择。输入 `?` 可以显示列表：  
```shell
Stage this hunk [y,n,a,d,/,j,J,g,e,?]? ?
y - stage this hunk
n - do not stage this hunk
a - stage this and all the remaining hunks in the file
d - do not stage this hunk nor any of the remaining hunks in the file
g - select a hunk to go to
/ - search for a hunk matching the given regex
j - leave this hunk undecided, see next undecided hunk
J - leave this hunk undecided, see next hunk
k - leave this hunk undecided, see previous undecided hunk
K - leave this hunk undecided, see previous hunk
s - split the current hunk into smaller hunks
e - manually edit the current hunk
? - print help
```
如果你想暂存各个区块，通常你会输入 `y` 或者 `n` ，但是暂存特定文件里的全部区块或者暂时跳过对一个区块的处理同样也很有用。如果你暂存了文件的一个部分而保留另外一个部分不被暂存，你的状态输出看起来会是这样：  
```shell
What now> 1
           staged     unstaged path
  1:    unchanged        +0/-1 TODO
  2:        +1/-1      nothing index.html
  3:        +1/-1        +4/-0 lib/simplegit.rb
```
simplegit.rb 的状态非常有意思。它显示有几行被暂存了，有几行没有。你部分地暂存了这个文件。在这时，你可以退出交互式脚本然后运行git commit来提交部分暂存的文件。  

你也可以不通过交互式增加的模式来实现部分文件暂存——你可以在命令行下通过 `git add -p` 或者 `git add --patch` 来启动同样的脚本。  

## 3. 储藏（Stashing）  

当你正在进行项目中某一部分的工作，里面的东西处于一个比较杂乱的状态，而你想转到其他分支上进行一些工作。问题是，你不想提交进行了一半的工作，否则以后你无法回到这个工作点。解决这个问题的办法就是 `git stash` 命令。  
**储藏** 可以获取你工作目录的中间状态——也就是你修改过的被追踪的文件和暂存的变更——并将它保存到一个未完结变更的堆栈中，随时可以重新应用。  

### 1. 储藏你的工作  

你运行 `git status`，你可以看到你的中间状态：  
```shell
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#      modified:   index.html
#
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#
#      modified:   lib/simplegit.rb
#
```
现在你想切换分支，但是你还不想提交你正在进行中的工作；所以你储藏这些变更。为了往堆栈推送一个新的储藏，只要运行 `git stash`：  
```shell
$ git stash
Saved working directory and index state \
  "WIP on master: 049d078 added the index file"
HEAD is now at 049d078 added the index file
(To restore them type "git stash apply")
```
你的工作目录就干净了：  
```shell
$ git status
# On branch master
nothing to commit, working directory clean
```
这时，你可以方便地切换到其他分支工作；你的变更都保存在栈上。要查看现有的储藏，你可以使用 `git stash list`：  
```shell
$ git stash list
stash@{0}: WIP on master: 049d078 added the index file
stash@{1}: WIP on master: c264051 Revert "added file_size"
stash@{2}: WIP on master: 21d80a5 added number to log
```
在这个案例中，之前已经进行了两次储藏，所以你可以访问到三个不同的储藏。你可以重新应用你刚刚实施的储藏，所采用的命令就是之前在原始的 `stash` 命令的帮助输出里提示的：`git stash apply`。如果你想应用更早的储藏，你可以通过名字指定它，像这样：`git stash apply stash@{2}`。如果你不指明，Git 默认使用最近的储藏并尝试应用它：  
```shell
$ git stash apply
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#
#      modified:   index.html
#      modified:   lib/simplegit.rb
#
```
你可以看到 Git 重新修改了你所储藏的那些当时尚未提交的文件。在这个案例里，你尝试应用储藏的工作目录是干净的，并且属于同一分支；但是一个干净的工作目录和应用到相同的分支上并不是应用储藏的必要条件。你可以在其中一个分支上保留一份储藏，随后切换到另外一个分支，再重新应用这些变更。在工作目录里包含已修改和未提交的文件时，你也可以应用储藏——Git 会给出归并冲突如果有任何变更无法干净地被应用。  
对文件的变更被重新应用，但是被暂存的文件没有重新被暂存。想那样的话，你必须在运行 `git stash apply` 命令时带上一个 `--index` 的选项来告诉命令重新应用被暂存的变更。如果你是这么做的，你应该已经回到你原来的位置：  
```shell
$ git stash apply --index
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#      modified:   index.html
#
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#
#      modified:   lib/simplegit.rb
#
```
apply 选项只尝试应用储藏的工作——储藏的内容仍然在栈上。要移除它，你可以运行 git stash drop，加上你希望移除的储藏的名字：  
```shell
$ git stash list
stash@{0}: WIP on master: 049d078 added the index file
stash@{1}: WIP on master: c264051 Revert "added file_size"
stash@{2}: WIP on master: 21d80a5 added number to log
$ git stash drop stash@{0}
Dropped stash@{0} (364e91f3f268f0900bc3ee613f9f733e82aaed43)
```
你也可以运行 `git stash pop` 来重新应用储藏，同时立刻将其从堆栈中移走。  

### 2. 取消储藏(Un-applying a Stash)  

在某些情况下，你可能想应用储藏的修改，在进行了一些其他的修改后，又要取消之前所应用储藏的修改。Git没有提供类似于 stash unapply 的命令，但是可以通过取消该储藏的补丁达到同样的效果：  
```shell
$ git stash show -p stash@{0} | git apply -R
```
同样的，如果你沒有指定具体的某个储藏，Git 会选择最近的储藏：  
```shell
$ git stash show -p | git apply -R
```
你可能会想要新建一个別名，在你的 Git 里增加一个 `stash-unapply` 命令，这样更有效率。例如：  
```shell
$ git config --global alias.stash-unapply '!git stash show -p | git apply -R'
$ git stash apply
$ #... work work work
$ git stash-unapply
```

### 3. 从储藏中创建分支  

如果你储藏了一些工作，暂时不去理会，然后继续在你储藏工作的分支上工作，你在重新应用工作时可能会碰到一些问题。如果尝试应用的变更是针对一个你那之后修改过的文件，你会碰到一个归并冲突并且必须去化解它。如果你想用更方便的方法来重新检验你储藏的变更，你可以运行 `git stash branch`，这会创建一个新的分支，检出你储藏工作时的所处的提交，重新应用你的工作，如果成功，将会丢弃储藏。
```shell
$ git stash branch testchanges
Switched to a new branch "testchanges"
# On branch testchanges
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#      modified:   index.html
#
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#
#      modified:   lib/simplegit.rb
#
Dropped refs/stash@{0} (f0dfc4d5dc332d1cee34a634182e168c4efc3359)
```
这是一个很棒的捷径来恢复储藏的工作然后在新的分支上继续当时的工作。  

## 4. 重写历史  

Git 的一个卓越之处就是它允许你在最后可能的时刻再作决定。你可以在你即将提交暂存区时决定什么文件归入哪一次提交，你可以使用 `stash` 命令来决定你暂时搁置的工作，你可以重写已经发生的提交以使它们看起来是另外一种样子。这个包括改变提交的次序、改变说明或者修改提交中包含的文件，将提交归并、拆分或者完全删除——这一切在你尚未开始将你的工作和别人共享前都是可以的。  

### 1. 改变最近一次提交  

改变最近一次提交也许是最常见的重写历史的行为。对于你的最近一次提交，你经常想做两件基本事情：改变提交说明，或者改变你刚刚通过增加，改变，删除而记录的快照。  

如果你只想修改最近一次提交说明，这非常简单：  
```shell
$ git commit --amend
```
这会把你带入文本编辑器，里面包含了你最近一次提交说明，供你修改。当你保存并退出编辑器，这个编辑器会写入一个新的提交，里面包含了那个说明，并且让它成为你的新的最近一次提交。  

如果你完成提交后又想修改被提交的快照，增加或者修改其中的文件，你通过修改文件然后对其运行 `git add` 或对一个已被记录的文件运行 `git rm` ，随后的 `git commit --amend` 会获取你当前的暂存区并将它作为新提交对应的快照。  
使用这项技术的时候你必须小心，因为修正会改变提交的 SHA-1 值。这个很像是一次非常小的 rebase ——不要在你最近一次提交被推送后还去修正它。  

### 2. 修改多个提交说明  

要修改历史中更早的提交，必须采用更复杂的工具。Git 没有一个修改历史的工具，但是你可以使用 `rebase` 工具来衍合一系列的提交到它们原来所在的 HEAD 上而不是移到新的上。依靠这个交互式的 `rebase` 工具，你就可以停留在每一次提交后，如果你想修改或改变说明、增加文件或任何其他事情。你可以通过给git `rebase` 增加 `-i` 选项来以交互方式地运行 `rebase` 。你必须通过告诉命令衍合到哪次提交，来指明你需要重写的提交的回溯深度。  
例如，你想修改最近三次的提交说明，或者其中任意一次，你必须给 `git rebase -i` 提供一个参数，指明你想要修改的提交的父提交，例如 `HEAD~2` 或者 `HEAD~3` 。可能记住 `~3` 更加容易，因为你想修改最近三次提交；但是请记住你事实上所指的是四次提交之前，即你想修改的提交的父提交。  
```shell
$ git rebase -i HEAD~3
```
再次提醒这是一个衍合命令—— `HEAD~3..HEAD` 范围内的每一次提交都会被重写，无论你是否修改说明。不要涵盖你已经推送到中心服务器的提交——这么做会使其他开发者产生混乱，因为你提供了同样变更的不同版本。  
运行这个命令会为你的文本编辑器提供一个提交列表，看起来像下面这样  
```
pick f7f3f6d changed my name a bit
pick 310154e updated README formatting and added blame
pick a5f4a0d added cat-file

# Rebase 710f0f8..a5f4a0d onto 710f0f8
#
# Commands:
#  p, pick = use commit
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#
# If you remove a line here THAT COMMIT WILL BE LOST.
# However, if you remove everything, the rebase will be aborted.
#
```
很重要的一点是你得注意这些提交的顺序与你通常通过 `log` 命令看到的是相反的。如果你运行 `log` ，你会看到下面这样的结果：  
```shell
$ git log --pretty=format:"%h %s" HEAD~3..HEAD
a5f4a0d added cat-file
310154e updated README formatting and added blame
f7f3f6d changed my name a bit
```
请注意这里的倒序。  

你需要修改这个脚本来让它停留在你想修改的变更上。要做到这一点，你只要将你想修改的每一次提交前面的pick改为edit。例如，只想修改第三次提交说明的话，你就像下面这样修改文件：  
```
edit f7f3f6d changed my name a bit
pick 310154e updated README formatting and added blame
pick a5f4a0d added cat-file
```
当你保存并退出编辑器，Git会倒回至列表中的最后一次提交，然后把你送到命令行中，同时显示以下信息：  
```shell
$ git rebase -i HEAD~3
Stopped at 7482e0d... updated the gemspec to hopefully work better
You can amend the commit now, with

       git commit --amend

Once you’re satisfied with your changes, run

       git rebase --continue
```
输入 `$ git commit --amend` 修改提交说明，退出编辑器。然后，运行 `$ git rebase --continue` 这个命令会自动应用其他两次提交，你就完成任务了。  

### 3. 重排提交  

你也可以使用交互式的衍合来彻底重排或删除提交。如果你想删除"added cat-file"这个提交并且修改其他两次提交引入的顺序，你将 rebase 脚本从这个  
```
pick f7f3f6d changed my name a bit
pick 310154e updated README formatting and added blame
pick a5f4a0d added cat-file
```
改为这个：  
```
pick 310154e updated README formatting and added blame
pick f7f3f6d changed my name a bit
```
当你保存并退出编辑器，Git 将分支倒回至这些提交的父提交，应用 `310154e` ，然后 `f7f3f6d` ，接着停止。你有效地修改了这些提交的顺序并且彻底删除了 "added cat-file" 这次提交。  

### 4. 压制(Squashing)提交  

交互式的衍合工具还可以将一系列提交压制为单一提交。脚本在 rebase 的信息里放了一些有用的指示：  
```
#
# Commands:
#  p, pick = use commit
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#
# If you remove a line here THAT COMMIT WILL BE LOST.
# However, if you remove everything, the rebase will be aborted.
#
```
如果不用 `pick` 或者 `edit` ，而是指定 `squash` ，Git 会同时应用那个变更和它之前的变更并将提交说明归并。因此，如果你想将这三个提交合并为单一提交，你可以将脚本修改成这样：  
```
pick f7f3f6d changed my name a bit
squash 310154e updated README formatting and added blame
squash a5f4a0d added cat-file
```
当你保存并退出编辑器，Git 会应用全部三次变更然后将你送回编辑器来归并三次提交说明。  
```
# This is a combination of 3 commits.
# The first commit's message is:
changed my name a bit

# This is the 2nd commit message:

updated README formatting and added blame

# This is the 3rd commit message:

added cat-file
```
当你保存之后，你就拥有了一个包含前三次提交的全部变更的单一提交。  

### 5. 拆分提交  

拆分提交就是撤销一次提交，然后多次部分地暂存或提交直到结束。  
例如，假设你想将三次提交中的中间一次拆分成两次提交，你可以在rebase -i脚本中修改你想拆分的提交前的指令为 `edit` ：  
```
pick f7f3f6d changed my name a bit
edit 310154e updated README formatting and added blame
pick a5f4a0d added cat-file
```
然后，这个脚本就将你带入命令行，你重置那次提交，提取被重置的变更，从中创建多次提交。当你保存并退出编辑器，Git 倒回到列表中第一次提交的父提交，然后将你带到控制台。那里你可以用 `git reset HEAD^` 对那次提交进行一次混合的重置，这将撤销那次提交并且将修改的文件撤回。此时你可以暂存并提交文件，直到你拥有多次提交，结束后，运行 `git rebase --continue` 。  
```shell
$ git reset HEAD^
$ git add README
$ git commit -m 'updated README formatting'
$ git add lib/simplegit.rb
$ git commit -m 'added blame'
$ git rebase --continue
```
Git 在脚本中应用了最后一次提交（`a5f4a0d`），你的历史看起来就像这样了：  
```shell
$ git log -4 --pretty=format:"%h %s"
1c002dd added cat-file
9b29157 added blame
35cfb2b updated README formatting
f3cc40e changed my name a bit
```
再次提醒，这会修改你列表中的提交的 SHA 值，所以请确保这个列表里不包含你已经推送到共享仓库的提交。

### 6. 核弹级选项: filter-branch  

如果你想用脚本的方式修改大量的提交，还有一个重写历史的选项可以用， 例如，全局性地修改电子邮件地址或者将一个文件从所有提交中删除。这个命令是 `filter-branch` ，这个会大面积地修改你的历史，所以你很有可能不该去用它，除非你的项目尚未公开，没有其他人在你准备修改的提交的基础上工作。尽管如此，这个可以非常有用。  

1. 从所有提交中删除一个文件  

也许你不小心提交了一个包含密码的文件，而你想让你的项目开源。`filter-branch` 大概会是你用来清理整个历史的工具。要从整个历史中删除一个名叫 `password.txt` 的文件，你可以在 `filter-branch` 上使用 `--tree-filter` 选项：
```shell
$ git filter-branch --tree-filter 'rm -f passwords.txt' HEAD
Rewrite 6b9b3cf04e7c5686a9cb838c3f36a8cb6a0fc2bd (21/21)
Ref 'refs/heads/master' was rewritten
```
`--tree-filter` 选项会在每次检出项目时先执行指定的命令然后重新提交结果。在这个例子中，你会在所有快照中删除一个名叫 `password.txt` 的文件，无论它是否存在。如果你想删除所有不小心提交上去的编辑器备份文件，你可以运行类似 `git filter-branch --tree-filter "find * -type f -name '*~' -delete" HEAD` 的命令。  
你可以观察到 Git 重写目录树并且提交，然后将分支指针移到末尾。一个比较好的办法是在一个测试分支上做这些然后在你确定产物真的是你所要的之后，再 `hard-reset` 你的主分支。要在你所有的分支上运行 `filter-branch` 的话，你可以传递一个 `--all` 给命令。  

2. 将一个子目录设置为新的根目录  

假设你完成了从另外一个代码控制系统的导入工作，得到了一些没有意义的子目录（trunk, tags等等）。如果你想让 trunk 子目录成为每一次提交的新的项目根目录， `filter-branch` 也可以帮你做到：  
```shell
$ git filter-branch --subdirectory-filter trunk HEAD
Rewrite 856f0bf61e41a27326cdae8f09fe708d679f596f (12/12)
Ref 'refs/heads/master' was rewritten
```
现在你的项目根目录就是trunk子目录了。Git 会自动地删除不对这个子目录产生影响的提交。  

3. 全局性地更换电子邮件地址  

你可以用 `filter-branch` 来更换多次提交里的电子邮件地址。你必须小心一些，只改变属于你的电子邮件地址，所以你使用 `--commit-filter` ：
```shell
$ git filter-branch --commit-filter '
        if [ "$GIT_AUTHOR_EMAIL" = "schacon@localhost" ];
        then
                GIT_AUTHOR_NAME="Scott Chacon";
                GIT_AUTHOR_EMAIL="schacon@example.com";
                git commit-tree "$@";
        else
                git commit-tree "$@";
        fi' HEAD
```
这个会遍历并重写所有提交使之拥有你的新地址。因为提交里包含了它们的父提交的SHA-1值，这个命令会修改你的历史中的所有提交，而不仅仅是包含了匹配的电子邮件地址的那些。  

## 5. 使用 Git 调试  

Git 同样提供了一些工具来帮助你调试项目中遇到的问题。  

### 1. 文件标注  

如果你在追踪代码中的缺陷想知道这是什么时候为什么被引进来的，文件标注会是你的最佳工具。它会显示文件中对每一行进行修改的最近一次提交。因此，如果你发现自己代码中的一个方法存在缺陷，你可以用git blame来标注文件，查看那个方法的每一行分别是由谁在哪一天修改的。  

下面这个例子使用了-L选项来限制输出范围在第12至22行：  
```shell
$ git blame -L 12,22 simplegit.rb
^4832fe2 (Scott Chacon  2008-03-15 10:31:28 -0700 12)  def show(tree = 'master')
^4832fe2 (Scott Chacon  2008-03-15 10:31:28 -0700 13)   command("git show #{tree}")
^4832fe2 (Scott Chacon  2008-03-15 10:31:28 -0700 14)  end
^4832fe2 (Scott Chacon  2008-03-15 10:31:28 -0700 15)
9f6560e4 (Scott Chacon  2008-03-17 21:52:20 -0700 16)  def log(tree = 'master')
79eaf55d (Scott Chacon  2008-04-06 10:15:08 -0700 17)   command("git log #{tree}")
9f6560e4 (Scott Chacon  2008-03-17 21:52:20 -0700 18)  end
9f6560e4 (Scott Chacon  2008-03-17 21:52:20 -0700 19)
42cf2861 (Magnus Chacon 2008-04-13 10:45:01 -0700 20)  def blame(path)
42cf2861 (Magnus Chacon 2008-04-13 10:45:01 -0700 21)   command("git blame #{path}")
42cf2861 (Magnus Chacon 2008-04-13 10:45:01 -0700 22)  end
```
请注意第一个域里是最后一次修改该行的那次提交的 SHA-1 值。接下去的两个域是从那次提交中抽取的值——作者姓名和日期——所以你可以方便地获知谁在什么时候修改了这一行。在这后面是行号和文件的内容。请注意 ^4832fe2 提交的那些行，这些指的是文件最初提交的那些行。那个提交是文件第一次被加入这个项目时存在的，自那以后未被修改过。  

在 Git 中你不需要显式地记录文件的重命名。它会记录快照然后根据现实尝试找出隐式的重命名动作。这其中有一个很有意思的特性就是你可以让它找出所有的代码移动。如果你在 `git blame` 后加上 `-C` ，Git 会分析你在标注的文件然后尝试找出其中代码片段的原始出处，如果它是从其他地方拷贝过来的话。  

我在将一个名叫 GITServerHandler.m 的文件分解到多个文件中，其中一个是 GITPackUpload.m 。通过对 GITPackUpload.m 执行带 `-C` 参数的 `blame` 命令，我可以看到代码块的原始出处：  
```shell
$ git blame -C -L 141,153 GITPackUpload.m
f344f58d GITServerHandler.m (Scott 2009-01-04 141)
f344f58d GITServerHandler.m (Scott 2009-01-04 142) - (void) gatherObjectShasFromC
f344f58d GITServerHandler.m (Scott 2009-01-04 143) {
70befddd GITServerHandler.m (Scott 2009-03-22 144)         //NSLog(@"GATHER COMMI
ad11ac80 GITPackUpload.m    (Scott 2009-03-24 145)
ad11ac80 GITPackUpload.m    (Scott 2009-03-24 146)         NSString *parentSha;
ad11ac80 GITPackUpload.m    (Scott 2009-03-24 147)         GITCommit *commit = [g
ad11ac80 GITPackUpload.m    (Scott 2009-03-24 148)
ad11ac80 GITPackUpload.m    (Scott 2009-03-24 149)         //NSLog(@"GATHER COMMI
ad11ac80 GITPackUpload.m    (Scott 2009-03-24 150)
56ef2caf GITServerHandler.m (Scott 2009-01-05 151)         if(commit) {
56ef2caf GITServerHandler.m (Scott 2009-01-05 152)                 [refDict setOb
56ef2caf GITServerHandler.m (Scott 2009-01-05 153)
```
通常，你会把你拷贝代码的那次提交作为原始提交，因为这是你在这个文件中第一次接触到那几行。Git可以告诉你编写那些行的原始提交，即便是在另一个文件里。  

### 2. 二分查找  

标注文件在你知道问题是哪里引入的时候会有帮助。如果你不知道，并且自上次代码可用的状态已经经历了上百次的提交，你可能就要求助于 `bisect` 命令了。`bisect` 会在你的提交历史中进行二分查找来尽快地确定哪一次提交引入了错误。  

例如你刚刚推送了一个代码发布版本到产品环境中，对代码为什么会表现成那样百思不得其解。你回到你的代码中，还好你可以重现那个问题，但是找不到在哪里。你可以对代码执行 `bisect` 来寻找。首先你运行 `git bisect start` 启动，然后你用 `git bisect bad` 来告诉系统当前的提交已经有问题了。然后你必须告诉 `bisect` 已知的最后一次正常状态是哪次提交，使用 `git bisect good [good_commit]` ：  
```shell
$ git bisect start
$ git bisect bad
$ git bisect good v1.0
Bisecting: 6 revisions left to test after this
[ecb6e1bc347ccecc5f9350d878ce677feb13d3b2] error handling on repo
```
Git 发现在你标记为正常的提交(v1.0)和当前的错误版本之间有大约 12 次提交，于是它检出中间的一个。在这里，你可以运行测试来检查问题是否存在于这次提交。假设这里是没有错误的，那么你就通过 `git bisect good` 来告诉 Git 然后继续你的旅程：  
```shell
$ git bisect good
Bisecting: 3 revisions left to test after this
[b047b02ea83310a70fd603dc8cd7a6cd13d15c04] secure this thing
```
现在你在另外一个提交上了，在你刚刚测试通过的和一个错误提交的中点处。你再次运行测试然后发现这次提交是错误的，因此你通过 `git bisect bad` 来告诉 Git：  
```shell
$ git bisect bad
Bisecting: 1 revisions left to test after this
[f71ce38690acf49c1f3c9bea38e09d82a5ce6014] drop exceptions table
```
这次提交是好的，那么 Git 就获得了确定问题引入位置所需的所有信息。它告诉你第一个错误提交的 SHA-1 值并且显示一些提交说明以及哪些文件在那次提交里修改过，这样你可以找出缺陷被引入的根源：  
```shell
$ git bisect good
b047b02ea83310a70fd603dc8cd7a6cd13d15c04 is first bad commit
commit b047b02ea83310a70fd603dc8cd7a6cd13d15c04
Author: PJ Hyett <pjhyett@example.com>
Date:   Tue Jan 27 14:48:32 2009 -0800

    secure this thing

:040000 040000 40ee3e7821b895e52c1695092db9bdc4c61d1730
f24d3c6ebcfc639b1a3814550e62d60b8e68a8e4 M  config
```
当你完成之后，你应该运行 `git bisect reset` 来重设你的HEAD到你开始前的地方，  
```shell
$ git bisect reset
```
这是个强大的工具，可以帮助你检查上百的提交，在几分钟内找出缺陷引入的位置。事实上，如果你有一个脚本会在工程正常时返回0，错误时返回非0的话，你可以完全自动地执行 `git bisect` 。首先你需要提供已知的错误和正确提交来告诉它二分查找的范围。你可以通过 `bisect start` 命令来列出它们，先列出已知的错误提交再列出已知的正确提交：  
```shell
$ git bisect start HEAD v1.0
$ git bisect run test-error.sh
```
这样会自动地在每一个检出的提交里运行 `test-error.sh` 直到 Git 找出第一个破损的提交。你也可以运行像 `make` 或者` make tests` 或者任何你所拥有的来为你执行自动化的测试。  

## 6. 子模块  

当你在一个项目上工作时，你需要在其中使用另外一个项目。也许它是一个第三方开发的库或者是你独立开发和并在多个父项目中使用的。这个场景下一个常见的问题产生了：你想将两个项目单独处理但是又需要在其中一个中使用另外一个。  
假设你在开发一个网站，为之创建Atom源。你不想编写一个自己的Atom生成代码，而是决定使用一个库。你可能不得不像CPAN install或者Ruby gem一样包含来自共享库的代码，或者将代码拷贝到你的项目树中。如果采用包含库的办法，那么不管用什么办法都很难去定制这个库，部署它就更加困难了，因为你必须确保每个客户都拥有那个库。把代码包含到你自己的项目中带来的问题是，当上游被修改时，任何你进行的定制化的修改都很难归并。  

Git 通过子模块处理这个问题。子模块允许你将一个 Git 仓库当作另外一个Git仓库的子目录。这允许你克隆另外一个仓库到你的项目中并且保持你的提交相对独立。  


### 1. 子模块初步  

假设你想把 Rack 库（一个 Ruby 的 web 服务器网关接口）加入到你的项目中，可能既要保持你自己的变更，又要延续上游的变更。首先你要把外部的仓库克隆到你的子目录中。你通过 `git submodule add` 将外部项目加为子模块：  
```shell
$ git submodule add git://github.com/chneukirchen/rack.git rack
Initialized empty Git repository in /opt/subtest/rack/.git/
remote: Counting objects: 3181, done.
remote: Compressing objects: 100% (1534/1534), done.
remote: Total 3181 (delta 1951), reused 2623 (delta 1603)
Receiving objects: 100% (3181/3181), 675.42 KiB | 422 KiB/s, done.
Resolving deltas: 100% (1951/1951), done.
```
现在你就在项目里的rack子目录下有了一个 `Rack` 项目。你可以进入那个子目录，进行变更，加入你自己的远程可写仓库来推送你的变更，从原始仓库拉取和归并等等。如果你在加入子模块后立刻运行 `git status` ，你会看到下面两项：  
```shell
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#      new file:   .gitmodules
#      new file:   rack
#
```
首先你注意到有一个.gitmodules文件。这是一个配置文件，保存了项目 URL 和你拉取到的本地子目录  
```shell
$ cat .gitmodules
[submodule "rack"]
      path = rack
      url = git://github.com/chneukirchen/rack.git
```
如果你有多个子模块，这个文件里会有多个条目。很重要的一点是这个文件跟其他文件一样也是处于版本控制之下的，就像你的 `.gitignore` 文件一样。它跟项目里的其他文件一样可以被推送和拉取。这是其他克隆此项目的人获知子模块项目来源的途径。  
`git status` 的输出里所列的另一项目是 `rack` 。如果你在那上面运行 `git diff`，会发现一些有趣的东西：  
```shell
$ git diff --cached rack
diff --git a/rack b/rack
new file mode 160000
index 0000000..08d709f
--- /dev/null
+++ b/rack
@@ -0,0 +1 @@
+Subproject commit 08d709f78b8c5b0fbeb7821e37fa53e69afcf433
```
尽管 `rack` 是你工作目录里的子目录，但 Git 把它视作一个子模块，当你不在那个目录里时并不记录它的内容。取而代之的是，Git 将它记录成来自那个仓库的一个特殊的提交。当你在那个子目录里修改并提交时，子项目会通知那里的 HEAD 已经发生变更并记录你当前正在工作的那个提交；通过那样的方法，当其他人克隆此项目，他们可以重新创建一致的环境。  

这是关于子模块的重要一点：你记录他们当前确切所处的提交。你不能记录一个子模块的 `master` 或者其他的符号引用。  

当你提交时，会看到类似下面的：  
```shell
$ git commit -m 'first commit with submodule rack'
[master 0550271] first commit with submodule rack
 2 files changed, 4 insertions(+), 0 deletions(-)
 create mode 100644 .gitmodules
 create mode 160000 rack
```
注意 rack 条目的 160000 模式。这在Git中是一个特殊模式，基本意思是你将一个提交记录为一个目录项而不是子目录或者文件。  
你可以将 `rack` 目录当作一个独立的项目，保持一个指向子目录的最新提交的指针然后反复地更新上层项目。所有的Git命令都在两个子目录里独立工作：  


### 2. 克隆一个带子模块的项目  

这里你将克隆一个带子模块的项目。当你接收到这样一个项目，你将得到了包含子项目的目录，但里面没有文件：  
```shell
$ git clone git://github.com/schacon/myproject.git
Initialized empty Git repository in /opt/myproject/.git/
remote: Counting objects: 6, done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 6 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (6/6), done.
$ cd myproject
$ ls -l
total 8
-rw-r--r--  1 schacon  admin   3 Apr  9 09:11 README
drwxr-xr-x  2 schacon  admin  68 Apr  9 09:11 rack
$ ls rack/
$
```
`rack` 目录存在了，但是是空的。你必须运行两个命令： `git submodule init` 来初始化你的本地配置文件， `git submodule update` 来从那个项目拉取所有数据并检出你上层项目里所列的合适的提交：  
```shell
$ git submodule init
Submodule 'rack' (git://github.com/chneukirchen/rack.git) registered for path 'rack'
$ git submodule update
Initialized empty Git repository in /opt/myproject/rack/.git/
remote: Counting objects: 3181, done.
remote: Compressing objects: 100% (1534/1534), done.
remote: Total 3181 (delta 1951), reused 2623 (delta 1603)
Receiving objects: 100% (3181/3181), 675.42 KiB | 173 KiB/s, done.
Resolving deltas: 100% (1951/1951), done.
Submodule path 'rack': checked out '08d709f78b8c5b0fbeb7821e37fa53e69afcf433'
```
现在你的 `rack` 子目录就处于你先前提交的确切状态了。如果另外一个开发者变更了 `rack` 的代码并提交，你拉取那个引用然后归并之，将得到稍有点怪异的东西：  
```shell
$ git merge origin/master
Updating 0550271..85a3eee
Fast forward
 rack |    2 +-
 1 files changed, 1 insertions(+), 1 deletions(-)
[master*]$ git status
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#      modified:   rack
#
```
你归并来的仅仅上是一个指向你的子模块的指针；但是它并不更新你子模块目录里的代码，所以看起来你的工作目录处于一个临时状态：  
```shell
$ git diff
diff --git a/rack b/rack
index 6c5e70b..08d709f 160000
--- a/rack
+++ b/rack
@@ -1 +1 @@
-Subproject commit 6c5e70b984a60b3cecd395edd5b48a7575bf58e0
+Subproject commit 08d709f78b8c5b0fbeb7821e37fa53e69afcf433
```
因为你所拥有的指向子模块的指针和子模块目录的真实状态并不匹配。为了修复这一点，你必须再次运行 `git submodule update` ：  
```shell
$ git submodule update
remote: Counting objects: 5, done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 1), reused 2 (delta 0)
Unpacking objects: 100% (3/3), done.
From git@github.com:schacon/rack
   08d709f..6c5e70b  master     -> origin/master
Submodule path 'rack': checked out '6c5e70b984a60b3cecd395edd5b48a7575bf58e0'
```
每次你从主项目中拉取一个子模块的变更都必须这样做。  

一个常见问题是当开发者对子模块做了一个本地的变更但是并没有推送到公共服务器。然后他们提交了一个指向那个非公开状态的指针然后推送上层项目。当其他开发者试图运行 `git submodule update`，那个子模块系统会找不到所引用的提交，因为它只存在于第一个开发者的系统中。如果发生那种情况，你会看到类似这样的错误：  
```shell
$ git submodule update
fatal: reference isn’t a tree: 6c5e70b984a60b3cecd395edd5b48a7575bf58e0
Unable to checkout '6c5e70b984a60b3cecd395edd5ba7575bf58e0' in submodule path 'rack'
```
你不得不去查看谁最后变更了子模块  
```shell
$ git log -1 rack
commit 85a3eee996800fcfa91e2119372dd4172bf76678
Author: Scott Chacon <schacon@gmail.com>
Date:   Thu Apr 9 09:19:14 2009 -0700

    added a submodule reference I will never make public. hahahahaha!
```

### 3. 上层项目  

有时候，开发者想按照他们的分组获取一个大项目的子目录的子集。  
在 Git 中实现这个的一个好办法是你将每一个子目录都做成独立的 Git 仓库，然后创建一个上层项目的 Git 仓库包含多个子模块。这个办法的一个优势是你可以在上层项目中通过标签和分支更为明确地定义项目之间的关系。  

### 4. 子模块的问题  

使用子模块并非没有任何缺点。首先，你在子模块目录中工作时必须相对小心。当你运行 `git submodule update` ，它会检出项目的指定版本，但是不在分支内。这叫做获得一个分离的头——这意味着 `HEAD` 文件直接指向一次提交，而不是一个符号引用。问题在于你通常并不想在一个分离的头的环境下工作，因为太容易丢失变更了。如果你先执行了一次 `submodule update` ，然后在那个子模块目录里不创建分支就进行提交，然后再次从上层项目里运行 `git submodule update` 同时不进行提交，Git 会毫无提示地覆盖你的变更。技术上讲你不会丢失工作，但是你将失去指向它的分支，因此会很难取到。  
为了避免这个问题，当你在子模块目录里工作时应使用 `git checkout -b work` 创建一个分支。当你再次在子模块里更新的时候，它仍然会覆盖你的工作，但是至少你拥有一个可以回溯的指针。  

切换带有子模块的分支同样也很有技巧。如果你创建一个新的分支，增加了一个子模块，然后切换回不带该子模块的分支，你仍然会拥有一个未被追踪的子模块的目录  
```shell
$ git checkout -b rack
Switched to a new branch "rack"
$ git submodule add git@github.com:schacon/rack.git rack
Initialized empty Git repository in /opt/myproj/rack/.git/
...
Receiving objects: 100% (3184/3184), 677.42 KiB | 34 KiB/s, done.
Resolving deltas: 100% (1952/1952), done.
$ git commit -am 'added rack submodule'
[rack cc49a69] added rack submodule
 2 files changed, 4 insertions(+), 0 deletions(-)
 create mode 100644 .gitmodules
 create mode 160000 rack
$ git checkout master
Switched to branch "master"
$ git status
# On branch master
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#      rack/
```
你将不得不将它移走或者删除，这样的话当你切换回去的时候必须重新克隆它——你可能会丢失你未推送的本地的变更或分支。  

最后一个需要引起注意的是关于从子目录切换到子模块的。如果你已经跟踪了你项目中的一些文件但是想把它们移到子模块去，你必须非常小心。  
假设你的项目中有一个子目录里放了 `rack` 的文件，然后你想将它转换为子模块。如果你删除子目录然后运行 `submodule add` ，  
```shell
$ rm -Rf rack/
$ git submodule add git@github.com:schacon/rack.git rack
'rack' already exists in the index
```
你必须先将 `rack` 目录撤回。然后你才能加入子模块：  
```shell
$ git rm -r rack
$ git submodule add git@github.com:schacon/rack.git rack
Initialized empty Git repository in /opt/testsub/rack/.git/
remote: Counting objects: 3184, done.
remote: Compressing objects: 100% (1465/1465), done.
remote: Total 3184 (delta 1952), reused 2770 (delta 1675)
Receiving objects: 100% (3184/3184), 677.42 KiB | 88 KiB/s, done.
Resolving deltas: 100% (1952/1952), done.
```
现在假设你在一个分支里那样做了。如果你尝试切换回一个仍然在目录里保留那些文件而不是子模块的分支时——你会得到下面的错误：  
```shell
$ git checkout master
error: Untracked working tree file 'rack/AUTHORS' would be overwritten by merge.
```
你必须先移除 `rack` 子模块的目录才能切换到不包含它的分支，当你切换回来，你会得到一个空的 `rack` 目录。你可以运行 `git submodule update` 重新克隆，也可以将 `/tmp/rack` 目录重新移回空目录。  

## 7. 子树合并  

现在你已经看到了子模块系统的麻烦之处，让我们来看一下解决相同问题的另一途径。当 Git 归并时，它会检查需要归并的内容然后选择一个合适的归并策略。如果你归并的分支是两个，Git使用一个*递归策略*。如果你归并的分支超过两个，Git采用*章鱼策略*。这些策略是自动选择的，因为*递归策略*可以处理复杂的三路归并情况——比如多于一个共同祖先的——但是它只能处理两个分支的归并。*章鱼归并*可以处理多个分支但是但必须更加小心以避免冲突带来的麻烦，因此它被选中作为归并两个以上分支的默认策略。  
实际上，你也可以选择其他策略。其中的一个就是*子树归并*，你可以用它来处理子项目问题。这里你会看到如何换用*子树归并*的方法来实现前一节里所做的 rack 的嵌入。  

**子树归并** 的思想是你拥有两个工程，其中一个项目映射到另外一个项目的子目录中，反过来也一样。当你指定一个子树归并，Git可以聪明地探知其中一个是另外一个的子树从而实现正确的归并。  

首先你将 `Rack` 应用加入到项目中。你将 `Rack` 项目当作你项目中的一个远程引用，然后将它检出到它自身的分支：  
```shell
$ git remote add rack_remote git@github.com:schacon/rack.git
$ git fetch rack_remote
warning: no common commits
remote: Counting objects: 3184, done.
remote: Compressing objects: 100% (1465/1465), done.
remote: Total 3184 (delta 1952), reused 2770 (delta 1675)
Receiving objects: 100% (3184/3184), 677.42 KiB | 4 KiB/s, done.
Resolving deltas: 100% (1952/1952), done.
From git@github.com:schacon/rack
 * [new branch]      build      -> rack_remote/build
 * [new branch]      master     -> rack_remote/master
 * [new branch]      rack-0.4   -> rack_remote/rack-0.4
 * [new branch]      rack-0.9   -> rack_remote/rack-0.9
$ git checkout -b rack_branch rack_remote/master
Branch rack_branch set up to track remote branch refs/remotes/rack_remote/master.
Switched to a new branch "rack_branch"
```
现在在你的 `rack_branch` 分支中就有了 `Rack` 项目的根目录，而你自己的项目在 `master` 分支中。如果你先检出其中一个然后另外一个，你会看到它们有不同的项目根目录：  
```shell
$ ls
AUTHORS	       KNOWN-ISSUES   Rakefile      contrib	       lib
COPYING	       README         bin           example	       test
$ git checkout master
Switched to branch "master"
$ ls
README
```
要将 `Rack` 项目当作子目录拉取到你的 `master` 项目中。你可以在 Git 中用 `git read-tree` 来实现。它读取一个分支的根目录树到当前的暂存区和工作目录。你只要切换回你的 `master` 分支，然后拉取 `rack_branch` 到你主项目的 `master` 分支的 `rack` 子目录：  
```shell
$ git read-tree --prefix=rack/ -u rack_branch
```
当你提交的时候，看起来就像你在那个子目录下拥有 `Rack` 的文件——就像你从一个 `tarball` 里拷贝的一样。有意思的是你可以比较容易地归并其中一个分支的变更到另外一个。因此，如果 `Rack` 项目更新了，你可以通过切换到那个分支并执行拉取来获得上游的变更：  
```shell
$ git checkout rack_branch
$ git pull
```
然后，你可以将那些变更归并回你的 `master` 分支。你可以使用 `git merge -s subtree` ，它会工作的很好；但是 Git 同时会把历史归并到一起，这可能不是你想要的。为了拉取变更并预置提交说明，需要在 `-s subtree` 策略选项的同时使用 `--squash和--no-commit` 选项。  
```shell
$ git checkout master
$ git merge --squash -s subtree --no-commit rack_branch
Squash commit -- not updating HEAD
Automatic merge went well; stopped before committing as requested
```
所有 `Rack` 项目的变更都被归并并且可以进行本地提交。你也可以做相反的事情——在你主分支的 `rack` 目录里进行变更然后归并回 `rack_branch` 分支，然后将它们提交给维护者或者推送到上游。  
为了得到 `rack` 子目录和你 `rack_branch` 分支的区别——以决定你是否需要归并它们——你不能使用一般的 `diff` 命令。而是对你想比较的分支运行 `git diff-tree` ：  
```shell
$ git diff-tree -p rack_branch
```
或者，为了比较你的 `rack` 子目录和服务器上你拉取时的 `master` 分支，你可以运行  
```shell
$ git diff-tree -p rack_remote/master
```

# 自定义 Git  

## 1. 配置 Git  

用 `git config` 配置 Git，要做的第一件事就是设置名字和邮箱地址：  
```shell
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```
Git 使用一系列的配置文件来存储你定义的偏好，它首先会查找 `/etc/gitconfig` 文件，该文件含有 对系统上所有用户及他们所拥有的仓库都生效的配置值（译注： `gitconfig` 是全局配置文件）， 如果传递 `--system` 选项给 `git config` 命令， Git 会读写这个文件。 接下来 Git 会查找每个用户的 `~/.gitconfig` 文件，你能传递 `--global` 选项让 Git读写该文件。  最后 Git 会查找由用户定义的各个库中 Git 目录下的配置文件（`.git/config`），该文件中的值只对属主库有效。 以上阐述的三层配置从一般到特殊层层推进，如果定义的值有冲突，以后面层中定义的为准，  

### 1. 客户端基本配置  

Git 能够识别的配置项被分为了两大类：客户端和服务器端，其中大部分基于你个人工作偏好，属于客户端配置。尽管有数不尽的选项，但我只阐述 其中经常使用或者会对你的工作流产生巨大影响的选项，如果你想观察你当前的 Git 能识别的选项列表，请运行  
```shell
$ git config --help
```
`git config` 的手册页（译注：以man命令的显示方式）非常细致地罗列了所有可用的配置项。  

**core.editor** 
Git 默认会调用你的环境变量 editor 定义的值作为文本编辑器，如果没有定义的话，会调用Vi来创建和编辑提交以及标签信息， 你可以使用 `core.editor` 改变默认编辑器：  
```shell
$ git config --global core.editor emacs
```
现在无论你的环境变量 editor 被定义成什么，Git 都会调用 Emacs 编辑信息。  

**commit.template**  
如果把此项指定为你系统上的一个文件，当你提交的时候， Git 会默认使用该文件定义的内容。 例如：你创建了一个模板文件 `$HOME/.gitmessage.txt` ，它看起来像这样：  
```
subject line

what happened

[ticket: X]
```
设置 `commit.template` ，当运行 `git commit` 时， Git 会在你的编辑器中显示以上的内容， 设置 `commit.template` 如下：  
```shell
$ git config --global commit.template $HOME/.gitmessage.txt
$ git commit
```
然后当你提交时，在编辑器中显示的提交信息如下：  
```
subject line

what happened

[ticket: X]
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
# modified:   lib/test.rb
#
~
~
".git/COMMIT_EDITMSG" 14L, 297C
```
如果你有特定的策略要运用在提交信息上，在系统上创建一个模板文件，设置 Git 默认使用它，这样当提交时，你的策略每次都会被运用。  

**core.pager**  
`core.pager` 指定 Git 运行诸如 `log` 、`diff` 等所使用的分页器，你能设置成用 more 或者任何你喜欢的分页器（默认用的是 less）， 当然你也可以什么都不用，设置空字符串：  
```shell
$ git config --global core.pager ''
```
这样不管命令的输出量多少，都会在一页显示所有内容。  

**user.signingkey**  
如果你要创建经签署的含附注的标签，那么把你的 GPG 签署密钥设置为配置项会更好，设置密钥 ID 如下：  
```shell
$ git config --global user.signingkey <gpg-key-id>
```
现在你能够签署标签，从而不必每次运行 `git tag` 命令时定义密钥：  
```shell
$ git tag -s <tag-name>
```

**core.excludesfile**  
你能在项目库的 `.gitignore` 文件里头用模式来定义那些无需纳入 Git 管理的文件，这样它们不会出现在未跟踪列表， 也不会在你运行 `git add` 后被暂存。然而，如果你想用项目库之外的文件来定义那些需被忽略的文件的话，用 `core.excludesfile`  通知 Git 该文件所处的位置，文件内容和 `.gitignore` 类似。  

**help.autocorrect**  
该配置项只在 Git 1.6.1及以上版本有效，假如你在Git 1.6中错打了一条命令，会显示：  
```shell
$ git com
git: 'com' is not a git-command. See 'git --help'.

Did you mean this?
     commit
```
如果你把 `help.autocorrect` 设置成 `1` （译注：启动自动修正），那么在只有一个命令被模糊匹配到的情况下，Git 会自动运行该命令。  

### 2. Git中的着色  

Git能够为输出到你终端的内容着色，以便你可以凭直观进行快速、简单地分析，有许多选项能供你使用以符合你的偏好。  

**color.ui**  
Git 会按照你需要自动为大部分的输出加上颜色，你能明确地规定哪些需要着色以及怎样着色，设置 `color.ui` 为 `true` 来打开所有的默认终端着色。  
```shell
$ git config --global color.ui true
```
设置好以后，当输出到终端时，Git 会为之加上颜色。其他的参数还有 `false` 和 `always` ，`false` 意味着不为输出着色， `always` 则表明在任何情况下都要着色，即使 Git 命令被重定向到文件或管道。Git 1.5.5版本引进了此项配置，如果你拥有的版本更老，你必须对颜色有关选项各自进行详细地设置。  
你会很少用到 `color.ui = always` ，在大多数情况下，如果你想在被重定向的输出中插入颜色码，你能传递 `--color` 标志给 Git 命令来迫使它这么做， `color.ui = true` 应该是你的首选。  

**color.\***  
想要具体到哪些命令输出需要被着色以及怎样着色或者 Git 的版本很老，你就要用到和具体命令有关的颜色配置选项，它们都能被置为 `true` 、`false` 或 `always`：  
```shell
color.branch
color.diff
color.interactive
color.status
```
除此之外，以上每个选项都有子选项，可以被用来覆盖其父设置，以达到为输出的各个部分着色的目的。例如，让 `diff` 输出的改变信息以粗体、蓝色前景和黑色背景的形式显示：  
```shell
$ git config --global color.diff.meta "blue black bold"
```
你能设置的颜色值如：`normal`、`black`、`red`、`green`、`yellow`、`blue`、`magenta`、`cyan`、`white`，正如以上例子设置的粗体属性，想要设置字体属性的话，可以选择如：`bold`、`dim`、`ul`、`blink`、`reverse`。

如果你想配置子选项的话，可以参考 `git config` 帮助页。  

### 3. 外部的合并与比较工具  

虽然 Git 自己实现了 `diff` ,而且到目前为止你一直在使用它，但你能够用一个外部的工具替代它，除此以外，你还能用一个图形化的工具来合并和解决冲突从而不必自己手动解决。有一个不错且免费的工具可以被用来做比较和合并工作，它就是 `P4Merge`（译注：`Perforce` 图形化合并工具），  
P4Merge可以在所有主流平台上运行，在Mac和Linux系统上，我会使用路径名，在Windows上，`/usr/local/bin` 应该被改为你环境中的可执行路径。  
下载 P4Merge：  
[http://www.perforce.com/product/components/perforce-visual-merge-and-diff-tools]()  
首先把你要运行的命令放入外部包装脚本中，我会使用 Mac 系统上的路径来指定该脚本的位置，在其他系统上，它应该被放置在二进制文件 `p4merge` 所在的目录中。创建一个 `merge` 包装脚本，名字叫作 `extMerge` ，让它带参数调用 `p4merge` 二进制文件：  
```shell
$ cat /usr/local/bin/extMerge
#!/bin/sh
/Applications/p4merge.app/Contents/MacOS/p4merge $*
```
`diff` 包装脚本首先确定传递过来 7 个参数，随后把其中 2 个传递给 `merge` 包装脚本，默认情况下， Git 传递以下参数给 `diff ：  
```shell
path old-file old-hex old-mode new-file new-hex new-mode
```
由于你仅仅需要 `old-file` 和 `new-file` 参数，用 `diff` 包装脚本来传递它们吧。  
```shell
$ cat /usr/local/bin/extDiff
#!/bin/sh
[ $# -eq 7 ] && /usr/local/bin/extMerge "$2" "$5"
```
确认这两个脚本是可执行的：  
```shell
$ sudo chmod +x /usr/local/bin/extMerge
$ sudo chmod +x /usr/local/bin/extDiff
```
在来配置使用你自定义的比较和合并工具吧。这需要许多自定义设置：  
`merge.tool` 通知 Git 使用哪个合并工具；  
`mergetool.*.cmd` 规定命令运行的方式；   
`mergetool.trustExitCode` 会通知 Git 程序的退出是否指示合并操作成功；  
`diff.external` 通知 Git 用什么命令做比较。  
因此，你能运行以下4条配置命令：  
```shell
$ git config --global merge.tool extMerge
$ git config --global mergetool.extMerge.cmd \
    'extMerge "$BASE" "$LOCAL" "$REMOTE" "$MERGED"'
$ git config --global mergetool.trustExitCode false
$ git config --global diff.external extDiff
```
或者直接编辑 `~/.gitconfig` 文件如下：  
```
[merge]
  tool = extMerge
[mergetool "extMerge"]
  cmd = extMerge \"$BASE\" \"$LOCAL\" \"$REMOTE\" \"$MERGED\"
  trustExitCode = false
[diff]
  external = extDiff
```
设置完毕后，运行diff命令：  
```shell
$ git diff 32d1776b1^ 32d1776b1
```
命令行居然没有发现 `diff` 命令的输出，其实，Git 调用了刚刚设置的 `P4Merge` ，  
当你设法合并两个分支，结果却有冲突时，运行 `git mergetool`，Git 会调用 `P4Merge` 让你通过图形界面来解决冲突。  
设置包装脚本的好处是你能简单地改变 `diff` 和 `merge` 工具，例如把 `extDiff` 和 `extMerge` 改成 `KDiff3` ，要做的仅仅是编辑 `extMerge` 脚本文件：  
```shell
$ cat /usr/local/bin/extMerge
#!/bin/sh
/Applications/kdiff3.app/Contents/MacOS/kdiff3 $*
```
现在 Git 会使用 `KDiff3` 来做比较、合并和解决冲突。

Git 预先设置了许多其他的合并和解决冲突的工具，而你不必设置 `cmd` 。可以把合并工具设置为：`kdiff3`、`opendiff`、`tkdiff`、`meld`、`xxdiff`、`emerge`、`vimdiff`、`gvimdiff`。如果你不想用到 `KDiff3` 的所有功能，只是想用它来合并，那么 `kdiff3` 正符合你的要求，运行：  
```shell
$ git config --global merge.tool kdiff3
```
如果运行了以上命令，没有设置 `extMerge` 和 `extDiff` 文件，Git 会用 `KDiff3` 做合并，让通常内设的比较工具来做比较。  

### 4. 格式化与空白  






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

---
> 参考链接  
> [Git 官网](https://git-scm.com)  
> [Git Github仓库](https://github.com/git/git)  
> [Git](https://kapeli.com/cheat_sheets/Git.docset/Contents/Resources/Documents/index)  
> [图解 Git](http://marklodato.github.io/visual-git-guide/index-zh-cn.html#basic-usage)  
> [Pro Git](http://iissnan.com/progit/)  
> [Git 教程](http://www.runoob.com/git/git-tutorial.html)  
> [git - 简易指南](http://www.bootcss.com/p/git-guide/)  
