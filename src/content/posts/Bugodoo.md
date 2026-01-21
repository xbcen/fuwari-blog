---
title: Algodoo Bug
published: 2025-08-11
description: 'Algodoo华佗？还是Algodoo华雄'
image: ''
tags: ["Algodoo","Bug"]
category: 'Algodoo'
draft: false 
lang: ''
---

叠甲：看完本章不能保证你成为Algodoo大牢，但可以帮助你应对Algodoo中的Bug。

无把握请勿修改代码，若因此造成bug建议重开Algodoo。

# 门诊（不急的bug）

## UI没了。

![1.1](https://raw.githubusercontent.com/xbcen/pic/main/picture/1.1.png "UI没了")

解决方法：按tab键。

若第一步无作用，请执行以下操作：

1. 按下键盘F10。

2. 切换英文输入法。

3. 盲打以下代码：`gui.skin.opacity = 0.925`

4. 回车。

实在不行重置（还是速通大牢）

## 排名重复。

![1.2](https://raw.githubusercontent.com/xbcen/pic/main/picture/1.2.png "重复的排行榜")

1.选中文本框。

![1.2.1](https://raw.githubusercontent.com/xbcen/pic/main/picture/1.2.1.png "被选中的文本框")

2.右键-碰撞作用层-勾上J。

## 烟花喷射战士。

![1.3](https://raw.githubusercontent.com/xbcen/pic/main/picture/1.3.png "冠军的烟花")

1.选中球。

2.右键-碰撞作用层-取消可与液体作用。

## 烟花错位，不显示。

![1.1](https://raw.githubusercontent.com/xbcen/pic/main/picture/1.1.png "UI没了")

1.选中球，右键，选取，选取，选取圆形物件。

脚本选单，在poststep中将`vecs:=[[56,-201],[56,-201]]`;中的`[56,-201]`更改为球现在所在的位置。

## 按快捷键的时候Algodoo莫名其妙关闭了。

成因：按到ctrl+Q了。

挽救方案：重新打开Algodoo，看看有没有自动保存些什么。

## 变量[BAD]

方法1：ctrl+z。

方法2：在上面输入框输入：`xxx=xxx`

![输入框](https://raw.githubusercontent.com/xbcen/pic/main/picture/输入框.png "Algodoo输入框")

如：ondie=(e)=>{}

# 急诊（急性bug，请做好图没了的准备）

## 同时过关。

1. 按F10，输入以下代码：`scene.my.spots关卡号=scene.my.spots关卡号+1`，回车。

（例:`scene.my.spots2=scene.my.spots2+1`）。

2. 选中过关区，右键，脚本选单，在oncollide中输入以下代码：

```
(e)=>{
e.other._M ? {
e.other.pos = scene.my.s关卡号m;
e.other.collideset = 16;
scene.my.spots关卡号 = scene.my.spots关卡号 - 1
} : {};
scene.my.spots关卡号 == 1 ? {
colorhsva = [180, 1, 1, 1];
oncollide = (e)=>{
e.other.pos = scene.my.no(52-关卡号);
e.other.collideset = 768;
scene.my.spots关卡号 = scene.my.spots关卡号 - 1;
scene.my.spots关卡号 < 1 ? {
timetolive = 0
} : {}
}
} : {}
}
```

## 开队（存在于跑毒，建议在19关开始时按下空格，方便回溯）。

1. ctrl+z。

2. 选中所有球，右键，脚本选单，在上面的输入框输入：`_B=10`

## 球全叠50名。

![2.3](https://raw.githubusercontent.com/xbcen/pic/main/picture/2.3.png "叠球的排行榜")

1. ctrl+z/调整排行榜。

2. 选中所有球，右键，选取，选取，选取圆形物件。

3. 脚本选单，在ondie中输入：`(e)=>{scene.my.num = scene.my.num - 1}`

## 球排名中间空一位。
![2.4](https://raw.githubusercontent.com/xbcen/pic/main/picture/2.4.png "排名之间空一位的排行榜")

1. ctrl+z/调整排行榜。

2. 选中所有球，右键，选取，选取，选取追踪绘图器。

3. 脚本选单，在ondie中输入：`(e)=>{}`

## 圆周运动。

成因：球和障碍物黏附在一起，导致球跟着障碍物圆周运动/不动。

解决方法：选中球，右键，几何行为，松开。

## 叠球排行榜不显示名字

选中所有球，右键，脚本选单，在上面的输入框输入：`_name = materialname`

## 记忆体溢位（请做好心理准备）。

成因：回收站里东西太多了？

1. 复制自己没保存的东西，粘贴到记事本里。

2. 打开自己的图。

3. 复制记事本里的内容，粘贴到Algodoo中。

> 如果有作图的需求，建议更新Algodoo版本至2.2.0或以上。