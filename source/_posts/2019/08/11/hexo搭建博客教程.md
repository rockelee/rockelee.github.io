---
title: hexo搭建博客教程
date: 2019-08-11 19:00:00
categories: 
- 工具
tags:
- 
---

### 初步环境安装及介绍
- Node.js
- git
- github 创建一个repo， 命名为 username.github.io

Node.js安装好后，创建一个名为`blog`的文件夹， 然后`cd blog`， 运行`hexo init`初始化此目录。 运行`hexo g`生成博客。
然后运行`hexo s`启动 hexo 服务器， 然后在浏览器中输入博客地址， `loalhost:4000`即可看到博客了。

hexo 本质上就是一个markdown解释引擎， 将md文件翻译为静态html文件。
使用的基本流程如下：
- 编写博客
- 生成html网页
- 本地预览
- 上传部署到github

### 常用命令
可能还需要安装其他依赖部件：
- npm install hexo-server --save
  - 安装hexo服务器， 用于本地预览
- npm install hexo-deployer-git --save
  - 安装部署模块， 用于上传到github
- npm install hexo-math --save
  - 渲染公式

常用命令：
- hexo init
- hexo new [layout] file
- hexo g == hexo generate #生成
  - hexo g --watch  # 不但监控文件变动， 一旦有变动， 就更新html文件
  - hexo g --deploy # 生成html文件后， 立马上传到github
  - hexo g -d == hexo g --deploy
- hexo s == hexo server   #启动服务预览
  - hexo server           #Hexo会监视文件变动并自动更新，无须重启服务器
  - hexo server -s        #静态模式
  - hexo server -p 5000   #更改端口
  - hexo server -i 192.168.1.1 #自定义 IP
- hexo d == hexo deploy   #部署
- hexo clean #清除缓存，若是网页正常情况下可以忽略这条命令
- hexo publish [layout] file
  - 草稿箱中的文件移入到source/\_posts目录

基本流程就这么东西， 剩下的就是按照hexo的规则编写文章了。

### 写作环境
hexo常见目录与文件介绍
- node_modules
- themes， 主题
  - \_config.yml
- public
  - 部署到github上的目录，其他目录不会被上传到github上
- package.json
  - 依赖部件， 可以自由移除
- scaffolds
  - 模板文件
- source
  - 资源目录， 比如可以放图片等等
- \_config.yml
  - 配置文件
- 其他都是可以忽略的

一般而言， 只需要配置_config.yml/scaffolds/source即可。
下面只提及一些重要配置。

**_config.yml**
- default_layout: draft
  - 默认生成的博客md文件想入草稿箱
- new_post_name: :year/:month/:day/:title.md
- permalink: :year/:month/:day/:title/
  - hexo new file
  - hexo publish file


**scaffolds**
不同模板文件。 生成md文件时，会预置一些内容在里面，主要用在`hexo new [layout] file`中。如果省略layout选项， 则使用\_config.yml中的default_layout。一般而言， default_layout的值是_draft。编写一般的博客， 使用`hexo new file`，编写好后，`hexo publish file`移入source/\_posts目录

**source**
存放各种博客文件。 主要包括
- \_drafts， 通过 `hexo new draft blogname`生成
  - draft.md
- \_posts， 通过 `hexo new post blogname`生成
  - date/blog.md
- 其他博客， 通过 `hexo new page blogname`生成
  - blogname/index.md
  - 这种形式， 主要用于 博客的 about之类的选项中。

配置以后， 博客的撰写流程一般如下：
- `hexo new filename`， 在source/\_draft目录下生成博客md文件
- 编写好后， 使用`hexo s --draft`预览草稿。
- 确定不在更改以后， `hexo publish filename`
  - 会将博客md文件 移动到 source/\_post/date 目录下
- `hexo g`， 生成html文件
- `hexo d`， 部署到github

其他功能
- 增加类别， 类似于 "machinelearning"， 可以在themes/theme-name/\_config.yml 中的menu中添加"machinelearning: /tags/machinelearning"
  - 然后为 与 machinelearing 相关的博客 打上 machinelearning 的tag
- 增加About， `hexo new page about`， 然后在可以在themes/theme-name/\_config.yml 中的menu中添加"About: /about"
  - 上面旨在说明两种功能的区别， 一个是博客列表， 一个是博客md文件


### 常用markdown语法


### reference
- https://hexo.io/zh-cn/docs/writing