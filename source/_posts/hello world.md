---
title: hello world
date: 2017-11-29 10:36:10
tags:
  - 杂
  - hexo
---
距离上次开博客已经两年多了，两年前在 github-pages 上用 jekyll 搭了一个简易的博客，然而懒癌晚期写了三篇就无疾而终。<del>时隔两年，我变秃了，也变强了！</del>在学习和工作的过程中，觉得有一个载体来记录和总结自己的思考和成长过程还是必须的。之前一直用 OneNote 做笔记，但换了 Mac 后发现很多功能都不支持了，心想还是博客方便，故决心重开一个。

<!-- more -->

昨天简单调研了一下几个受欢迎的博客框架，然后就被 [hexo](https://github.com/hexojs/hexo) 所深深吸引了，安装配置简单灵活，还有各种好看的主题……就决定是你了！主题用的是 hexo 社区最受欢迎的 [NexT](https://github.com/iissnan/hexo-theme-next)。

粗略浏览了一遍文档后就开撸。搭好环境测试了一下没问题，我把原先的GitHub 上的博客仓库改了个名字扔到一边，替换成了现在这个。新增了两个仓库：

* [Yiming_Blog](https://github.com/ymjrcc/Yiming_Blog)：这是博客脚手架仓库，包括本地环境、主题、各种配置以及 md 格式的博文等。  
* [blog](https://github.com/ymjrcc/blog)：这是上面那个项目自动生成部署的静态博客站点源码，在 Yiming_Blog 中配置好后，用 markdown 写完博客，在项目根目录直接执行 `hexo g -d` 命令，就能生成相应的静态页面，一键发布到我的 github-pages 上，通过 [这个链接](https://ymjrcc.github.io/blog/) 即可访问。

博客的大部分配置通过修改项目中的 `_config.yml` 文件来实现。与博客框架相关的配置文件在根目录下，与主题相关的配置文件在 `theme` 文件夹对应的主题文件夹里。具体参考 [hexo 官方文档](https://hexo.io/zh-cn/docs/) 、[NexT 官方文档](http://theme-next.iissnan.com/) 。

在生成 GitHub 仓库时遇到一个问题。由于 NexT 主题我是 `git clone` 到 `theme` 文件夹里的，所以它本身就是一个 git 仓库，而 `Yiming_Blog` 也是一个 git 仓库，于是就形成了大仓库嵌套小仓库的现象。这会导致小仓库里的改动无法被大仓库捕获。于是我把小仓库的 `.git` 文件夹删除了，使其恢复为普通文件夹，与大仓库融为一体。虽然这样做对将来主题版本更新不是很方便，但考虑到主题版本也不会经常更新，就先这样吧。以后如果要更新主题版本，记得先把 `_config.yml` 备份一下就好。

好了，暂时先交代这么多吧。希望这次可以坚持久一点，做到笔耕不辍，在持续总结中不断提高自己的姿势水平！

---

hexo 常用操作：
* `hexo new <title>`        //写新文章
* `hexo new draft <title>`  //建立草稿
* `hexo publish <title>`    //发布草稿
* `hexo s`                  //本地运行
* `hexo s --draft`          //本地预览草稿
* `hexo clean`              //清除缓存
* `hexo g -d`               //生成静态文件并部署到服务器

hexo 中引入图片等资源：
1. 将资源文件放在 `source` 文件夹下对应的文件夹里
2. 在文章中用 md 语法引入：
  * 在根目录下：`![](/images/img1.jpg)` 
  * 在子目录`/path`下：`![](/path/images/img2.jpg)`  
(若博客放在网站子目录下，如`www.mywebsite.com/blog`，记得图片路径前也要加上子目录，否则无法解析！)