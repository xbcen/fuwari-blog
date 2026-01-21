---
title: Algodoo plus：物体的移动
published: 2026-01-21
description: 'Algodoo中关卡的神奇物体是怎么动的……'
image: ''
tags: ["Algodoo","Algodoo plus","代码"]
category: 'Algodoo'
draft: false 
lang: ''
---

这是一个新系列，讲的是如何让你的图更加有趣以及代码的简洁。

这个系列建立在你已有一定的 Algodoo 代码经验上，不然可能看不懂。

没啥事的话，让我们开始吧 :)

# 物体的运动

接下来会给出 vel 和 pos 两种选择，前者不容易穿模。

1.如果把物件放在`ondie`中，需要将`sim.time`加上`sim.time-scene.my.time关卡号`，并在物件的`onspawn`中定义：`scene.my.time关卡号 = sim.time`。

2.vel 方式需要将物体的密度设置为一个较大数，如：8888888,1919810，pos 建议密度 + inf，提高运行速度。

3.0.1633334 来源于`Sim.gravityStrength / Sim.frequency`的计算结果。

# 1. 简单路径平移

直接给代码，没啥好讲。

左右运动：

```
pos = [pos(0) + math.sin(sim.time) * x , pos(1)];
vel = [math.sin(sim.time) * x, 0.1633334];
```

上下运动：

```
pos = [pos(0) , pos(1) + math.sin(sim.time) * x];
vel = [0, math.sin(sim.time) * x];
```

注意事项：

1.x 代表物体移动到最左边中心 / 最下面中心到移动到最右边中心 / 最上面中心的距离 / 2。

2.提高 / 降低移动速度请同时扩大 / 缩小 `math.sin ()` 与 `x` 的值。

如：`math.sin(sim.time * 2) * 2x`

3.代码为自左向右 / 自下往上，需要向物体放置于最左边。如果需要右自向左 / 自上往下，请在`math.sin`前面加上`-`（即`- math.sin`），并向物体放置于最右边 / 最上边。

# 2. 函数路径平移

注意事项：

1. 函数平移需要确定你的函数经过以下处理后仍有实数解，否则物件会消失。

2. 函数平移提高 / 降低移动速度请同时扩大 / 缩小 `x1~,y1~,sim.time` 的值。

如：`vel = [1 * a, 3 * a * (sim.time * a) ^ 2 + 0.1633334]`

3. 若绘制圆锥曲线时，请直接使用 $\left\{\begin{aligned}x&=sin x \\y&=cos x \end{aligned}\right.$ 形式的参数方程。

首先需要有一个函数`f (x)`。

将其转为参数方程（其中参数为`sim.time`），得到 x 和 y

$\left\{\begin{aligned}x&=t_1\\y&=t_2\end{aligned}\right.$

则`pos=[pos(0) + t1~, pos(1) + t2~]`

将其求导，可得

$\left\{\begin{aligned}x_1&=t_1^{\prime}\\y_1&=t_2^{\prime}\end{aligned}\right.$

则`vel = [x1~, y1~]`

注意事项：

物件运动范围为函数的一、三象限部分。

如果这样的话，你的物件可能就一去不复返了，我们可以使其看起来折返，将参数`sim.time`变成`math.sin(sim.time)* n`。

注意事项：

1. 截取的是以原点为中心，`2 x 2n`的长方形内的部分。

2. 若将`x1~, y1~`分别扩大`a, b`倍，则会在以物件为中心，`2a x 2bn`的长方形内运动。

题外话：

不知道求导？不知道参数方程？没事，你把下面的这一段话发送给AI：

> 接下来我会给你一个函数
>
>你需要将其转为参数函数，得到x与y（其中参数为a）
>
>然后分别求导，得到x1与y1
>
>最后你只需要直接给我以下内容，不要夹带其他内容：
>
>pos=[x,y]
>
>vel=[x1,y1+0.1633334]
>
>（参数a按照上面文章的内容填入）

基本说完了，可以在评论区指正/补充/提出建议。
