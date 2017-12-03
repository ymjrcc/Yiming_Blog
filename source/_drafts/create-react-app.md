---
title: create-react-app notes
tags:
---

记录关于 `create-react-app` 的一些骚操作。

<!-- more -->

### 使 CRA 支持 css modules

https://www.npmjs.com/package/react-scripts-cssmodules

`create-react-app my-app --scripts-version react-scripts-cssmodules` 

css 文件需要命名为 `xxx.module.css` 方能解析：     
`import styles from './Button.module.css';`

### 使 CRA 支持 decorators 等新特性

https://www.npmjs.com/package/custom-react-scripts  
(包括 css modules，是上面那个的增强版)

`create-react-app my-app --scripts-version custom-react-scripts`  

修改 `.env` 文件可配置项目。
