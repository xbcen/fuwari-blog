---
title: Algodoo代码
published: 2025-08-11
description: 'Algodoo代码合集，收集中……'
image: ''
tags: ["Algodoo","代码"]
category: 'Algodoo'
draft: true 
lang: ''
---

调整ui不透明度：`gui.skin.opacity = 0.925`

更改背景（天空颜色）：`app.background.skycolor=颜色（rgba）`

生成圆形：`Scene.addCircle()`

生成方形：`Scene.addBox()`

生成追踪器（追尾）：`scene.addPen()`

生成物件时生成变量需要这么写：`x := a`

注：0～1随机取值：`rand.uniform01`

-3～+3随机取值（标准正态分布）：`rand.normal`

注：取值在-3～+3以外的概率非常小，但不是0%。`

赛博风向（弧度制）：`sim.windangle`

赛博风力（单位：平方米/秒）：`sim.windstrength`

x～y随机取值（y>x）：`rand.uniform01*(y-x)+x`

取整数（舍尾法，也有把文本转换为数字格式的作用）：`math.toint(x)`

左右简单平移：`pos = [pos(0) + math.sin(sim.time) , pos(1)]`

上下简单平移：`pos = [pos(0) , pos(1) + math.sin(sim.time)]`

左右平移（不容易穿模，写poststep）：`vel = [math.sin(sim.time - scene.my.time关卡号) * x, 0.16333334];`

上下平移（不容易穿模，写poststep）：`vel = [0, math.sin(sim.time - scene.my.time关卡号) * x]`

注：1.x代表物体移动到最左边中心/最下面中心到移动到最右边中心/最上面中心的距离/2
　　2.提高/降低移动速度请同时扩大/缩小math.sin()与x的值。
　　如：`math.sin((sim.time - scene.my.time关卡号) * 2) * 2x`
　　3.需要将物体的密度设置为一个较大数，如：8888888,1919810
　　4.代码为自左向右/自下往上，需要向物体放置于最左边。如果需要右自向左/自上往下，请在`math.sin`前面加上-（即`- math.sin`），并向物体放置于最右边/最上边。
　　5.需要在物件的onspawn中定义：`scene.my.time关卡号 = sim.time`
　　6.0.16333334来源于`Sim.gravityStrength / Sim.frequency`的计算结果。

摄像机缩放：`scene.camera.zoom`

注：`scene.camera.zoom`的值是缩放值的150倍。（如：`scene.camera.zoom=36`，缩放值为36/150=0.24x）

摄像机位置：`scene.camera.pan`

老生常谈for循环（a为整数）：`for(a, (x)=>{//代码//})`

按回车键自动运行（写update）（小键盘回车请将"return"改为"enter"，其他键位请自己查询）：

```thyme
(e)=>{
Keys.isDown("return")?{
Sim.running = true
}:{}
}
```

隐藏左上角UI（写update）：

```thyme
(e)=>{
sim.running ? {
Scene.addWidget({
Widgetid := "MenuBar";
visible := false
});
} : {
Scene.addWidget({
Widgetid := "MenuBar";
visible := true
});
}
}
```

物体顺逆轮流转（1）（写轴承poststep）：

```thyme
(e)=>{
sim.tick % 数值 == 0 ? {
ccw = ! ccw
} : {}
}
```

物体顺逆轮流转（2）（写轴承poststep）：

```thyme
(e)=>{
motorspeed = math.sin(sim.time) * math.pi
}
```

注：`math.pi`相当于马达速度30rpm。

物体顺逆轮流转（3）（写物体poststep）

```thyme
(e)=>{
angle=math.sin(sim.time)
}
```

染色（写物体oncollide）：
```thyme
(e)=>{
color = e.other.color;
update = e.other.update
}
```

被雷射笔照到过关（写雷射笔onlaserHit）：

```thyme
(e)=>{
e.geom._M ? {
e.other.pos = scene.my.s关卡号m;
e.other.collideset = 16;
scene.my.spots = scene.my.spots关卡号 - 1
} : {}
}
```
排行榜文字背景（增加可读性）(写oncollide，使用时请去掉注释):

```thyme
(e)=>{
e.other._pp ? {
e.other.update = (e)=>{};
e.other.text = "<markup><span background=\"#cccccc\"//背景hex颜色><span color=\"#000000\"//球hex颜色>球名字</span></span></markup>";
e.other.textcolor = [1,1,1,1]
} : {}
}
```

随机概率过关（需要先定义_rand变量）（写物体oncollide）：

```thyme
(e)=>{
e.other._M ? {
_rand = rand.uniform01;
_rand <= 0.5 ? {
e.other.pos = scene.my.s关卡号m;
e.other.collideset = 16;
scene.my.spots关卡号 = scene.my.spots关卡号 - 1
} : {
e.other.pos = scene.my.s关卡号
};
scene.my.spots关卡号 < 1 ? {
scene.removeentity(e.this)
} : {}
} : {}
}
```

回家静止（写物体oncollide）：

```thyme
(e)=>{
e.other.timetolive=6;
e.other.density=+inf;
e.other.poststep=(e)=>{
timetolive < 1?{
timetolive=+inf;
density=2.0;
poststep=(e)=>{}
}:{}
}
}
```

回家区免疫下层（写oncollide）：


```thyme
(e)=>{
e.pos(1) >= e.this.pos(1) ? {
e.other.pos = scene.my.s关卡号
} : {}
}
```

反重力（写oncollide）：
```thyme
(e)=>{
e.other._M ? {
e.other.postStep = (e)=>{
vel = vel + [ - math.sin(sim.gravityAngleOffset), math.cos(sim.gravityAngleOffset)] * Sim.gravityStrength * 2 / Sim.frequency
}
} : {}
}
```