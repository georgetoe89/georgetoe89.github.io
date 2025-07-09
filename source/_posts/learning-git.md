---
title: Learning Git
tags:
  - StudyNotes
  - git
categories:
  - - StudyNotes
    - git
author: George Gu
abbrlink: 687c80d3
date: 2023-10-19 21:58:02
updated: 2023-10-24 21:15:02
img: https://git-scm.com/images/logo@2x.png
summary:
---

## 版本管理

### Version Control

> 版本控制，也称为源代码控制，是一种跟踪和管理软件代码变更的实践。版本控制系统是软件工具，可帮助软件团队管理源代码随时间推移而发生的变更。
>  
> 版本控制软件在特殊类型的数据库中跟踪对代码的每一次修改。如果犯了错误，开发人员可以回退并比较代码的早期版本，以帮助修复错误，同时最大限度地减少对所有团队成员的干扰。

Reference:

- [What is Version Control](https://www.atlassian.com/zh/git/tutorials/what-is-version-control)

常见版本控制软件：

|Software|Network Architecture|Conflict Resolution|Development Status|
|---|---|---|---|
|Git|Distributed|Merge|Active|
|Mercurial|Distributed|Merge|Active|
|SVN|Client-Server|Merge or Lock|Active|
|CVS|Client-Server|Merge|Maintenance only|

### What is Git

> 到目前为止，当今世界上使用最广泛的现代版本控制系统是 Git。
> 
> Git 采用分布式架构，是 DVCS（分布式版本控制系统）的示例。在 Git 中，每个开发人员的代码工作副本也是一个可以包含所有变更完整历史记录的存储库，而不是像曾经流行的 CVS 或 Subversion（也称为 SVN）等版本控制系统那样，只有一个地方存放软件的完整版本历史记录。
> 
> Git 的设计考虑了:
> 1. 分布式
> 2. 性能
> 3. 安全性
> 4. 灵活性

Reference: 
- [What is Git](https://www.atlassian.com/zh/git/tutorials/what-is-git)

## 安装Git

### Windows

1. 下载安装程序[Git for Windows 安装程序](https://git-for-windows.github.io/)

2. 执行安装程序

### Linux

Debian系（包括Ubuntu）可以使用apt-get安装

```commandline
sudo apt-get update
sudo apt-get install git
```

通过`git --version`来验证安装是否完成：

```commandline
git --version
```

如果显示
```commandline
git version x.x.x
```
即安装成功，`x.x.x`即为实际安装的Git版本

### 基本配置

完成Git安装后建议立刻配置一些基础信息：

```commandline
git config --global user.name <你的名字>
git config --global user.email <你的邮箱>
```

如果你已经注册了Github或其他在线代码托管平台，这里的名字和邮箱需要与注册的信息保持一致

## 使用Git

### 配置代码库

#### 初始化新代码库: git init

使用`git init`来创建新的代码库。执行此命令将在您当前工作目录中创建一个新的`.git`子目录。这也将创建一个新的主分支。

假如已经有一个现有项目文件夹，要将其配置成代码库，那么首先使用`cd`命令定位到该项目文件夹，然后执行`git init`

```commandline
cd /path/to/your/existing/code
git init
```

如果在使用`git init`命令时带了参数：
```commandline
git init <repo name>
```

那将在当前目录下创建Repo的项目文件夹`repo name`，并将项目文件夹配置成代码库

#### 克隆远程代码库

如果已在远程代码库（如Github、GitLab等）中设置了项目，或者需要从其他开发者的远程项目复制，那么应该使用`git clone`命令。

```commandline
git clone <url to remote git repo>
```

该命令将克隆url所指向的repo到本地，并保存于本地的项目同名目录下。通常应该在执行`git clone`命令前，先使用`cd`命令将当前工作目录指定到期望的项目目录。

若想在克隆时指定目标目录，那么执行命令

```commandline
git clone <url to remote git repo> <target directory>
```

### 编辑和保存变更

编辑或更改了本地的代码库中的内容（代码、文档等）后，应当向代码库提交更改以保存变更。

首先使用`git add`命令将变更的内容保存到暂存区。

```commandline
git add <file>  # 保存指定文件到暂存区
git add --all  # 将所有变更的文件保存到暂存区
```

然后使用`git commit`命令提交保存变更。

```commandline
git commit -m <commit message>  # commit message 记录变更说明等信息
```

### 向远程代码库推送变更，从远程代码库获得更新

`git push`命令用于向远程代码库推送本地代码库的变更。推送后，其他与之合作开发的开发者将能获得这些变更。

`git pull`命令用于将远程代码库的更新拉取到本地代码库。

当本地代码库使用`git clone`创建时，该代码库的远程代码库信息已经被自动配置。如果是使用`git init`创建的本地代码库，需要配置远程代码库：

```commandline
git remote add <remote_name> <remote_repo_url> 
```

参数`remote_name`一般为`origin`。也可以根据需要配置成`remote`等其他便于识别的名称。

### 配置和设置

前面已经提到，安装Git后建议立即配置一些基础信息。

```commandline
git config --global user.name <你的名字>
git config --global user.email <你的邮箱>
```

其中`--global`选项指定这些配置将应用于全局。
如果只想更改当前代码库的配置，请在指定工作目录为当前代码库的前提下，将上述命令中的`--global`选项改为`--local`

其他设置，如指定文本编辑器，请参考 [git config help文档](https://git-scm.com/docs/git-config) 进行编辑。

git共有3个不同的配置变量存储位置，分别是：

1. /etc/gitconfig文件，是系统上每一个用户的通用配置。使用`git config --system`命令来修改其中的内容。
2. ~/.gitconfig文件，针对当前用户的通用配置。使用`git config --global`命令来修改其中的内容。
3. 代码库目录中.git/config文件，针对当前代码库的配置项。使用`git config --local`命令来修改其中的内容。

这三个位置的配置优先级依次提高，也就是说下面（如`local`）的配置将覆盖前面的配置（如`global`）。

## Git设计思路

### 工作目录、暂存区和代码库

基本的Git工作流程如下：

1. 在工作区中修改文件。
2. 将你想要下次提交的更改选择性地暂存，这样只会将更改的部分添加到暂存区。
3. 提交更新，找到暂存区的文件，将快照永久性存储到代码库。
4. 如果在修改文件过程中想要将当前的更改应用到其他分支中，那么不暂存这些更改而切换分支，将在切换后的分支中看到这些更改。原来的分支因为没有提交而未更改。

如果代码库中保存着特定版本的文件，就属于`已提交`状态。 如果文件已修改并放入暂存区，就属于`已暂存`状态。 如果自上次检出后，作了修改但还没有放到暂存区域，就是`已修改`状态。

![Working directory, stage area and repository](https://git-scm.com/images/about/index1@2x.png)
![Working directory, stage area and repository](https://git-scm.com/book/en/v2/images/areas.png)

Reference: 
- [What is Git](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F)

### 分支

Git的分支，其本质上仅仅是指向提交对象的可变指针。

例如在master分支的基础上，创建一个testing分支：
```commandline
git branch testing
```
此时两个分支都指向同一个提交。
![两个指向相同提交历史的分支](https://git-scm.com/book/en/v2/images/head-to-master.png "两个指向相同提交历史的分支")

Git拥有一个特殊的指针`HEAD`来描述当前所在的本地分支。

使用`git checkout`命令来切换分支。
```commandline
git checkout testing
```

在testing分支下做一些更改并提交，HEAD指针将随之指向新的提交。

![HEAD 分支随着提交操作自动向前移动](https://git-scm.com/book/en/v2/images/advance-testing.png "HEAD 分支随着提交操作自动向前移动")

此时如果切换回master分支，并在master分支更改、提交，那么这个项目将形成分叉（diverged）

![项目分叉历史](https://git-scm.com/book/en/v2/images/advance-master.png "项目分叉历史")

> Note: 分支切换会改变你工作目录中的文件
> 
>> 在切换分支时，一定要注意你工作目录里的文件会被改变。 如果是切换到一个较旧的分支，你的工作目录会恢复到该分支最后一次提交时的样子。 如果 Git 不能干净利落地完成这个任务，它将禁止切换分支。

Reference: 
- [Git分支简介](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%AE%80%E4%BB%8B)
- [Branches in a Nutshell](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)

### 合并或变基

#### 合并 Merge

如上面的例子，在代码编写过程中经常会遇到分叉。当分叉的项目开发完（或者开发到某个节点），需要将分叉的两个分支合并起来，那就需要将项目的两个（或多个）分支合并。

```commandline
git checkout <master>  # 切换到你想合并到的分支，也是后续将保留的分支
git merge <hotfix>  # 选择需要合并的分支
```

![将Hotfix合并到Master](https://git-scm.com/book/en/v2/images/basic-branching-5.png)

当Hotfix被合并后，可以删除该分支。

然后切换到先前的工作分支`iss53`继续工作。当`iss53`的工作也完成了，那么我们又需要将该分支的工作合并到master：

```commandline
git checkout <master>  # 切换到你想合并到的分支，也是后续将保留的分支
git merge <iss53>  # 选择需要合并的分支
```

![一次典型合并中所用到的三个快照](https://git-scm.com/book/en/v2/images/basic-merging-1.png "一次典型合并中所用到的三个快照")

这种典型的分支合并，将在合并完成后自动形成一个新的提交，以记录这次合并。合并后，我们的提交记录看起来会是：

![一个合并提交](https://git-scm.com/book/en/v2/images/basic-merging-2.png "一个合并提交")

通常来说，经过一段时间的开发，当打算与其他分支合并时，往往会遇到冲突：同一个文件在不同分支下被执行了不同的修改。这个时候的合并需要首先解决冲突，然后再继续执行合并。

如何高效的使用分支管理工作流，请参考 [Branching Workflows](https://git-scm.com/book/en/v2/Git-Branching-Branching-Workflows) [分支开发工作流](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E5%BC%80%E5%8F%91%E5%B7%A5%E4%BD%9C%E6%B5%81)

#### 变基 Rebase

除了合并Merge，变基Rebase也是一种常用的整合分支的方法。假如我们现在有如下的提交历史：

![分叉的提交历史](https://git-scm.com/book/en/v2/images/basic-rebase-1.png "分叉的提交历史")

通过`git merge`命令来进行代码合并的效果如下：

![通过合并操作来整合分叉的历史](https://git-scm.com/book/en/v2/images/basic-rebase-2.png "通过合并操作来整合分叉的历史")

而

> 其实，还有一种方法：你可以提取在 C4 中引入的补丁和修改，然后在 C3 的基础上应用一次。 在 Git 中，这种操作就叫做 变基（rebase）。 你可以使用 rebase 命令将提交到某一分支上的所有修改都移至另一分支上，就好像“重新播放”一样。

在这个例子中，你可以检出 experiment 分支，然后将它变基到 master 分支上：

```commandline
git checkout experiment
git rebase master
```

> 它的原理是首先找到这两个分支（即当前分支 experiment、变基操作的目标基底分支 master） 的最近共同祖先 C2，然后对比当前分支相对于该祖先的历次提交，提取相应的修改并存为临时文件， 然后将当前分支指向目标基底 C3, 最后以此将之前另存为临时文件的修改依序应用。

现在回到 master 分支，进行一次快进合并

```commandline
git checkout master
git merge experiment
```

![master 分支的快进合并](https://git-scm.com/book/en/v2/images/basic-rebase-4.png "master 分支的快进合并")

#### Merge or Rebase

什么时候应该用merge，什么时候应该用rebase呢？

> 如果提交存在于你的仓库之外，而别人可能基于这些提交进行开发，那么不要执行变基
> 
> 总的原则是，只对尚未推送或分享给别人的本地修改执行变基操作清理历史， 从不对已推送至别处的提交执行变基操作，这样，你才能享受到两种方式带来的便利。

而StackOverflow上的这个回答，可以看到大家的讨论：

[When do you use Git rebase instead of Git merge?](https://stackoverflow.com/questions/804115/when-do-you-use-git-rebase-instead-of-git-merge)

总结来说

- 如果你的代码库只有你一个开发者，平时更多处于单线工作状态（在一个分支上完成工作以后才切换到另一个分支继续工作），那么Rebase和Merge都可以。此时Rebase会给你留下更简单的提交记录。如果你更倾向于保留更原汁原味的提交记录，那么Merge更合适。

- 如果你的代码库有多人合作开发，会定期将大家的工作都合并到一起，或者你的代码库已经推送出去，那么Merge更合适。

Reference: 

- [Branching Workflows](https://git-scm.com/book/en/v2/Git-Branching-Branching-Workflows)
- [分支开发工作流](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E5%BC%80%E5%8F%91%E5%B7%A5%E4%BD%9C%E6%B5%81)

- [When do you use Git rebase instead of Git merge?](https://stackoverflow.com/questions/804115/when-do-you-use-git-rebase-instead-of-git-merge)

### gitignore

项目中一些不需要通过Git管理的文件，比如日志、大批量的测试数据等，可以通过`.gitignore`文件来指定。已经被Git追踪的文件不会受.gitignore的影响，因此应当在提交前留意当前暂存区的新文件，确保不需git管理的文件被添加到.gitignore中。

.gitignore文件可以保存于项目根目录下，以对整个项目生效。也可以放置于某个特定的目录下，此时将只对该目录以及其子目录生效。

.gitignore文件中的每一行均代表一个文件名的正则表达式。

- 空行不匹配任何文件
- 行开头的"`#`"表示注释
- "` \ `" 反斜杠表示转义
- "`!`" 表示排除。先前排除的文件将再次包含在内
- "`/`" 作为文件夹分隔符
- 行如果以"`/`"结尾，将仅匹配文件夹
- "`*`"为通配符，可以匹配任意字符
- "`?`"为通配符，可以匹配任意一个字符
- "`**`"为通配符，在路径匹配中起作用：
    - 前导"`**`"后跟斜杠表示在所有目录中匹配
    - 结尾的"`/**`"匹配里面的所有内容
    - 斜杠后跟两个连续的星号，然后斜杠，"`/**/`"，匹配零个或多个目录

一个常见的.gitignore文件内容举例：

```
.git/
target/
out/
=======
# compiled output
**/dist*
**/build*
**egg-info
*/node_modules*.\ve

# pycache
*__pycache__*

# Logs
logs
*.log

# IDEs and editors
.idea/*
.idea
.project
.classpath
.c9/
*.launch
.settings/
*.sublime-workspace
.ipynb_checkpoints
.jupyter

# IDE - VSCode
.vscode/*
.vscode/settings.json
!.vscode/tasks.json.idea/
!.vscode/tasks.json
!.vscode/launch.json
!.vscode/extensions.json

# tmp code
**/tmp*
**/temp*
././tmp*

```

## Reference

- [Git](https://git-scm.com/)
- [Git - Reference](https://git-scm.com/docs)
- [Git - Book](https://git-scm.com/book/en/v2)
- [Git - Book中文](https://git-scm.com/book/zh/v2)
- [ATLASSIAN Git Tutorials](https://www.atlassian.com/git/tutorials)
- [ATLASSIAN Git 教程](https://www.atlassian.com/zh/git/tutorials)