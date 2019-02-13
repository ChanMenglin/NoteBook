---
title: Markdown 语法
date: 2018-08-29 08:42:00 +0800
categories: Markdown 语法
---

# Markdown 语法

本文的写作目的：相信现在有很多人都在使用 Markdown ，但目前 Markdown 的语法支持及说明都不好，因此在本文中归纳整理了一些被广泛支持的 Markdown 语法，如有遗落或错误请各位指正，欢迎补充。

## 1. 标题

```test
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```

效果如下：

# 一级标题

## 二级标题

### 三级标题

#### 四级标题

##### 五级标题

###### 六级标题

> 最多到六级标题

## 2. 文字

### 2.1 加粗

```test
粗体：**粗体** 或 __粗体__
```

粗体：**粗体** 或 __粗体__
> 符号中的内容可换行，可包含空格

### 2.2 斜体

```test
斜体：*斜体* 或 _斜体_
```

斜体：*斜体* 或 _斜体_
> 符号中的内容可换行，可包含空格

### 2.3 删除线

```test
~~要划除的行内内容~~
```

~~要划除的行内内容~~

### 2.4 字体、字号、颜色

Markdown 没有原生设置字体、字号、颜色的方法，我们可以使用 **行内HTML**（下文会讲）实现，

```test
字体：<font face="黑体">黑体字</font>
字号：<font size="10">10号字</font>
颜色：<font color=#ff0000>红色字</font>
```

字体：<font face="黑体">黑体字</font>  
字号：<font size="5">5号字</font>  
颜色：<font color=#ff0000>红色字</font>  
> ```face```、```size```、```color```分别用来设置字体的 字体、字号 和 颜色

### 2.5 下划线

Markdown 没有原生下划线标记，我们可以使用 **行内HTML**（下文会讲）实现，共两种方式。  

**方法一**  

```html
<u>Underlined Text</u>
```

<u>Underlined Text</u>  

**方法二**  

```html
<span style="border-bottom:2px dashed yellow;">Underlined Text</span>
```

<span style="border-bottom:1px dashed;">Underlined Text</span>
> ```style``` 中的样式可自由定制  

> 方案1：快速添加下划线，但 ```u``` 标签的下划线自定义程度低，
>
> 方案2（推荐）：由于方案1的不完美，因此我个人建议可以使用 ```html``` 的 ```span``` 标签、设置行内 ```CSS``` 样式，如 ```border-bottom``` 来添加下划线。这种方式自定义程度最高。

## 3. 排版

### 3.1 链接

```test
行内式：
[链接名](链接地址“标题”)
[百度](https://www.baidu.com)

参考式：
[链接名](识别链接的标记)

[百度1]

[百度1]: https://www.baidu.com
```

