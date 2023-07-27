---
layout:     post
title:      自己想的一个例子用Behavior Design来实践行为树
subtitle:   
date:       2023-07-27
author:     JohnWayne
header-img: resources/2023-07-27-自己想的一个例子用Behavior Design来实践行为树/CoverBackground.png
catalog: true
tags:
    - 行为树
    - 游戏开发
---
# 

------
CSDN上的教程有很多 [【游戏开发教程】BehaviorDesigner插件制作AI行为树（Unity | 保姆级教程 | 动态图演示 | Unity2021最新版][1]，介绍了顺序节点、并行节点、选择节点、随机、优先级、中断、竞争、评估的概念，触发事件、通过继承来拓展节点。

看教程不如手撸一遍。夏天到了，我们来实现蚊子的行为模式：循环执行检测附近是否有人，有人的话飞到身边，等待5s，5s后开始吸血，如果5s内人有动作，则中断等待，立刻逃走。

------

## 不用代码实现的需求

### 1. 吸血的行为树
![](https://raw.githubusercontent.com/johnwayne1995/johnwayne1995.github.io/master/resources/2023-07-27-自己想的一个例子用Behavior Design来实践行为树/吸血.png)

### 2. 吸血被人打断的行为树
![](https://raw.githubusercontent.com/johnwayne1995/johnwayne1995.github.io/master/resources/2023-07-27-自己想的一个例子用Behavior Design来实践行为树/被人打断.png)

### 3. 为什么不能用Parallel Selector？

### 4. 执行
![](https://raw.githubusercontent.com/johnwayne1995/johnwayne1995.github.io/master/resources/2023-07-27-自己想的一个例子用Behavior Design来实践行为树/吸血.gif)
![](https://raw.githubusercontent.com/johnwayne1995/johnwayne1995.github.io/master/resources/2023-07-27-自己想的一个例子用Behavior Design来实践行为树/被人打断.gif)

---

## 需要用代码实现的需求

让我们丰富一下这个功能，封装一层Action做节点
![](https://raw.githubusercontent.com/johnwayne1995/johnwayne1995.github.io/master/resources/2023-07-27-自己想的一个例子用Behavior Design来实践行为树/吸血封装.png)

------

## BehaviorDesign不能做哪些事情？

[nodeCanvas工具和BehaviorDesign的特性比较][2]

[待更]

作者 [JohnWayne]     
2023 年 07月 27日


[1]: https://blog.csdn.net/linxinfa/article/details/124483690
[2]: https://nodecanvas.paradoxnotion.com/features-comparison/

