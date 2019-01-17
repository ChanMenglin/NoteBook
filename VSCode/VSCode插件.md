# VSCode

[Visual Studio Code 官网](https://code.visualstudio.com)  
[vscode-tips-and-tricks](https://github.com/Microsoft/vscode-tips-and-tricks)  

## 设置

### 1. 设置语言

使用快捷键  
Windows、Linux 快捷键是：ctrl+shift+p  
macOS 快捷键是：command + shift + p  

搜索：`Configure Default Language`  
选择第一条后会打开 `locale.json` 文件  
修改语言设置为 `zh-cn`     
保存对 `locale.json` 文件的修改  
安装插件 [Chinese (Simplified) Language Pack for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-zh-hans) 插件后重启 VSCode 语言就设置成功了。


## 快捷键

[Visual Studio代码的键绑定](https://code.visualstudio.com/docs/getstarted/keybindings#_basic-editing)  
[Basic Editing - Keyboard shortcuts](https://code.visualstudio.com/docs/editor/codebasics#_keyboard-shortcuts)

[VSCode 快捷键 Mac(中文)](https://www.jianshu.com/p/9f50dfc985e2)  
[VSCode for Windows 快捷键(英文)](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf)  
[VSCode for Mac 快捷键(英文)](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)

快捷键映射插件：  
[Visual Studio Keymap](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vs-keybindings)  
[Vim](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim)  
[Sublime Text Keymap and Settings Importer](https://marketplace.visualstudio.com/items?itemName=ms-vscode.sublime-keybindings)  
[Atom Keymap](https://marketplace.visualstudio.com/items?itemName=ms-vscode.atom-keybindings)

### 快捷键（基于 MacOS）

常用快捷键

| 键    | 命令   |
| :---: | :---: |
| ⌘+    | 放大 |
| ⌘-    | 缩小 |
| ^⇧⌘←  | 缩小选择范围 |
| ^⇧⌘→  | 增加选择范围 |
|⇧⌘K    | 删除行 |
| ⇧⌥F   | 格式文档 |
| ⌘K⌘F  | 格式选中文本 |
| ⌥⌘↓   | 在下面插入光标 |
| ⌥⌘↑   | 在上方插入光标 |
| ⌘K⌘C  | 添加行注释 |
| ⌘K⌘U  | 删除行注释 |
| ⌘F    | 查找 |
| ⌥⌘F   | 更换 |
| ⌥⌘C   | 切换查找区分大小写 |
| ⌥↑    | 向上移动行 |
| ⌥↓    | 向下移动行 |
| ⇧⌥↑   | 向上复制行 |
| ⇧⌥↓   | 向下复制行 |
| ⇧⌥↓   | 向下复制行 |
| ⇧⌥推动鼠标 | 左对齐选择 |
| ⇧⌥⌘↑/↓/←/→| 左对齐选择 |

基本编辑

| 键    | 命令  | 命令ID
| :---: | :--: | ----- |
| ⌘X    | 剪切线（空选）| editor.action.clipboardCutAction |
| ⌘C    | 复制行（空选） | editor.action.clipboardCopyAction |
|⇧⌘K    | 删除行 | editor.action.deleteLines |
| ⌘Enter| 在下面插入行 |editor.action.insertLineAfter |
| ⇧⌘Enter | 在上方插入线条 | editor.action.insertLineBefore |
| ⌥↓ | 向下移动线路 | editor.action.moveLinesDownAction |
| ⌥↑ | 向上移动 | editor.action.moveLinesUpAction
| ⇧⌥↓| 复制线下 | editor.action.copyLinesDownAction
| ⇧⌥↑ | 复制排队 | editor.action.copyLinesUpAction
| ⌘D | 添加选择到下一个查找匹配 | editor.action.addSelectionToNextFindMatch
| ⌘K⌘D | 将上一个选择移到下一个查找匹配 | editor.action.moveSelectionToNextFindMatch
| ⌘U | 撤消上一个光标操作 | cursorUndo
| ⇧⌥I | 将光标插入所选每行的末尾 | editor.action.insertCursorAtEndOfEachLineSelected
| ⇧⌘L | 选择所有出现的当前选择 | editor.action.selectHighlights
| ⌘F2 | 选择所有出现的当前单词 | editor.action.changeAll
| ⌘I | 选择当前行 | expandLineSelection
| ⌥⌘↓ | 在下面插入光标 | editor.action.insertCursorBelow
| ⌥⌘↑ | 在上方插入光标 | editor.action.insertCursorAbove
| ⇧⌘\ | 跳转到匹配的括号 | editor.action.jumpToBracket
| ⌘] | 缩进线 | editor.action.indentLines
| ⌘[ | Outdent Line | editor.action.outdentLines
| 家 | 转到行首 | cursorHome
| 结束 | 转到行尾 | cursorEnd
| ⌘↓ | 转到文件结尾 | cursorBottom
| ⌘↑ | 转到文件的开头 | cursorTop
| ^PageDown | 向下滚动线 | scrollLineDown
| ^PageUp | 滚动排队 | scrollLineUp
| ⌘PageDown | 向下滚动页面 | scrollPageDown
| ⌘PageUp | 向上滚动页面 | scrollPageUp
| ⌥⌘[ | 折叠（折叠）区域 | editor.fold
| ⌥⌘] | 展开（uncollapse）区域 | editor.unfold
| ⌘K⌘[ | 折叠（折叠）所有次区域 | editor.foldRecursively
| ⌘K⌘] | 展开（展开）所有子区域 | editor.unfoldRecursively
| ⌘K⌘0 | 折叠（折叠）所有区域 | editor.foldAll
| ⌘K⌘J | 展开（展开）所有区域 | editor.unfoldAll
| ⌘K⌘C | 添加行注释 | editor.action.addCommentLine
| ⌘K⌘U | 删除行注释 | editor.action.removeCommentLine
| ⌘/ | 切换线评论 | editor.action.commentLine
| ⇧⌥A | 切换块注释 | editor.action.blockComment
| ⌘F | 查找 | actions.find
| ⌥⌘F | 更换 | editor.action.startFindReplaceAction
| ⌘G | 找下一个 | editor.action.nextMatchFindAction
| ⇧⌘G | 找到上一个 | editor.action.previousMatchFindAction
| ⌥Enter | 选择查找匹配的所有出现次数 | editor.action.selectAllMatches
| ⌥⌘C | 切换查找区分大小写 | toggleFindCaseSensitive
| ⌥⌘R | 切换查找正则表达式 | toggleFindRegex
| ⌥⌘W | 切换查找整个单词 | toggleFindWholeWord
| ^⇧M | 切换使用Tab键设置焦点 | editor.action.toggleTabFocusMode
| 未分配 | 切换渲染空白 | toggleRenderWhitespace
| ⌥Z | 切换Word Wrap | editor.action.toggleWordWrap

丰富的语言编辑

| 键    | 命令  | 命令ID
| :---: | :--: | ----- |
| ^Space | 触发建议 | editor.action.triggerSuggest
| ⇧⌘Space | 触发参数提示 | editor.action.triggerParameterHints
| ⇧⌥F | 格式文档 | editor.action.formatDocument
| ⌘K⌘F | 格式选择 | editor.action.formatSelection
| F12 | 转到定义 | editor.action.revealDefinition
| ⌘K⌘I | 显示悬停 | editor.action.showHover
| ⌥F12 | 窥视定义 | editor.action.peekDefinition
| ⌘KF12 | 打开定义到一边 | editor.action.revealDefinitionAside
| ⌘。 | 快速解决 | editor.action.quickFix
| ⇧F12 | 窥视参考 | editor.action.referenceSearch.trigger
| F2 | 重命名符号 | editor.action.rename
| ⇧⌘。 | 替换为下一个值 | editor.action.inPlaceReplace.down
| ⇧⌘， | 替换为以前的值 | editor.action.inPlaceReplace.up
| ^⇧⌘→ | 展开AST选择 | editor.action.smartSelect.grow
| ^⇧⌘← | 收缩AST选择 | editor.action.smartSelect.shrink
| ⌘K⌘X | 修剪尾随空格 | editor.action.trimTrailingWhitespace
| ⌘KM | 更改语言模式 | workbench.action.editor.changeLanguageMode


### 设置选中文字大小写切换

```json
{
        "key": "ctrl+shift+u",
        "command": "editor.action.transformToUppercase",
        "when": "editorTextFocus"
    },
    {
        "key": "ctrl+shift+l",
        "command": "editor.action.transformToLowercase",
        "when": "editorTextFocus"
    }
}
```

## VSCode 插件

[插件搜索](https://marketplace.visualstudio.com/vscode)  

[GitHub Pull Requests](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)  

### VSCode 插件（前端）

[vscode 插件和配置推荐（前端开发）](https://github.com/varHarrie/varharrie.github.io/issues/10)  

### VSCode 插件（C#）

| 插件 | 作用 | 作者 |
| --- | :--- | :-: |
| [C#](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) | C# 开发基础，提供智能提示等 | [Microsoft](https://marketplace.visualstudio.com/publishers/Microsoft) |
| [Mono Debug](https://marketplace.visualstudio.com/items?itemName=ms-vscode.mono-debug) | 提供 Debug 功能 | [Microsoft](https://marketplace.visualstudio.com/publishers/Microsoft) |
| [Mono Debug](https://marketplace.visualstudio.com/items?itemName=ms-vscode.mono-debug) | 调试工具 | [Microsoft](https://marketplace.visualstudio.com/publishers/Microsoft) |
| [C# XML Documentation Comments](https://marketplace.visualstudio.com/items?itemName=k--kato.docomment) | 实现和vs一样的xml注释。比如按三下///自动补全 | [Keisuke Kato](https://marketplace.visualstudio.com/items?itemName=k--kato.docomment) |
| [NuGet Package Manager](https://marketplace.visualstudio.com/items?itemName=jmrog.vscode-nuget-package-manager) | 搜索Nuget包并自动向project.json添加 | [jmrog](https://marketplace.visualstudio.com/publishers/jmrog) |



## VSCode 主题

[One Dark Pro](https://marketplace.visualstudio.com/items?itemName=zhuangtongfa.Material-theme#review-details)  
