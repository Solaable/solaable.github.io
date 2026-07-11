+++
title="hugo个人博客搭建学习"
date = 2026-06-19T18:27:06+08:00
author = "Sola"
keywords = ["test", ""]
cover = ""
summary = "目标是了解如何在github上搭建一个个人博客，并且会简单的操作来修改它。"
+++

#hugo个人博客搭建  
简单学习一下hugo的基础知识，来为我们修改下载的模板做铺垫。
在学习之前必须要知道的是：
Hugo是由Go编写的快速现代静态网站生成器。
每个 Hugo 项目都是一个目录，其中的子目录贡献于站点的内容、结构、行为和呈现。
##项目结构  
hugo是根据文件目录来渲染出html的，要修改它必须了解它的项目结构。
在创建一个站点时，会自动生成以下目录：   
```
my-site/
├── archetypes/存放了一个文件，用来在创建md文件的时候添加到头部，写了一些创建日期，作者的信息以及一些基础设计。
│   └── default.md
├── assets/包含通常通过资源管道传递的全局资源。包括图片、CSS、Sass、JavaScript 和TypeScript 等资源。
├── content/一般存放要展示的md文件。
├── data/data 目录包含用于增强内容、配置、本地化和导航的数据文件（JSON、TOML、YAML 或 XML）。
├── i18n/语言翻译，用来在多语言时替换网站基础文本。  
├── layouts/包含将内容、数据和资源转换为完整网站的模板。 
├── static/包含在构建站点时将复制到 public 目录的文件，例如 favicon.ico、robots.txt 和用于验证站点拥有权的文件。
├── themes/themes 目录包含一个或多个主题，每个主题位于自己的子目录中。  
└── hugo.toml  包含站点配置，可能分为多个子目录和文件。对于配置较少或不需要在不同环境中以不同方式运行的项目，项目根目录中的单个 hugo.toml 配置文件就足够了。       
```
##安装步骤
一般来说，在hugo官网下载了模板后，根据其的Readme.md即可配置自己的个人博客网站。  
需要着重注意的是archetypes、content、hugo.toml、themes文件夹。  
以我使用的模板为例，我会记录完整安装步骤。  
这里先贴出hugo的[中文文档](https://hugo.opendocs.io/getting-started/)网站  
### 1. 准备工作  
* [安装Hugo](https://hugo.opendocs.io/installation/) 
* [安装Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)  
安装步骤可在各大视频网站搜索。  
### 2. 安装theme模板  
* Init hugo site 创建hugo项目结构  
```bash
hugo new site mysite
cd mysite
```
* Install the theme 克隆主题到目录中  
```bash
git submodule add git@github.com:MeiK2333/github-style.git themes/github-style
```
###3. 根据readme.md来修改文件  
以该主题为例，依照readme.md，修改config.toml文件的配置。  
这样一个基础的hugo项目就完成了，接下来需要为博客添加文章。  
###4. 新建博客文章  
使用命令行在项目目录下运行以下代码来创建文章 ：   
```
hugo new post/title_of_the_post.md
```
使用以下来配置文章信息：  
* summarry 文章简介
```
---
title: "title"
date: 2019-10-22T18:46:47+08:00
draft: false
summary: "The summary content"
---
```
* last modified date 最后修改时间
add to `config.toml`

```toml
lastmod = true

[frontmatter]
  lastmod = ["lastmod", ":fileModTime", ":default"]
```