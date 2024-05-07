---
layout:     post
title:      Unity PlayableAPI：中世纪近战游戏实战开发笔记
subtitle:   
date:       2024-05-07
author:     JohnWayne
header-img: resources/Gigaya.jpg
catalog: true
tags:
    - 动画系统
    - 游戏开发
---

>Unity作为一款流行的游戏开发引擎，其持续的技术创新为游戏开发者提供了更多的可能性。其中，Unity PlayableAPI是一项强大的工具，允许开发者以更灵活的方式创建复杂的游戏玩法和动画。本文将首先回顾Unity PlayableAPI的历史发展，然后以一个中世纪近战游戏为例，探讨具体的技术实现，并最终分析其利弊。

------

## Unity PlayableAPI的历史发展
Unity PlayableAPI是Unity引擎自2016年引入的一项功能，它提供了一种将动画片段和控制逻辑组合在一起的方式，从而创建更复杂、更交互式的游戏玩法。随着Unity版本的更新，PlayableAPI得到了不断的改进和扩展，为开发者提供了更多的灵活性和效率。

## 中世纪近战游戏的技术实现
我们以一个中世纪近战游戏为例，介绍如何利用Unity PlayableAPI实现其中的核心功能。

Playable可以通过一组API来创建一个Graph，而每个Graph可以由多个树形结构组成，每个树状结构都由一个Output节点作为根节点，叶子结点则由各种Playable组成。

基本层级有AnimUnit, AnimAdapter, Mixer, LayerMixer, BlendTree2D, QueuePlayer
<img src="https://raw.githubusercontent.com/johnwayne1995/johnwayne1995.github.io/master/resources/2024-05-07-Unity PlayableAPI：中世纪近战游戏实战开发笔记/mindmap.svg" width="800" height="600">
![](https://raw.githubusercontent.com/johnwayne1995/johnwayne1995.github.io/master/resources/2024-05-07-Unity PlayableAPI：中世纪近战游戏实战开发笔记/mindmap.svg?sanitize=true)
## 利与弊
###灵活性：PlayableAPI提供了灵活的方式来创建复杂的动画逻辑，使开发者能够实现各种创新的游戏玩法。

效率：通过可重复使用的PlayableBehaviour脚本和状态机，可以提高开发效率，减少重复劳动。

交互性：PlayableAPI允许动态地控制动画播放，使游戏更具交互性和响应性。
###弊：
学习曲线：对于新手开发者来说，学习和掌握PlayableAPI可能需要一定的时间和精力。

复杂性：随着项目规模的增长，PlayableAPI的使用可能会变得复杂，需要谨慎设计和管理动画逻辑。


### 参考链接

<iframe src="//player.bilibili.com/player.html?aid=893386401&bvid=BV1SP4y177YQ&cid=493316198&p=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>

作者 [张巍]

2024 年 05月 07日    
