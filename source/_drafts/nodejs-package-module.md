---
title: Node.js 包与模块机制
tags:
  - nodejs
---
`CommonJS` 对模块遵循三个约定：`require`、模块上下文、模块标识。

<!-- more -->

* `const blahblah = require("boom_shakalaka");`
* 模块上下文：`require` 函数、`exports` 对象、`module` 对象
* 模块标识其实就是一个字符串，用于传给 require 函数的

目录寻径依次解析文件夹下的 `index.js`、 `index.json`、 `index.node` 文件，但若文件夹下有 `package.json` 文件且里面包含 `main` 字段，则会首先寻找 `main` 字段指定的文件。

`https://github.com/expressjs/express/blob/master/lib/response.js` 可通过 `const Resp = require("express/lib/response");` 这种方式直接加载进来。

`CommonJS` 包描述文件：`package.json`（与 `Node.js` 中的不太一样）

`package.json` 包含的必填字段如图。

![](/blog/images/node-package-module1.jpg)

`package.json` 包含的选填字段如图。

![](/blog/images/node-package-module2.jpg)

其他自定义字段会被 `CommonJS` 规范忽略掉。

一个遵循 CommonJS 规范的包会有如下的一个目录呈现： 
 
* package.json 在根目录；
* 二进制文件应当在 bin 目录下；
* JavaScript 源码应当在 lib 目录下；
* 文档应当在 doc 目录下；
* 单元测试文件应当在 test 目录下。

`npm` 对 `package.json` 的依赖比较强，相对而言 `Node.js` 更依赖于 `node_modules` 目录。`npm` 只是 `Node.js` 中的一种包管理机制，其他还有 `cnpm`、`yarn` 等。

`npm` 的 `package.json` 与 `CommonJS` 的 `package.json` 的异同：

![](/blog/images/node-package-module3.jpg)
