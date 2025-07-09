---
title: 使用Hexo创建静态博客
tags: [StudyNotes, Hexo]
categories:
  - [StudyNotes, Hexo]
abbrlink: 41311
date: 2023-10-14 00:39:28
updated: 2023-10-14 00:39:28
---

## 为什么选择Hexo

一切的开始只是一次头脑发热，想要写一些博客。在因为各种原因排除新浪、CSDN等博客平台后，我把眼光投向了自己搭建博客网站的方向。对比WordPress、Hugo、Jekyll、Hexo等静态网站框架后，结合自己掌握相关知识的程度和自己目前的使用环境，最终选择了Hexo。并选择把该项目托管到GitLab Pages服务。

## 环境准备

根据自己的实际情况选择在Windows上运行Hexo作为日常编辑文章的环境，并且利用Linux的虚拟机来负责调试。关于操作系统的选择不再赘述。

接下来继续安装Hexo依赖的运行环境。Hexo官网[hexo.io](https://hexo.io)和EasyHexo[easyhexo.com](https://easyhexo.com)有完整详细的说明文档。这里重点推荐EasyHexo的[环境安装说明](https://easyhexo.com/1-Hexo-install-and-config/1-2-install-hexo.html)

### 1. Git

后续代码管理的工具，根据OS安装不同版本
- Windows: 前往[Git官网](https://git-scm.com/download/win)下载对应的安装包
- Linux (Ubuntu): 
```commandline
sudo apt-get install git-core
```

### 3. Node.js

Hexo运行的环境，根据OS安装不同版本
- Windows: 前往[nvs](https://github.com/jasongin/nvs/)安装
- Linux (Ubuntu): 前往[nvm](https://github.com/nvm-sh/nvm)安装或前往[NodeSource](https://github.com/nodesource/distributions)安装

### 4. Hexo

完成Node的安装后，可以通过以下命令快捷安装Hexo

```commandline
npm install -g hexo-cli
```

## 准备本地目录

在本地的合适位置建立博客的本地文件夹，并执行以下命令

```commandline
hexo init <folder>
cd <folder>
npm install
```

成功执行完成后，Hexo就算完成在本地的安装了。

安装完成后的本地文件结构，请参考Hexo官网的[建站(中文)](https://hexo.io/zh-cn/docs/setup)部分

## 配置Hexo

简单修改以下Hexo的配置文件`_config.yml`即可快速完成最简单的配置

```yaml
# Site
title:
subtitle:
description:
keywords:
author:
language:
timezone:

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url:
root:
```

其中，Site部分按个人喜好填写即可。在本地调试时，`url`填写http://localhost即可，`root`填写"/"即可。

对Hexo配置文件的详细介绍请参考Hexo官网的[配置(中文)](https://hexo.io/zh-cn/docs/configuration)部分。

了解更多Hexo的配置项以后，可以根据自己的需求逐步更改其余的配置项，这里不再赘述。

## Try it!

在终端执行

```commandline
hexo generate
hexo server
```

然后打开浏览器，输入localhost:4000看看吧

## 安装主题

Hexo默认使用landscape主题。如果对这个主题不满意，可以前往Hexo官网[Themes](https://hexo.io/themes/)挑选自己满意的主题。这里选择了[hexo-theme-matery](https://github.com/blinkfox/hexo-theme-matery)主题。

不同的主题安装方式各有不同，请参考各主题帮助文档。安装完成后，仍有不少Hexo的配置和主题的配置需要修改。请参考各主题的说明文档。

Matery主题的安装和配置描述见其[README.md](https://github.com/blinkfox/hexo-theme-matery#readme)或[README_CN.md](https://github.com/blinkfox/hexo-theme-matery/blob/develop/README_CN.md)

## 安装插件

Hexo和主题都可以通过插件增加功能，比如本地搜索、字数和访问统计、音乐和视频播放等功能。

以下为本站使用的插件

### 1. 本地搜索

给博客添加本地搜索功能需要search插件

1. 安装

```commandline
npm install hexo-generator-search --save
``` 

2. 修改配置

修改Hexo配置文件`_config.yml`，添加以下内容：

```yaml
search:
  path: search.xml
  field: post
```

安装完成后清理重启Hexo即可在博客中使用搜索功能

### 2. 文章永久链接

修改文章默认的永久链接形式。

1. 安装

```commandline
npm install hexo-abbrlink --save
```

2. 修改配置

修改Hexo配置文件`_config.yml`

```yaml
# permalink: :year/:month/:day/:title/
# permalink_defaults:
permalink: posts/:abbrlink.html
abbrlink:
  alg: crc32  # 算法：crc16(default) and crc32
  rep: hex    # 进制：dec(default) and hex
```

安装完成后清理重启Hexo，这时文章链接已经完成修改，变成上述配置的以CRC32的hex形式。

### 3. 文章字数统计

给文章添加字数统计、阅读时长信息。

1. 安装

```commandline
npm install hexo-wordcount --save
```

2. 修改配置

修改Matery主题配置文件`/themes/<matery路径>/_config.yml`，根据自己的需要激活对应的选项

```yaml
postInfo:
  date: true
  update: false
  wordCount: false # 设置文章字数统计为 true.
  totalCount: false # 设置站点文章总字数统计为 true.
  min2read: false # 阅读时长.
  readCount: false # 阅读次数.
```

安装完成后清理重启Hexo即可在文章上部显示相关内容。

## 部署

完成建站、本地调试以后，就可以选择部署到远程服务器。这一步的完整操作请参考Hexo官网的[一键部署](https://hexo.io/zh-cn/docs/one-command-deployment)部分

如果你的远程服务来自于Github Pages或GitLab Pages，Hexo官网也有相关说明。这里不再赘述。

- [Github Pages](https://hexo.io/zh-cn/docs/github-pages)
- [GitLab Pages](https://hexo.io/zh-cn/docs/gitlab-pages.html)



## 相关文章

## Reference

- Hexo官网: [hexo.io](https://hexo.io)
- Hexo中文官网: [hexo.io/zh-cn](https://hexo.io/zh-cn)
- EasyHexo: [Easy Hexo](https://easyhexo.com/)
- 斯莫笔记: [Hexo搭建静态博客（一）——基础搭建](https://small-rose.github.io/posts/9f117b.html)