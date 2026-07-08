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
├── archetypes/
│   └── default.md
├── assets/
├── content/
├── data/
├── i18n/
├── layouts/
├── static/
├── themes/
└── hugo.toml         <-- 站点配置
```
每个子目录都贡献于站点的内容、结构、行为或呈现。  
####archetypes  
简单来说就是存放了一个文件，用来在创建md文件的时候添加到头部，写了一些创建日期，作者的信息以及一些基础设计。
####assets
assets 目录包含通常通过资源管道传递的全局资源。包括图片、CSS、Sass、JavaScript 和 TypeScript 等资源。
####config(.toml文件)
config 目录包含站点配置，可能分为多个子目录和文件。对于配置较少或不需要在不同环境中以不同方式运行的项目，项目根目录中的单个 hugo.toml 配置文件就足够了。
####content
content 目录包含组成站点内容的标记文件（通常是 markdown）和页面资源。详见 详情.
####data
data 目录包含用于增强内容、配置、本地化和导航的数据文件（JSON、TOML、YAML 或 XML）。详见 详情.
####i18n
i18n 目录包含多语言站点的翻译表。详见 详情.
####layouts
layouts 目录包含将内容、数据和资源转换为完整网站的模板。详见 详情.
####public
public 目录包含发布的网站，在运行 hugo 命令时生成。Hugo 根据需要重建此目录及其内容。详见 详情.
####resources
resources 目录包含 Hugo 资源管道的缓存输出，在运行 hugo 或 hugo server 命令时生成。默认情况下，此缓存目录包括 CSS 和图片。Hugo 根据需要重建此目录及其内容。
####static
static 目录包含在构建站点时将复制到 public 目录的文件，例如 favicon.ico、robots.txt 和用于验证站点拥有权的文件。在引入 页面包 和 资源管道 之前，static 目录也用于存放图片、CSS 和 JavaScript 等资源。详见 详情.
####themes
themes 目录包含一个或多个主题，每个主题位于自己的子目录中。