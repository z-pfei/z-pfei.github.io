---
title: git stash
date:
tags: git stash
comments: true
categories: git
---
## git stash

<!-- more -->

前几天在使用git时遇到一个小问题，问题描述如下：

在分支0开发一个小需求时临时要改一个bug，于是我`git stash`，然后切换到分支1，在这个分支做了些修改又要临时到分支2，于是我又`git stash`，在分支2处理好后回到分支0继续我最开始工作，于是我`git stash pop`，然后惨了，恢复出来的代码不是我想要的，完全给我添乱。

上面的描述有些绕，出现这种情况的原因是`git stash pop`取出的是stash list中第一条，而我需要stash list中的第二条，所以现在取出来的是在分支1搁置的修改。

如果你使用了`git stash`搁置过多次修改，在从搁置栈中取数据时不确定是不是要取第一条，那么不要直接`git stash pop`，因为他是恢复搁置栈中的第一个，不管分支，所以在别的分支上`git stash`之后又在当前分支`git stash pop`会把在其他分支上搁置的改动merge到当前分支发生冲突。可以这样，

+ 首先用`git stash list`查看搁置栈中的内容；

+ 然后用`git stash apply stash@{n}`取出相应的第n条搁置数据；ok啦~
___
顺便一提`git stash pop`和`git stash apply`的区别
`git stash apply`只会读搁置栈中的数据，恢复之后搁置栈中的数据仍在，而`git stash pop`取出数据后搁置栈中的数据也就不存在了