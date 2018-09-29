# NPM

官网：
[NPM 官网](https://www.npmjs.com) | 
[NPM 中文社区](https://npm.community)  
文档：
[Documentation](https://docs.npmjs.com) | 
[中文文档](https://www.npmjs.com.cn)  
工具：
[CNPM(TAONPM)](https://npm.taobao.org) | 
[NPM Orgs(公开)](https://www.npmjs.com/features) | 
[npm Enterprise(私有)](https://www.npm-enterprise.com) - 
[文档](https://npme.npmjs.com/docs/)  
搜索：
[UNPKG](https://unpkg.com/#/) | 
[npms](https://npms.io) | 
[nodemodules](http://node-modules.com)  
学习：
[NodeSchool](https://nodeschool.io/zh-cn/)

---
## 1. 安装Node.js和npm

### 1. Mac OS / X或Windows

使用 [Node.js下载页面](https://nodejs.org/zh-cn/download/) 中的一个安装程序。安装标有LTS的版本。其他版本尚未经过npm测试。  

### 2. Linux

选择以下选项之一：  
* 点击 [此处](https://nodejs.org/zh-cn/download/package-manager/) 以许多Linux开发人员喜欢的方式安装npm for Linux
* 滚动 [Node.js下载页面](https://nodejs.org/zh-cn/download/) 上的安装程序
* 检查 [NodeSource的二进制分发](https://github.com/nodesource/distributions) ，看看是否有一个适用于您的系统的更新版本

### 3. 使用版本管理器安装Node.js和npm

由于 npm 和 node.js 产品由不同的实体管理，因此更新和维护可能变得复杂。此外，Node.js 安装过程将 npm 安装在仅具有本地权限的目录中。当您尝试全局运行包时，这可能会导致权限错误。  

为了解决这两个问题，许多开发人员选择使用节点版本管理器或 nvm 来安装 npm。版本管理器将避免权限错误，并将解决更新 Node.js 和 npm 的复杂性。

此外，开发人员可以使用 nvm 在多个版本的 npm 上测试他们的应用程序。nvm 使您可以轻松切换 npm 以及节点版本。这样可以更轻松地确保您的应用程序适用于大多数用户，即使他们使用的是其他版本的 npm。如果您决定安装版本管理器，请使用您选择的版本管理器的说明来学习如何切换版本，并了解如何使用最新版本的 npm 保持最新。  

#### 安装 nvm [Github](https://github.com/creationix/nvm) | [使用](https://github.com/creationix/nvm/blob/master/README.md#usage)

macOS：[nvm for MacOS](https://github.com/creationix/nvm/blob/master/README.md#installation)  
Windows：[nvm-Windowns](https://github.com/coreybutler/nvm-windows)  
Linux：[nvm for Linux](https://github.com/creationix/nvm/blob/master/README.md#installation)  

> 更多信息可在 [此处](https://nodejs.org/zh-cn/download/package-manager/) 查看

## 2. 检查安装是否成功

执行 `node -v` 打印出 Node 版本号则说明 Node 安装成功。  
运行 `npm -v` 打印出 NPM 版本号则说明 NPM 安装成功。  

> 提示：执行命令时可能需要管理员权限才能进行相关操作，你可以在命令前添加 `sudo `，添加管理员权限，本文中所有命令均默认已获得管理员权限，如在使用中提示权限不足请自行添加 `sudo ` 命令。  

在国内由于众所周知的原因，在安装完 NPM 后我们需要安装 [CNPM](https://npm.taobao.org) (可认为 NPM 的中国区镜像) 才能愉快的使用 NPM（CNPM 支持 NPM 除了 `publish` 之外的所有命令）。  

安装 CNPM： `npm install -g cnpm --registry=https://registry.npm.taobao.org`  
在安装完成后就可以使用 `cnpm` 代替 `npm` 命令了。

安装官方最新测试版：`npm install npm@latest -g`  

测试新帐户：`npm login`  
系统将提示您输入用户名，密码和电子邮件。请务必使用与在网站上输入的用户名完全相同的方式拼写您的用户名，否则您将创建一个新帐户。   

测试您是否已成功登录：`npm whoami`  


### 更新

在Linux上更新节点 [NodeSource](https://github.com/nodesource/distributions) 获取最新节点的说明  
在Windows上更新节点 从 <https://nodejs.org/zh-cn/download> 安装最新的msi  
在OSX上更新节点 从 <https://nodejs.org/zh-cn/download> 安装最新的软件包  
或者如果你使用 [homebrew](http://brew.sh/) `brew install node`  

### 一种简单的方法来保持最新  

Node.js有很多版本，它的开发非常活跃。作为管理各种版本的良好实践，我们建议您使用版本管理器来安装Node.js. 有很多很棒的选择，这里有几个：  
* [NVM](https://github.com/creationix/nvm)
* [nodist](https://github.com/marcelklehr/nodist)
* [ñ](https://github.com/tj/n)
* [nave](https://github.com/isaacs/nave)
* [nodebrew](https://github.com/hokaccha/nodebrew)


尝试下一个版本：  
Linux/ Mac IS：`npm install npm@next -g` 或 `npm install -g npm@latest`  
Windows：Microsoft编写了一个小命令行工具来自动执行以下步骤。你可以在[这里](https://github.com/felixrieseberg/npm-windows-upgrade)下载它  

清除 NPM 缓存：`npm cache clean --force`  

### 卸载
`sudo npm uninstall npm -g` 如果失败，请获取npm源代码，并执行以下操作：`sudo make uninstall`  

### 常见错误

只需运行 `npm cache clean` 并再次尝试即可解决一些奇怪的问题。  

`npm install` 如果遇到问题，使用 `-verbose` 选项查看更多详细信息。  

`npm ERR! Error: ENOSPC, write` 您正在尝试安装在没有空间或没有写入权限的驱动器上。 
* 释放一些磁盘空间或
* 将 tmp 文件夹设置在具有更多空间的位置：`npm config set tmp /path/to/big/drive/tmp`
* 自己构建节点并将其安装在可写空间很大的地方。

```shell
npm ERR! not found: git
ENOGIT
```
你需要安装git。或者，您可能需要将您的git信息添加到您的npm配置文件中。您可以[从命令行或从网站](https://docs.npmjs.com/getting-started/modifying_your_profile_from_command_line)执行此操作。

[更多常见错误](https://docs.npmjs.com/troubleshooting/common-errors)  

[NPM 配置](https://docs.npmjs.com/misc/config)  

## 3. CLI命令 [文档](https://docs.npmjs.com/cli/help) 

命令行中的简写
| 简写                   | 完整命令      |
| :-------------------- | :----------- |
| -v                    | --version
| -h, -?, --help, -H    | --usage
| -s, --silent          | --loglevel silent
| -q, --quiet           | --loglevel warn
| -d                    | --loglevel info
| -dd, --verbose        | --loglevel verbose
| -ddd                  | --loglevel silly
| -g                    | --global
| -C                    | --prefix
| -l                    | --long
| -m                    | --message
| -p, --porcelain       | --parseable
| -reg                  | --registry
| -f                    | --force
| -desc                 | --description
| -S                    | --save
| -P                    | --save-prod
| -D                    | --save-dev
| -O                    | --save-optional
| -B                    | --save-bundle
| -E                    | --save-exact
| -y                    | --yes
| -n                    | --yes false
ll and la commands: ls --long

获取帮助 `npm help <term> [<terms..>]`  


`package.json` <https://docs.npmjs.com/files/package.json>  

在安装一个要打包到生产环境的安装包时，你应该使用 `npm install --save`，如果你在安装一个用于开发环境的安装包（例如，linter, 测试库等），你应该使用 `npm install --save-dev`。请在 [npm 文档](https://docs.npmjs.com/cli/install) 中查找更多信息。