---
title: VS Code 常用操作
date: 2017-12-01 15:25:17
tags:
  - vscode
---


### 快捷键
* `cmd + shift + V` 打开预览视图（写 md 的时候很方便）
* `cmd + \` 当前文件分屏（文件太长需要跳来跳去看的时候）
* `shift + alt + ↑/↓` 复制当前行到上一行/下一行
* `shift + alt + 鼠标左键` 批量选中文本并编辑

<!-- more -->

---

### 修改文件缩进及格式化
在窗口底栏右侧可选择使用空格还是 tab、每次缩进多少个空格。  
选择后可以 `shift + alt + F` 格式化代码。

---

### 编写 snippets
按 F1 键，选择“首选项：打开用户代码段”  
![](/blog/images/vsc1.png)
选择语言，根据提示编写。  
![](/blog/images/vsc2.png)  

---

### 支持 decorator
用户设置中，`"javascript.implicitProjectConfig.experimentalDecorators": true`  
(上面只是使得 `vs code` 不报错，要真正使用还需要安装相应 `babel` 插件，见 `create-react-app` 一文)

---

### 在非 html 文件里快捷打出 html 元素
1. install `HTML Snippets` extension
2. Go to the extensions folder matching your OS ( `Mac: ~/.vscode/extensions` )
3. Find the extension `abusaidm.html-snippets-x.x.x`
4. Find package.json inside the extension's directory and open it with any text editor, e.g. VSC
5. Locate the sections with snippets and you will see:
```js
{
     "language": "html",
     "path": "./snippets/snippets.json"
}
//Add the below snippet with another language you want.
,{
     "language": "NEW LANGUAGE",
     "path": "./snippets/snippets.json"
}
```
6. Close VSCode and start it again, I have noticed a reload doesn't always work as intended, now the extension should work with the languages you added.
Example of languages: `php`、`javascript`、`javascriptreact`

[参考链接](https://github.com/abusaidm/html-snippets/issues/27#issuecomment-282512411)

---