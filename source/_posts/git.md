---
title: git
date: 2016-04-12 17:50:25
tags: git
comments: true
categories: git
---

<style type="text/css">
	.titles{
		color: #C00000;
		font-size: 16px;
	}
	.tips{
		color: #cccccc;
		font-size: 12px;
		padding-left: 40px;
	}
</style>

<h2>我的git学习笔记</h2>
<!-- more -->
<span class="titles">常用命令集合：</span>
1.克隆已存在的git项目
```javascript
$ git clone 项目地址
```
2.把当前git项目里没有纳入版本控制的都添加进版本`(注意后面必须加点号)`
```javascript
$ git add .
```
3.把代码提交进本地的版本库并添加注释
```javascript
$ git commit -m "这次提交的注释"
```
	git commit --amend -m "提交的注释" 	// 重新提交，当做了一次提交之后发现有漏掉的文件没有提交可以使用此命令，注意会覆盖上一次提交
	git commit -a 	// 如果只有更新没有add，此命令可以跳过git add

4.把所有add过却没有commit的文件去掉add状态变为未被跟踪过
```javascript
$ git reset head
```
5.查看当前git里文件的状态`（这条命令很实用，若忘了下一步该如何操作此命令会做相应提示）`
```javascript
$ git status
```
6.在git里移除某个文件`（连带从工作目录中删除，这个只能删除没有修改和放入暂存区的）`
```javascript
$ git rm "文件名"
```
	git rm -f 	// 这里的f是fource强迫的缩写强制删除，这个能删除修改了放入暂存区的，不能被git恢复
7.更换文件名
```javascript
$ git mv "以前的名字" "后来的名字"
```
8.查看git的日志。只能显示几条，最新的显示在前面`（命令过长终止该命令只需按q键）`
```javascript
$ git log
```
	git log --author=***	// 查看某作者的提交记录（可以加上负值来控制显示条数）
	git log -p     // 按补丁格式显示每个更新之间的差异
	git log --stat 	   // 显示每次更新的文件修改统计信息
	git log --pretty=oneline（每个提交放在一行显示）/short（不显示Date）/full(不显示Date显示提交者)/fuller（显示作者、修改日期、提交者、提交日期）/format(后跟指定格式)    // 指定不同于默认格式的方式展示提交历史
9.列出项目所有的分支。列出来的分支前带*号的为当前分支
```javascript
$ git branch
```
	git branch "新分支名"	// 在本地新建分支
	git branch -a       // 查看所有分支（origin/master分支，这实际上是git从远程clone下来的一个分支，指向远端origin的master分支，用来跟踪远程origin的master变化情况）
	git branch -v 		// 查看每一个分支的最后一次提交
	git branch -d "分支名"	// 删除本地分支
10.切换分支
```javascript
$ git checkout "分支名"
```
	git checkout -b "分支名"	// 新建并切换到新分支
	git checkout -- [file] 		// 撤销之前所做修改
11.合并分支（合并merge后的分支到当前分支）
```javascript
$ git merge "分支名"
```
	git merge --abort	// 合并时遇到冲突可取消合并，恢复index
12.创建一个名为.git的子目录
```javascript
$ git init
```
13.从远程分支获取最新版本并merge到本地
```javascript
$ git pull
```
14.更新本地更改到远程
```javascript
$ git push
```
	git push --set-upstream origin "分支名"		// To push the current branch and set the remote as upstream
	git push origin :"分支名"		// 删除远程分支，：前一定要加空格，相当于push一个空分支到远程
15.搁置当前正在进行的工作（比如想pull最新的代码，又不想加新commit，或为了fix一个紧急的bug，先stash，返回到上一个commit，改完bug之后再stash pop，继续原来的工作）
```javascript
$ git stash
```
___
在分支开发工作流中，当你做这么多操作的时候，这些分支全部存储于本地。当你新建和合并分支的时候，所有这一切都只发生在你本地的git版本库中，没有与服务器发生交互。