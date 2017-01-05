---
title: 由实时系统想到的
date: 2017-01-05 09:48:08
tags: [工作经验]
---

到底什么是实时或者准实时？平时经常听到这些词汇，有些概念还是要理理清楚。  
对于实时系统，按照wiki的说法：
> Real-time programs must guarantee response within specified time constraints, often referred to as "deadlines".Systems of this type whose correctness depends on their temporal aspects as well as their functional aspects. 
> 

也就是说，实时系统是指，在给定的时间限制内，程序必须完成响应。程序的正确性不仅依赖于逻辑正确还依赖于时效性。  
<!-- more -->  
一般的业务系统，我们小码农开发的时候很少考虑时效性，功能正常就行，一个原因是我们默认访问数据库，数据库响应10ms以内，另一个原因是一般的业务对时效性要求不高，能容忍一定的脏数据。
  
到这里，其实讨论一个系统是不是实时已经没有意义了，我们重要的是保证程序正确，它需要考虑逻辑是否正确，时效性是否符合要求。
  
比如说实时搜索，延迟多久才是合适的呢？首先，用户等待的耐心可能最多就3s，你必须在3s内返回，3s是上限。其次，在这段延迟时间内，你搜索的结果不能很大概率发生了变更，导致不符合用户筛选的条件，这个错误率必须是一个可容忍的范围内。

恩，大概就是这个意思。






