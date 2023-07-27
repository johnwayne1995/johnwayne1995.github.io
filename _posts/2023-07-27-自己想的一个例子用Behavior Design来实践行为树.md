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
并行选择节点，并行执行，一真即真，**一真即停**，全假才假。

### 4. 执行
![](https://raw.githubusercontent.com/johnwayne1995/johnwayne1995.github.io/master/resources/2023-07-27-自己想的一个例子用Behavior Design来实践行为树/吸血.gif)
![](https://raw.githubusercontent.com/johnwayne1995/johnwayne1995.github.io/master/resources/2023-07-27-自己想的一个例子用Behavior Design来实践行为树/被人打断.gif)

---

## 需要用代码实现的需求

让我们丰富一下这个功能，封装一层Action做节点
![](https://raw.githubusercontent.com/johnwayne1995/johnwayne1995.github.io/master/resources/2023-07-27-自己想的一个例子用Behavior Design来实践行为树/吸血封装.png)

```CSharp
// Bite.cs, 自定义节点：叮人。注意要继承Action

using UnityEngine;
using BehaviorDesigner.Runtime.Tasks;

public class Bite : Action
{
    public override TaskStatus OnUpdate()
    {
        Debug.Log("bite");
        return TaskStatus.Success;
    }
}

------------------

public class GameLoop: MonoBehaviour 
{

    private BehaviorTree m_bt;

    void Start()
    {
        // 动态添加行为树
        var bt = gameObject.AddComponent<BehaviorTree>();
        // 加载行为树资源
        var extBt = Resources.Load<ExternalBehaviorTree>("mosquitoBehavior");
        bt.StartWhenEnabled = false;
        bt.RestartWhenComplete = true;
        // 设置行为树
        bt.ExternalBehavior = extBt;
        bt.EnableBehavior();
        // 把行为树对象缓存起来，后面需要通过它来设置变量和发送时间
        m_bt = bt;
    }
    
    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            m_bt.SendEvent("DiscoverPerson");
        }
        if (Input.GetKeyDown(KeyCode.F))
        {
            m_bt.SendEvent("OnPersonMove");
        }
    }
}



```

------

## BehaviorDesign不能做哪些事情？

[nodeCanvas工具和BehaviorDesign的特性比较][2]
[BehaviorDesign可以集成PlayMarker和对话系统][3]


[待更]

作者 [JohnWayne]
2023 年 07月 27日


[1]: https://blog.csdn.net/linxinfa/article/details/124483690
[2]: https://nodecanvas.paradoxnotion.com/features-comparison/
[2]: https://opsive.com/support/documentation/behavior-designer/integrations/

