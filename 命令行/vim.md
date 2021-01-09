# vim

> 建议初学者读一读 [简明 VIM 练级攻略](https://coolshell.cn/articles/5426.html) 会助你更高效的学习 vim  
> [给程序员的VIM速查卡](https://coolshell.cn/articles/5479.html)  
> [vim 大冒险](http://vim-adventures.com/) 以游戏的方式学习 vim  
> [无插件VIM编程技巧](https://coolshell.cn/articles/11312.html)  

`:help` 帮助文档  

## 基础

### 快捷键

`i` 进入模式（insert）  
`u` 回溯之前的操作
`Esc` (`ctrl+c`/`ctrl+[`）退出编辑  

进入插入模式：  

`a` append 在当前字母的后面插入  
`i` insert 在当前字母的前面插入  
`o` open  line bello 在下面新建一行插入   

`A` ppend after line 在当前行的最后插入  
`I` insert before line 在当前行的最前插入  
`O` ppend a line above 在上新建一行插入  

退出模式：  

`:q` 退出当前文件  
`:wq` 保存退出当前文件  

命令模式：  

文件操作：  

`:set nu` 显示行号  
`:vs` 竖分屏  
`:sp` 横分屏  
`:e!` 重新加载文件（不保存当前更改）

查找：  

`:% s` 查找/搜索  

visual(可视)模式：

`v` 进入可视模式  
`V` 选择行  
`ctrl+v` 选择块  
`d` 删除  
`y` 复制  
`p` 粘贴  

### 编辑

`ctrl+h` 删除上一个字符  
`crel+w` 删除上一个单词  
`crrl+u` 删除当前行  

> 以上三个快捷键在终端中通用  
> 
> 终端中的其它一些快捷键：  
> `ctrl+a` 将光标移动到行首  
> `crel+e` 将光标移动到行尾  
> `crel+b` 向前移动光标  
> `crrl+f` 向后移动光标  

`gi` 快速跳转到最近编辑的位置，并进入编辑模式  

### 移动

- 字符间移动
  - `h` 左移
  - `j`下移
  - `k`上移
  - `l`右移
- 单词间移动
  - `w/W` 移动到下一个 world/WORLD 开头
  - `e/E` 移动到下一个 world/WORLD 结尾
  - `b/B` 返回上一个 world/WORLD 开头，可理解为 backw（wrold：以非空白符分割的单词，WORLD：以空白符分割的单词）
- 行间搜索
  - `f(char)` 移动到 char
  - `t` 移动到 char 的前一个字符
  - `;` 上一个
  - `,` 下一个
- 行间移动
  - `0` 移动到行首
  - `^` 移动到第一个非空白字符
  - `$` 移动到行尾
  - `g` 移动到行尾非空字符
- 垂直移动
  - `(`/`)` 在句子间移动
  - `{`/`}` 在段落间移动（插件 easy-motion 可简化操作）
- 页面移动
  - `gg/G` 移动到文件开头和结尾
  - `crel+1` 快速返回
  - `H/M/L` 快速跳转到屏幕的开头（Head）/中间（Middle）/结尾（Lower）
  - `ctrl+u/ctrl+f` 上下翻页（upward/forward）
  - `zz` 把屏幕置中

### 增删改查

- 增 `a i o A I O`
  - `a` append 在当前字母的后面插入  
  - `i` insert 在当前字母的前面插入  
  - `o` open  line bello 在下面新建一行插入   
  - `A` ppend after line 在当前行的最后插入  
  - `I` insert before line 在当前行的最前插入  
  - `O` ppend a line above 在上新建一行插入 
- 删 `x d`
  - nmomal/view 模式下 
    - `x` 快速删除一个字符，
    - `d`(delete) 快速删除一个单词(daw - d around word)
      - `dd` 删除一行
      - `dw` 删除一个单词 `daw`(default) 删除单词和空格，`diw` 仅删除单词
      - `dt)`(delete to `)`) 删除到 `)` 的内容
      - `dt$` 删除到行尾
      - `dt0` 删除到行首
    - `x` 和 `d` 都可以配合数字多次执行(数字+命令)
- 改 `r c s R C S`
  - namal 模式下
    - `r`(replace) 替换一个字符
    - `R` 不断替换替换后面一个字符
    - `s`(substitute) 替换并进入编辑模式
    - `S` 替换整行并进入插入模式
    - `c`(change) 修改 删除（用法与 `d` 相似）并进入插入模式
    - `C` 删除整行并进入插入模式
- 查 `/ ? n/N */#`
  - `/` 或 `?` 向前/反向查询
  - `n/N` 跳转到上一个/下一个匹配
  - `*/#` 进行当前单词的前向/后向匹配

> 配置  
>  
> :set hls - hight light search 高亮搜索结果  
> :set incsearch - incrament search 增量搜索  

### 搜索替换

- substitute - `:[range]s[ubstitute]/[pattern]/[string]/[glags]` 查找并替换文本（支持正则表达式）

range 范围，pattern 搜索(替换)模式，string 替换后的文本，flags 标志
- range `10,20` 表示 10-20 行，`%` 表示 全部
- flags 
  - `g`(global) 全局范围内执行
  - `c`(confirm) 执行前询问是否执行
  - `n`(number) 报告匹配的范围而不替换，可用于查询匹配次数

### 多文件操作

文件相关的概念  

- buffer 打开的一个文件的内存缓冲区
  - `:ls` 列举当前缓冲区
  - `:b n` 跳到第 n 个缓冲区
  - `:bpre`/`bnext`/`bfirst`/`blast` 跳到 上一个/下一个/第一个/最后一个 缓冲区
  - `:b buffer_name` 跳转

> `:e file_name` 打开文件（同时打开多个文件）

- window buffer 可视化的分割区域
  - 一个缓冲区可分割为多个窗口，每个窗口可以打开不同缓冲区
  - 每个窗口可进行无限分割
  - `ctrl+w>s` 水平分割，`ctrl+w>v` 垂直分割，或者`:sp` `:vs`

窗口切换（切换窗口的命令都是采用`ctrl+w`(window 作为前缀)）

| 命令       | 用途
|:----------|----------------|
| `ctrl+w>w` | 在窗口间循环切换
| `ctrl+w>h` | 切换到左边的窗口
| `ctrl+w>j` | 切换到下边的窗口
| `ctrl+w>k` | 切换到上边的窗口
| `ctrl+w>l` | 切换到右边的窗口

移动窗口（切换窗口的命令都是采用`ctrl+w`(window 作为前缀)）

| 命令       | 用途
|:----------|------------------------|
| `ctrl+w>W` | 将当前窗口在窗口间循环移动
| `ctrl+w>H` | 将当前窗口移动到左边的窗口
| `ctrl+w>J` | 将当前窗口移动到下边的窗口
| `ctrl+w>K` | 将当前窗口移动到上边的窗口
| `ctrl+w>L` | 将当前窗口移动到右边的窗口

重排窗口大小(`:h window-resize` 查看帮助文档）

| 命令       | 用途
|:----------|---------------------------|
| `ctrl+w>=` | 使所有窗口等宽等高
| `ctrl+w>_` | 最大化活动窗口的高度
| `ctrl+w>|` | 最大化活动窗口的宽度
| `[n]ctrl+w>_` | 将动窗口的高度设置为 n 行
| `[n]ctrl+w>|` | 将动窗口的宽度设置为 n 行

- tab

可以组织窗口为一个工作区(:h tabpage) 查看文档

| 命令       | 用途
|:----------|---------------------------|
| `:tabnew file_name` | 新建一个标签页
| `:tabe[dit] file_name` | 在新标签中打开文件
| `ctrl+w>T` | 将当前窗口移动到新标签页
| `:tabc[lose]` | 关闭当前标签及其所有窗口
| `:tabo[nly]` | 关闭除当前窗口外的所有其它窗口

tab 标签切换

| Ex 命令         | 普通模式 | 用途
|:---------------|:--------|----------------|
| `:tabn[ext] {N}` | `{N}gt` | 切换到编号为 N 的标签页
| `tabn[ext]`      | `gt`    | 切换到下一个标签页
| `tabp[revious]`  | `gT`    | 切换到上一个标签页

### 文本对象（text-object）

- `[number]<command>[text-object]`

- number - 表示次数
- command 命令 - d(delete), c(change), y(yank)
- text-object 文本对象 - w(单词), s(句子), p(段落)

> `iw`(inner word)。如果键入 `viw` 命令，那么首先将进入选择模式，然后 `iw` 将选中当前  
> `aw`(a word)，它不但会选中当前单词，还会包含当前单词之后的空格。  
> 
> 以下实例中的 [] 表示作用范围:  
> `iw` This is a [test] sentence.  
> `aw` This is a [test ]sentence.  
> `iW` This is a [...test...) sentence.  
> `aW` This is a [...test... jsentence.  
> `is` ..sentence. [This is a sentence.] This..  
> `as` ..sentence.[This is a sentence. ]This..End of previous paragraph.  
> `ip` [This is a paragraph. It has two sentences.  
The next  
End of previous paragraph.  
> `ap` [This is a paragraph. It has two sentences.  
]The next

### 复制粘贴与寄存器

#### 复制粘贴

- normal 模式
  - `y`(yank) 复制, `p`(put) 粘贴, `d` 和 `p` 剪切
  - 使用 `v`(visual) 选中要复制的区域再用 `p` 粘贴
  - 配合文本对象 `yiw` 复制一个单词，`yy` 复制一行
- insert 模式
  - 受用系统的复制粘贴的快捷键
  - `ctrl+r>+` 粘贴系统剪贴板的内容

> 一个坑  
> 在 vimrc 中设置 autoindent, 粘贴 python 代码缩进错乱  
> 解决办法：(3种选其一)
> 1. `:set paste` 和 `:set nopaste`
> 2. `"+p` 使用系统剪贴板
> 3. `:set clipboard=unnamed` 与 2 本周相同，可完美解决此问题

#### 寄存器

- vim 复制粘贴操作的是寄存器而不是系统剪贴板
- 默认情况下受用 `d`(删除) 或者 `y`(复制) 的内容存放在 “无名寄存器”
- 通过 `"{register}` 可以指定寄存器，不指定用默认的 “无名寄存器”(`""` 表示使用 “无名寄存器”)
- `:reg reg_name` 查看寄存器 `reg_name` 的内容

常见寄存器

- `"0` 复制专用寄存器 - 使用 `y` 复制文本同时会拷贝到复制寄存器0（`echo has('clipboard')` 输出 1，才可支持）
- `"+` 系统剪贴板 - `"+y` 复制到系统剪贴板，`"+p` 从系统剪贴板粘贴
- `"%` 当前文件名
- `".` 上次输入的文本

> `:set clipboard=unnamed` 将默认寄存器设置为系统剪贴板，此时就可以直接复制粘贴系统剪贴板的内容。如使用 `y` 会将内容直接粘贴到系统剪贴板，`p` 会直接从系统姐铁板粘贴内容

> 示例：
> `"ayiw` 复制一个单词到寄存器 `a`
> `"dbd` 删除当前行到寄存器 `b`
> `"ap` 粘贴寄存器 `a` 中的内容

### 宏（macro）

宏是一系列命令的集合，可以使用宏“录制”一些列操作，然后用于”回放“，宏可以非常方便的用于多行文本，录制的宏会保存在寄存器中

- normal 模式
  - `q` 开始/结束录制
  - `q[register]` 选择要保存宏的寄存器
  - `@[register]` 回放保存在寄存器中的宏

> 在view 模式下使用 normal 下的命令： `:normal [命令]`

### vim 中的补全

补全一般有三种类型：

1. `ctrl+n`, `ctrl+p` 补全单词
2. `ctrl+x`, `ctrl+f` 补全文件名
3. `ctrl+x`, `ctrl+o` 补全代码，需开启文件类型检测，安装插件

| 命令                | 补全类型 |
|:-------------------|---------------|
| `ctrl+n`           | 普通关键字
| `ctrl+x`, `ctrl+n` | 当前缓冲区关键字
| `ctrl+x`, `ctrl+i` | 包含文件关键字
| `ctrl+x`, `ctrl+j` | 标签文字关键字
| `ctrl+x`, `ctrl+k` | 字典查找
| `ctrl+x`, `ctrl+l` | 整行补全
| `ctrl+x`, `ctrl+f` | 文件名补全
| `ctrl+x`, `ctrl+o` | 全能（Omni） 补全

> 补全时若有多个匹配项可使用 `ctrl+n`(上一个) `ctrl+p`(下一个) 进行选择  
> `:r! echo %` 插入当前文件路径  
> `:r! echo %:p` 插入当前文件完整路径  

### vim 配色

- `:colorscheme` 显示当前配色
- `:colorchene <ctrl+d>` 显示所有
- `:colorcheme <配色名>` 修改配色

> 获取配色：  
> [rafi/awesome-vim-colorschemes](https://github.com/rafi/awesome-vim-colorschemes)  
> [vimcolorschemes](https://vimcolorschemes.com)  
> (flazz/vim-colorschemes)(https://github.com/flazz/vim-colorschemes)  


## 配置

vim 配置文件

- Linux/Unix 下新建一个配置文件 vim ~/.vimrc
- windows 系统 vim $MYVIMRC, 通过环境变量编辑配置文件

### 1. 常用设置

```text
" 常用设置
" (vimrc 中 " 表示注释)
" 设置行号
set number
" 设置语法高亮
syntax on
" 设置主题
colorscheme hybrid
" 按 F2 进入粘贴模式
set pastetoggle=<F2>
" 高亮搜索
set hlsearch
" 设置折叠方式
set foldmethod=indent
```

### 2. vim 中的映射

- 设置 leader 健：let mapleader = ','(通常是逗号或空格)
- 使用 `map` 可以实现映射，如：‘map [操作1] [操作2]’ 将 [操作2] 映射为 [操作1]
- 使用 `nmap/vmap/imap` 定义映射只在 normal/visual/insert 模式下生效
- `*map` 有递归风险，可使用 `nnoremap/vnoremao/inoremap` 代替 `nmap/vmap/imap` 命令(`*noremap` 不会递归解释，一般应始终使用 `*noremap` 命令)

## 插件使用

vim 插件管理器：[vim-plug](https://github.com/junegunn/vim-plug)(推荐), vundle, Pathogen, Dein.Vim, volt 等

vim 插件

vim 基本插件

- [vim-startify](https://github.com/mhinz/vim-startify) vim 开屏
- [vim-airline](https://github.com/vim-airline/vim-airline) vim 状态栏
- [indentLine](https://github.com/Yggdroot/indentLine) vim 缩进线

vim 美化

- [vim-hybrid](https://github.com/w0ng/vim-hybrid) vim 配色
- [solarized](https://github.com/altercation/solarized) vim 配色
- [gruvbox](https://github.com/morhetz/gruvbox) vim 配色

vim 文件目录

- [nerdtree](https://github.com/preservim/nerdtree) 文件树 `Plug 'scrooloose/nerdtree'`
- [ctrlp.vim](https://github.com/ctrlpvim/ctrlp.vim) 文件搜索 `Plug 'ctrlpvim/ctrlp.vim'`

vim 编辑

- [vim-easymotion](https://github.com/easymotion/vim-easymotion) vim 快速查找
- [vim-ssurround](https://github.com/tpope/vim-surround) vim 成对修改
- [vzf](https://github.com/junegunn/fzf) 命令行模糊搜索工具 | [fzf.vim](https://github.com/junegunn/fzf.vim) vim 模糊搜索
- [far.vim](https://github.com/brooth/far.vim) vim 搜索与替换

vim 代码编辑

- [vim-go](https://github.com/fatih/vim-go) golang `Plug 'fatih/vim-go', { 'do': ':GoUpdateBinaries' }`
- [python-mode](https://github.com/python-mode/python-mode) python `Plug 'python-mode/python-mode', { 'for': 'p    ython', 'branch': 'develop' }`
- [tagbar](https://github.com/preservim/tagbar) vim 代码大纲
- [vim-interestingwords](https://github.com/lfv89/vim-interestingwords) vim 高亮单词
- [deoplete.nvim](https://github.com/Shougo/deoplete.nvim) vim 代码补全
- [coc.vim](https://github.com/neoclide/coc.nvim) | [neoclide](https://github.com/neoclide) vim 代码补全 支持 LSP
- [Neoformat](https://github.com/sbdchd/neoformat) | [vim-autoformat](https://github.com/Chiel92/vim-autoformat) vim 格式化
- [neomake](https://github.com/neomake/neomake) | [ale](https://github.com/dense-analysis/ale) vim 静态检查(Lint)
- [vim-commentary](https://github.com/tpope/vim-commentary) vim 代码注释

vim git

- [vim-fugitive](https://github.com/tpope/vim-fugitive) git
- [vim-gitgutter](https://github.com/airblade/vim-gitgutter) 显示文件变动
- [gv.vim](https://github.com/junegunn/gv.vim) （[tig](https://github.com/jonas/tig) 命令行工具） 查看提交记录

寻找插件

[VimAwesome](https://vimawesome.com)  

## 与时俱进

与 vim 相关的工具

- [Tmux](https://github.com/tmux/tmux)
  - 【安装】brew(mac) aot-get(ubuntu)
  - 可以复用到终端、分屏、托管进程等
  - 在服务器上即使退出服务器也不会被 kill，托管进程很方便
  - 可以方便的分割屏幕实现多个进程共用屏幕
- vim 无处不在
  - 浏览器插件 [vimium](https://github.com/philc/vimium) 插件
  - 各种 IDE 都有 vim 插件
- [neovim](https://neovim.io/) | [Github](https://github.com/neovim/neovim)

vim 开源配置

- [SpcaeVim](https://spacevim.org/cn/) | [Github](https://github.com/SpaceVim/SpaceVim)

---

参考资料：

[fatih/vim-go](https://github.com/fatih/vim-go)  
[wiki](https://github.com/fatih/vim-go/wiki)  
[vim-go Tutorial](https://github.com/fatih/vim-go/wiki/Tutorial)  
[fatih/vim-go-tutorial](https://github.com/fatih/vim-go-tutorial)   
[《笨办法学Vimscript》](http://www.treelib.com/book-detail-id-47-aid-2888.html)  
[Practical VIM](https://www.gerardcondon.com/tools-docs/vim/practical-vim/readme.html)
[《PracticalVim》](https://vim-tips.hulin.ink) | [Github](https://github.com/flyingalex/Practical-Vim) | [zh-cn](https://github.com/flyingalex/Practical-Vim/tree/master/tips_cn)
[VimAwesome](https://vimawesome.com)  
[rafi/vim-config](https://github.com/rafi/vim-config)  
[Vim，第三只手](https://juejin.im/post/6889952686930657287)  

# vim 快捷键

![vi-vim-cheat-sheet-sch.gif](./images/vi-vim-cheat-sheet-sch.gif)

来源：http://blog.ngedit.com/vi-vim-cheat-sheet-sch.gif

---

鸣谢：[玩转Vim 从放弃到爱不释手 - 慕课网](https://www.imooc.com/learn/1129)
