
# Git 笔记 （2） #

## 本地库 ##
### 初始化/添加文件 ###


1. `mkdir test`  &emsp;//创建文件夹test

2. `cd /d/GitHub/test` &emsp;//进入目录

3. 输入：`git init`
 
4. 文件添加到暂存区：`git add `

5. 文件添加到本地库：`git commit -m “comment”`

### 本地库文件管理  ###
1. `git status` &emsp; //查看库文件状态


2. `git diff`&emsp; //查看库文件修改情况

3. `git rm` &emsp; //移除库文件
    > `git rm —cached <file>`可以移除远程库中的文件
    
4. `git checkout —file`&emsp; //撤销修改

## 远程库(GitHub网站) ##
### 推送到远程库 ###

1. 创建远程库
在`GitHub`网站上创建一个仓库(目前已经测试同名仓库，不同名仓库应该一样操作).
   >例如：`test`远程库

2. 创建ssh秘钥
  ```
  ssh-keygen -t rsa -C “youremail@example.com” 
  ```
   将`.ssh`目录中的`id_rsa.pub`秘钥复制到GitHub网站的`SSH Keys`中.


3. 关联本地库和远程库
打开Git Bash，进入本地库路径，输入 
```
 $ git remote add origin https://github.com/yuchengqi9/test.git
 $ git push -u origin master
```

> - 此处的 `-u`为第一次推送时所需，可以通过`git help push`查看说明</br>
以后推送时只需要使用`git push origin master`即可.
> - `git push -f origin master`可以强行推送，覆盖远程端的冲突，不过建议先`pull`到本地，然后 `git add *`···`git push`. 
> - **git remote add origin git@github.com:yuchengqi9/test.git**速度比上面`https`速度更快


### 从远程库克隆到本地  ###
```
git clone git@github.com:yuchengqi9/test.git
```
### 分支 ###
1. 创建分支```git checkout -b dev```，创建分支`dev`,并切换到`dev`，相当于两条指令：
   ```
    git branch dev,
    git checkout dev
   ```


2. 返回主分支`master`并合并`dev`
   ```
   git checkout master
   git merge dev
   ```


3. 删除`dev`分支
   ```git
   git branch -d dev
   ```
### pull到本地 ###
1. `git pull <远程主机名><远程分支名>:<本地分支名>`
 
2. 如果远程分支和当前分支合并，则可以省略本地分支 `git pull origin master`

3. 如果远程只有一个master分支和当前分支合并` git pull`
>如果不同终端的修改文件在上传下载时，会出现`refuse to merge unlated histories`，此时可以用`git pull —allow-unrelated-histories`命令下载到本地，然后修改重新`add—>commit—>push`到远端.

## 删除远程和本地仓库  ##
1. 进入本地`master`路径</br>
2. `git pull origin master`
3. `dir` &emsp;查看库目录
4. `git rm -r —cached target`&emsp; 删除`target`文件,`cached`命令可以只删除库中文件
5. `git commit ‘Delete target’`
6. `git push -u origin master`

>批量删除可以使用`git rm —cached *.docx `

### 各种删除 ###
>待更新
[git撤销大全](https://blog.csdn.net/bdss58/article/details/50363830)