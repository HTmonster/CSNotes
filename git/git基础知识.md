# GIT

##  初始化 git init

### 将目录初始化为仓库

## 提交到版本库

### 添加 git add

### 提交 git commit

- 参数 -m  提交的描述

## 状态

### 查看状态 git status

- modified
- deleted

### 比较 git diff

## 历史记录 

### git   log 提交记录

$ git log
commit: 版本号
Author: 提交者
Date: 日期
          描述

- --pretty=online  在一行内输出
- --graph  查看分支合并图

### git reflog  记录每一次命令

### git last 最近一次提交

## 版本控制

### 版本重置(回退）git reset   版本号

- 版本号

	- 上一个版本  HEAD^
	- 上上一个版本 HEAD^
	- 具体的版本id(不用写全）

- 参数

	- -- hard

### 版本库替换工作区 git checkout 

- --file 对应文件
- 子主题 2

### 删除文件 git  rm  文件名

## 远程仓库

### 添加远程库  git remote add 库名 ssh地址

### 推送到远程库 git push 库名 分支

### 克隆远程库 git clone  远程库地址

### 查看远程库信息 git remote

- -v 更详细信息

### 拉取 git pull

## 分支管理

### 创建分支 git branch 分支名

### 转到分支 git ckeckout 分支名

### 合并分支 git merge 分支名 

- 快速合并 不可以看出曾经合并
- 合并冲突 

	- 解决冲突 提交

- --no-ff 普通合并 【可以看出曾经合并】 

### 查看分支 git branch

### 删除分支 git branch -d[D] 分支名  

## 工作区间 暂时存储

### 工作现场暂存 git stash

### 查看列表 git stash list

### 返回现场 git stash pop

### 恢复指定现场 git stash apply  stash@{id}

## 标签 git tag

### git show

- 查看标签信息

### 创建

- -a 指定标签名  
- -m  指定说明文件
- -s 私钥签名

### 删除 -d

## 忽略文件 .gitignore

## 配置别名

### --global

### alias

## 区间

### 工作区

- 所能看到的目录

### 版本库

- 缓存区 stage (index)
- 第一个分支 master

	- HEAD  指向master的指针

## 可以合并为 git ckeckout -b 分支名

*XMind - Trial Version*