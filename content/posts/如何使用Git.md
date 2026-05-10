---
title: "如何使用Git"
date: 2023-03-18T13:17:37+08:00
draft: false
tags: [Git]
categories: [技术分享]
featured_image: 
description: 
---

[学习视频](https://www.bilibili.com/video/BV1FE411P7B3/?spm_id_from=333.337.search-card.all.click&vd_source=a76b8a2a6d9a18738abcb916b7836085)

[笔记资料](https://www.kuangstudy.com/bbs/1532247011263672321)

[Git简明指南](https://www.runoob.com/manual/git-guide/)

[Git历史](https://www.jianshu.com/p/8821e9846773)

Git是一个开源的分布式**版本控制**系统

当下最流行的版本控制工具

## 版本控制

版本控制（Revision control）是一种在开发的过程中用于管理我们对文件、目录或工程等内容的修改历史，方便查看更改历史记录，备份以便恢复以前的版本的软件工程技术。

作用：

- 实现跨区域多人协同开发
- 追踪和记载一个或者多个文件的历史记录
- 组织和保护你的源代码和文档
- 统计工作量 并行开发、提高开发效率
- 跟踪记录整个软件的开发过程
- 减轻开发人员的负担，节省时间，同时降低人为错误

1. 本地版本控制

   记录文件每次更新，对版本快照，记录补丁信息

2. 集中版本控制

   所有的版本数据保存在服务器上，协同开发者从服务器上同步更新自己修改

3. 分布式版本控制

   不会因为服务器损坏或网络问题，造成不能工作的情况

   每个人拥有全部代码，有安全隐患

## Git安装

git官网：http://git-scm.com/downloads

镜像：https://npm.taobao.org/mirrors/git-for-windows/



卸载：反安装即可

* 清理环境变量

* 卸载

安装

* 下载软件安装包
* 默认安装
* 右键看到对应程序

Git Bach：Unix与linux风格命令行，使用最多、推荐最多

Git CMD：Windows风格命令行

Git GUI：图形化Git，不建议新手使用

## 基本的Linux命令

cd：改变目录，直接cd进入默认目录

cd..：退回上一个目录

pwd：显示当前所在的目录路径

ls：列出当前目录中的所有文件，ls(ll)更详细

touch：新建一个文件，touch index。.

rm：删除一个文件

mkdir：新建一个目录，新建文件夹

rm -r：删除一个文件夹rm-r src 删除src目录 rm -rf f表示根，删除-rf，删除所有

mv：移动文件，mv index.html src 移动index文件到src目录下

reset：重新初始化终端，清屏

clear：清屏

history：查看命令历史

help：帮助

exit：退出

git config -l：查看配置 

> git config —system —list 系统配置 Git\etc\gitconfig
>
> git config —global —list  用户配置 C:users\Adminstrator\\.gitconfig



## Git基本理论

- **工作区(Workspace)**：平时存放项目代码的地方。
- **暂存区(Stage/Index)：**暂存区，用于临时存放你的改动，事实上它只是一个文件，保存即将提交到文件列 表信息
- **版本库(Repository)：**又称本地仓库，这个不算工作区，而是 Git 的版本库，里面有你提交到所有版本的数据。
- **远程仓库(Remote)**：托管代码的服务器github、gitee

![image-20230306135917942](D:\文档\Typora文档\images\如何使用Git\image-20230306135917942.png)

![img](https://kuangstudy.oss-cn-beijing.aliyuncs.com/bbs/2022/06/01/kuangstudy3c1708a2-4e6e-4433-9c51-6d8b4257ce72.png)

创建仓库

```bash
# 使用当前目录作为 Git 仓库，我们只需使它初始化。
git init
```

克隆远程仓库项目，相当于SVN导出项目

```bash
git clone <url>
```

## Git文件操作

文件四种状态

* Untracked：未跟踪，此文件在文件夹中，但并没有加入到git库，不参与版本控制，通过git add状态变为staged
* Unmodify：文件已经入库，未修改，版本库中的文件快照内容与文件夹中一致。这种文件如果被修改，变为Modified。如果使用git rm移除版本库，则变为Untracked文件。
* Modified：文件已修改，仅仅是修改，并没有进行其他操作。可以通过git add进入暂存staged状态，使用git checkout则丢弃修改，返回unmodify
* Staged：暂存状态，执行git commit修改同步到库中，这是库中文件与本地文件变为一致，文件unmodify状态。执行git rest HEAD filedname取消暂存，文件状态为modeified。

```bash
# 查看指定文件状态
git status [filename]
# 查看所有文件状态
git satus
# 添加所有文件到暂存区
git add .
# 提交暂存区数据到本地
git comit -m “消息内容”
# 提交暂存区文件到远程
git push
```

忽略文件

```bash
*.txt 		# 忽略所有.txt结尾文件
!lib.txt 	# 忽略所有.txt结尾文件，但lib.txt除外
build/ 		# 忽略build/目录下所有文件
/temp 		# 仅忽略项目根目录下的TODO文件，不包括其他目录的temp
doc/*.txt 	# 忽略某一文件夹下的文件
```

## 使用码云

设置本机SSH公钥，免密码登录

```bash
ssh-key #默认存放位置C:\Users\MPI_1070\.ssh
```



```bash
# 找到放置位置
git clone 
```

本地项目复制到git仓库文件夹，或者git仓库文件内容复制到项目文件

```
git add. # 添加所有文件到暂存区
git commit -m “消息内容”
git push # 提交到远程仓库
```



## 使用Github



## Git分支

多线程：主线程在走，不影响子影响。平行，互不影响。可以进行合并。在合并的时候就需要做一些处理。

```bash
# 列出所有本地分支
git branch
# 列出所有远程分支
git branch -r
# 新建一个分支，但依然停留在当前分支
git branch [branch-name]
# 新建一个分支，并切换到该分支
git checkout -b [branch]
# 合并指定分支到当前分支
$ git merge [branch]
# 删除分支
$ git branch -d [branch-name]
# 删除远程分支
$ git push origin --delete [branch-name]
$ git branch -dr [remote/branch]
```

