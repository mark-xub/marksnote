---
title: git 使用总结  
date: 2017-01-06 21:26:39
tags: [工具]
---
### workspace、index与head
首先，我们先区分workspace、index、head的概念，这是基础，理解了对大部分命令也就了然了。  

![dd](/img/gitinfo.png)

- workspace（working tree），就是你现在编辑的源文件和目录  
- index（staging area），git 特别设计的一个暂存区，用来保存还没提交的修改
- local repository，是所在仓库的所有分支信息，而head是一个指向当前提交的指针

<!-- more -->  

### add 与 diff
当 git add 一个文件时，git其实做了 
 
- 把文件内容通过SHA1算法生成的签名保存在**.git/index**目录下  
- 把文件内容变成blob对象保存在**.git/objects**目录下 

所以 git diff 比较的是working tree与index  
git diff --cached 比较的是index与head，即将要提交的变更  
git diff head 比较的是working tree与head  

### checkout、reset与revert 
- checkout 是将head移动到一个新的分支，作用于working tree，所以要把当前未提交的修改add到暂存区
- reset 是删除之前的提交记录,作用范围具体看命令文档 

```shell
--mixed               reset HEAD and index  
--soft                reset only HEAD  
--hard                reset HEAD, index and working tree  
--merge               reset HEAD, index and working tree  
```
- revert 是用一个新的提交覆盖原来的提交来达到回滚的目的

> 注意reset与revert的区别
> >如果一个branch在reset之后与原来的branch合并,reset时删除的提交记录还会出现，而revert不会。

### rebase 与 merge
- 使用merge，在分支合并时会产生一次新的提交
- 使用rebase，能把提交记录变成线性，防止每次都产生一次新的提交，但是它会使得本地的提交记录更改  
他们的一些区别可以看[这里](https://www.atlassian.com/git/tutorials/merging-vs-rebasing/conceptual-overview)  

> 最佳实践
> > - 如果要使用rebase，必须保证你当前的分支没有其他人用，并且upstream的分支上没有存在你当前分支的提交内容，否则就不要用
> > - 如果使用merge，最好加上--no-ff,保证一个清晰的分支提交，其他人能清楚的了解到merge的目的

