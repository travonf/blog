---
title: 多人开发必备Git技能
date: 2014-02-01 08:00:00
updated: 2014-02-01 08:00:00
tags: "git"
categories: ["Develop", "Git"]
---

如果你已经开始工作了，一定对 `Git` 不陌生，开发需要一个团队，版本控制必不可少。如果你还在学习，准备参加工作，那建议你抽空好好学习一下 `Git`。

`Git` 是一款免费、开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。在我们的工作中也是必备的技能，还记得第一天入职主管给我的第一个任务就是让我学习 `Git`，熟悉 `Git` 的整个开发流程。`Git` 具有以下特点：

速度快、灵活

自由选择工作方式

保持工作独立

适合分布式开发，强调个体

下面是我总结的几大块 `git` 命令，与君共享。

<!-- more -->

## 一、代码上传

```shell
$ git init # 初始化 git 仓库
```

```shell
$ git add --all # 添加本地文件到暂存区
$ git add . # 或
```

```shell
$ git commit -m “注释” # 添加本地文件到版本库
```

```shell
$ git remote add origin https://***.git # 添加远程仓库地址
```

```shell
$ git push origin master # 向远程仓库推送代码
```

## 二、代码下载

1.直接下载

```shell
$ git clone https://***.git # 克隆远程代码
```

2.通过抓取

```shell
$ git init # 初始化 git 仓库
```

```shell
$ git remote add origin https://***.git # 添加远程仓库地址
```

```shell
$ git fetch origin master # 抓取远程仓库代码（只有主支）
```

```shell
$ git merge origin/master # 合并到本地仓库
```

## 三、分支管理

```shell
$ git checkout -b dev # 创建一个名叫 dev 的分支并切换到此分支
```

```shell
$ git branch # 查看有几条分支
```

```shell
$ git checkout dev # 切换到 dev 分支
```

```shell
$ git branch -m oldname newname # 更换分支名称
```

```shell
$ git merge dev # 合并分支（要切换到要合并它的分支上）
```

```shell
$ git branch -d dev # 删除当前分支（强制删除：-D）
```

## 四、版本回退

```shell
$ git reflog # 显示回退的 id
```

```shell
$ git reset --hard commit-id # 回到想要回退的版本
```

```shell
$ git reset --hard HEAD^^ # 回退到上一个版本
$ git reset --hard HEAD~
```

```shell
$ git reset HEAD~5 # 撤销过去 5 个 commit 的命令，然后在添加提交
```

## 五、其他命令

```shell
$ git --version # 查看当前 git 版本
```

```shell
$ git help --all # 查看 git 命令
```

```shell
$ git diff # 查看当前工作区域版本库有哪些区别，修改了什么内容
```

```shell
$ git status # 查看仓库当前状态
```

```shell
$ git log # 查看提交的历史记录
```

```shell
$ git log --pretty=oneline # 当前记录在一行显示
```

```shell
$ git reflog # 可以查看所有分支的所有操作记录（包括 commit 和 reset 的操作），包括已经被删除的 commit 记录
```

```shell
$ git pull # 更新本地仓库
```

```shell
$ git remote -v # 查看远程信息库 pull 和 fetch 详细信息
```

```shell
$ git branch -r # 查看远程分支
```

```shell
$ git branch -a # 查看所有分支
```

```shell
$ git push --force origin dev # 强制推荐 dev 分支（rebase 后的分支历史改变了，可能导致不兼容现象）
```

```shell
$ git remote rm # 删除远程仓库
```

```shell
$ git remote show origin # 查看远程仓库的信息
```

## 六、总结

命令有些多，可真正在工作中用的最多的也就几条，其他的了解一下，用到的时候翻阅笔记吧。在这里提醒一下，在 `push` 自己的代码之前一定要 `pull` 一下，不然很容易把别人辛辛苦苦码的代码覆盖，这样很容易挨揍的哦~
