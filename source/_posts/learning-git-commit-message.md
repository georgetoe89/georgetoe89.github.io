---
title: Learning Git - Commit Message
tags:
  - StudyNotes
  - git
categories:
  - - StudyNotes
    - git
author: George Gu
abbrlink: 6025fbb1
date: 2025-04-28 21:14:32
updated: 2025-04-28 21:14:32
img: https://git-scm.com/images/logo@2x.png
summary:
---

## 编写规范的提交信息

在完成一个代码编写任务之后，需要执行`git commit`命令来提交代码的更改。其中，需要使用`-m`选项来给这一次提交的代码导入提交信息`commit message`。

一个好的commit message能清楚准确的描述这一次提交的代码更改的性质、主题、更改代码的范围、详细的更改描述、更改相关的问题单issue等。而在团队合作的情形下，规范的提交信息可以使团队成员更好地理解每次提交的意图和内容，清晰的知道其他成员提交的内容（以及自己的工作是否收到其影响），并在后续的代码审查、版本跟踪和Bug修复等环节提供帮助。同时，一些用于自动化生成变更日志、版本发布、错误修复跟踪等的工具，也依赖规范的提交信息。

常见的提交信息规范有以下几种：

- Angular 提交信息规范
- Conventional 提交信息规范

### Angular 提交信息规范

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

#### <type> 提交类型

常见的提交类型有：

- Feature: 新功能，常用简写feat
- Bugfix: 修复漏洞，常用简写fix
- Document: 文档，新增/更改代码注释和文档，常用简写doc
- Style: 代码格式变动，不涉及代码运行部分，
- Refactor: 代码重构，处于性能、代码可读性等原因，改写了代码（例如使用新的算法）而不影响上下游接口的改动，常用简写refact
- Test: 测试用例的增加、更新或删除，
- Chore：其他变更（如构建工具、依赖更新等）

#### <scope> 作用域

作用域描述代码更改的影响范围，可选。

#### <subject> 更改主题

更改主题是对本次更改的简短描述，通常不超过 50 个字符，并在一行之内完成，要求简洁、明确。

#### <body> 详细描述

详细描述部分可以更加详细的描述更改内容，包括但不限于：

- 代码更改了哪个文件
- 具体的更改内容
- 为什么更改

此时可以使用多行内容，逐个描述本次的更改。不过出于提交的单一性，建议一次提交只涉及一个主题更改，而在详细描述中，则主要围绕这一主题更改了多个位置的描述而展开

#### <footer> 脚注

其他需要说明的重要信息，例如破坏性更改或关联的 Issue 编号。

### Conventional 提交信息规范

Conventional 提交信息规范与Angular大致相同，具体格式如下

```
<type>[optional scope]: <subject>

[optional body]

[optional footer(s)]
```

也有其他公司形成了各自的规范，但大体上都与上面两种规范接近

## 自动生成/检查提交信息规范的工具

在VSCode或PyCharm中，利用插件可以自动生成规范的提交信息。

另外也有一些工具可以在提交到服务器时检查提交信息是否规范。

TODO: 待补充更多内容