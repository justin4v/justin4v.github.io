---
title:  Git简单理解与使用
categories: git
tags: git
author: justin4v
---

## 版本库概念

- **工作区(workspace)：**工作目录，发生更改的地方，不隐藏。
- **版本库(repository)：**workspace同级目录下有一个隐藏目录.git。不属于工作区，而是版本库 Repository。
- **暂存区(stage/index)：**stage, 或index。在repository 中的 index 文件中，故暂存区有时也叫作索引（index）。
- **远程库(remote)：**托管代码的远程服务器。

<!-- more -->

目录间的转换关系如下:

<img src="https://justin4v.github.io/image/git/git目录转换.jpg">

<img src="https://justin4v.github.io/image/git/git版本库结构.jpg">

<img src="https://justin4v.github.io/image/git/git目录.jpg">

- repository 中标记为 "index" 的区域是**暂存区**（stage, index）
- 标记为 "master" 的是 **master 分支所代表的目录树**。
- "HEAD" 实际是一个"游标"，指向当前分支（master）
- 所以命令中的HEAD 可以用 分支名（master） 来替换
-  objects 标识的区域为 Git 的 **对象库**，实际位于 ".git/objects" 目录下，里面包含了创建的各种对象及内容

## git 命令的效果

1. 当对**工作区修改（或新增）的文件**执行 **`git add`** 命令时，**stage的目录树被更新**，同时工作区修改（或新增）的文件内容被**写入到对象库**中的一个新的对象中，而该对象的 ID 被记录在暂存区的文件索引中

2. 当执行提交操作 **`git commit -m `** 时，**暂存区的目录树写到版本库（对象库）**中，master 分支会做相应的更新

   即 **master 指向**的目录树就是**提交时暂存区的目录树**

3. 当执行 **`git reset HEAD`** 命令时，**暂存区的目录树会被重写**，被 master 分支指向的目录树所替换，但是工作区不受影响

4. 当执行 **`git rm --cached `** 命令时，会直接**从暂存区删除文件**，工作区则不做出改变。

5. 当执行 **`git checkout .`** 或者 **`git checkout -- `** 命令时，会**用暂存区全部或指定的文件替换工作区的文件**

   这个操作很危险，会清除工作区中未添加到暂存区的改动

6. 当执行 **`git checkout HEAD .`** 或者 **`git checkout HEAD `** 命令时，会**用 HEAD 指向的 master 分支中的全部或者部分文件替换暂存区和以及工作区中的文件**

   这个命令也是极具危险性的，因为不但会清除工作区中未提交的改动，也会清除暂存区中未提交的改动