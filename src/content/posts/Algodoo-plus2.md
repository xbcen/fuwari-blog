---
title: Algodoo plus：函数
published: 2026-01-21
description: '(e)={}'
image: ''
tags: ["Algodoo","Algodoo plus"]
category: 'Algodoo'
draft: false 
lang: ''
---

函数的写法

基本的格式：

```(传参)=>{代码}```

如果不需要传参，则：

```{代码}```

举个实际例子：

```f=(a,b)=>{a+2b}```

这个函数的意思就是返回a+2b的结果。

当输入`f(1,2)`时就会返回5（`1+2*2`）。

# 用函数的原因

你现在写了个hsv转rgb的代码，非常长，但是你又要给一堆物件用上。

这个时候你就可以这样写：

1. 在控制台输入以下代码：`scene.my.f=(h,s,v)=>{//代码}`

2. 给物体要用的地方输入`scene.my.f(colorhsva(0),colorhsva(1),colorhsva(2))`

好的，任务完成了。

至于函数这东西，你们大概都见过，例如`(e)=>{}`

所以也会有`ondie(0)`这种写法。