[链接名](链接地址“标题”)
[百度](https://www.baidu.com)

[百度1]

[百度1]: https://www.baidu.com

> 如果链接名与链接地址一致则可以这样写：<链接地址>,链接地址会直接显示在页面上(电子邮件地址也可以使用这种方式展示)
<https://www.baidu.com>

### 3.2 图片

```test
![图片加载失败时显示的文字](图片地址,支持相对路径及网络地址)
```

### 3.3 列表

**有序列表**
使用数字和点表示有序列表。

```test
1. 有序列表一
2. 有序列表二
3. 有序列表三
```

1. 有序列表一
2. 有序列表二
3. 有序列表三

**无序列表**
使用 *，+，- 表示无序列表(三者选其一)。

```test
* 无序列表*
+ 无序列表+
- 无序列表-
```

* 无序列表*
+ 无序列表+
- 无序列表-

> 以上为了演示同时使用了三种标记，实际使用时同一个列表应使用相同的标记

**列表嵌套**  

```test
- 1. 第一个序列第一项
   - 1. 第二个序列第一项
   - 2. 第二个序列第二项
- 2. 第一个序列第二项
```

- 1. 第一个序列第一项
    - 1. 第二个序列第一项
    - 2. 第二个序列第二项
- 2. 第一个序列第二项

> 关于列表嵌套，实现方法较多，可自行探究  
> 
> 注意：无论是有序列表还是无序列表，文字与前面的符号之间一定要有一个空格

### 3.4 引用

使用 ```>``` 表示文字引用，本文多用做说明，建议在使用时在 ```>``` 后加一个空格，便于阅读

### 3.5 代码块

**行内代码块**
使用 `` 代表行内代码块

```test
`public static void...`
```

`public static void...`  
**代码块**

```test
    public static void...
```

    public static void...

> 前方有四个空格

本人习惯于使用 ``` ``` 代表块级代码

```html
<a>这是HTML 的 a 标签</a>
```

> 开始的 ``` 后可紧跟着添加代码块中代码的语言，一些编辑器会根据此标记对代码进行高亮处理，便于阅读。

| 名称	             | 关键字	                   | 说明
| :---------------- | :------------------------- | :------------------- |
| AppleScript       |	applescript              |    	
| ActionScript 3.0  |	actionscript3 , as3      |
| ColdFusion	    |   coldfusion , cf	         |	
| C	                |   cpp , c                  |
| C#	            |   c# , c-sharp , csharp    |
| CSS	            |   css	                     |
| Delphi            |	delphi , pascal , pas    |
| diff&patch        |	diff patch	             | 用代码版本库时,遇到代码冲突,其语法就是这个
| Dockerfile        | Dockerfile                 | Docker 容器
| Erlang            |	erl , erlang	         |
| Groovy            |	groovy	                 |
| Java              |	java	                 |
| JavaFX            |	jfx , javafx	         |
| JavaScript	    |   js , jscript , javascript|
| Perl              |	perl , pl , Perl	     |
| PHP	            |   php	                     |
| text	            |   text , plain	         | 就是普通文本
| Python	        |   py , python	             |
| Ruby	            |   ruby , rails , ror , rb  |
| Shell             |	bash , shell             |
| SASS&SCSS	        |   sass , scss	             |
| Scala	            |   scala	                 |
| SQL	            |   sql	                     |
| Visual Basic	    |   vb , vbnet	             |
| XML	            |   xml , xhtml , xslt , html|
| Objective C	    |   objc , obj-c	         |
| F#	            |   f# f-sharp , fsharp	     |
|                   |	xpp , dynamics-xpp	     |
| R	                |   r , s , splus	         |
| matlab            |	matlab	                 |
| swift	            |   swift	                 |
| GO	            |   go , golang	             |
| yml               |   yml                      | yml 文件格式

### 3.6 换行

Markdown中的换行需在要换行的内容的前一行的末尾加两个空格再回车，只敲回车是不会换行的。

### 3.7 分割线

在一行中用 **三个以上** 的星号、减号、底线来建立一个分隔线，行内不能有其他东西。你也可以在星号或是减号中间插入空格

```test
***
* * *
- - -
---------------------------------------
```

***
* * *
- - -
---------------------------------------

### 3.8 段落

**缩进、空格**
Markdown 的段落定义是由一个或多个连续的文本组成，中间的多个空格和 tab 会被认为是一个空格

```test
半方大的空白&ensp;或&#8194;结束  
全方大的空白&emsp;或&#8195;结束  
不断行的空白格&nbsp;或&#160;结束  
```

半方大的空白&ensp;或&#8194;结束  
全方大的空白&emsp;或&#8195;结束  
不断行的空白格&nbsp;或&#160;结束  

### 3.9 表格

```test
| Item      |    Value | Qty  |
| :-------- | --------:| :--: |
| Computer  | 1600 USD |  5   |
| Phone     |   12 USD |  12  |
| Pipe      |    1 USD | 234  |
```

| Item      |    Value | Qty  |
| :-------- | --------:| :--: |
| Computer  | 1600 USD |  5   |
| Phone     |   12 USD |  12  |
| Pipe      |    1 USD | 234  |

### 3.10 脚注(部分支持)

Footnote 1 link[^first].  
[^1]: This is a footnote  
[^label]: A footnote on "label"  
[^!DEF]: The definition of a footnote.  

### 3.11 Tasklist(部分支持)

```test
- [ ] Task no-checked
- [x] Task checked
```

- [ ] Task no-checked
- [x] Task checked

st->op->cond
cond(yes)->e
cond(no)->op

### 3.11 注释

```test
<!-- 这段话会被注释 -->
```

<!-- 这段话会被注释 -->

## 4. 转义字符

`\\` - \\ 反斜杠  
`\` - \` 反引号  
`\*` - \* 星号  
`\_` - \_ 下划线  
`\{\}` - \{\} 大括号  
`\[\]` - \[\] 中括号  
`\(\)` - \(\) 小括号  
`\#` - \# 井号  
`\+` - \+ 加号  
`\-` - \- 减号  
`\.` - \. 英文句号  
`\!` - \! 感叹号  
> 在转义的字符前加 ```\```

---

> 参考链接  
> <https://www.zybuluo.com/xxliixin1993/note/125827#2分级标题>  
> <https://www.zhihu.com/question/28375977>  
> <https://blog.csdn.net/u011419965/article/details/50536937>  
> <https://www.appinn.com/markdown/#overview>    
> <https://www.w3cschool.cn/markdownyfsm/cbx1e7.html>

