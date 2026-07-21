---
title:  Algodoo plus：数据类型
published: 2026-07-20
updated: 2026-07-20
description: '最没底的一集。'
image: './assets/cover/Algodoo-plus4.png'
tags: ["Algodoo","Algodoo plus"]
category: 'Algodoo'
draft: false 
lang: ''
path: 'algodoo-plus4'
pinned: false
---

# 数据类型

Algodoo中定义变量并不需要声明变量的数据类型。  
直接`变量=值`即可。

> [!WARNING]
> 但为了减少Bug、提高可读性，请不要混淆变量的数据类型。

## 整数（Int）

在$-2^{31}$到$2^{31}-1$范围内的整数。

例如`-1`、`20260720`、`1e10`。

## 浮点数（Float）

有小数部分的实数，提供6到9位有效数字的精度。

例如`1.1`、`5.0`、`3.1415927`、`+inf`。

> `+inf`、`-inf`为的数据类型为`Float`。  
> `正数 / 0.0 = +inf`  
> `负数 / 0.0 = -inf`  
> `0.0 / 0.0 = NaN`  
> `整数 / 0`会报错。

> [!NOTE]
> 请区分好`Float`与`Int`。
> 
> `Int / Int`时，结果仍为`Int`。

```bash showLineNumbers=false title="举例"
> 5 / 3
1
> 5.0 / 3
1.6666666
> 5 / 3.0
1.6666666
> 5.0 / 3.0
1.6666666
```

## 字符串（String）

表示文本信息。

例如`"Hello, World!"`、`"111"`。

字符串可以被视为一种特殊的数组，其与数组的部分特性相通。  
例如`string.length()`。

## 布尔值（Bool）

只有`true`（真）与`false`（假）。

如`list(1) == 12`、`14 > -1`、`true && false`的结果。

主要用于判断。

## 数组（Array）

参见[数组](/posts/algodoo-plus3/)

## 其他数据类型

### undefined

未定义的变量。

### null

空值。

如在物件脚本选单的输入框或控制台的`entity`。

### NaN（Not a Number）

表示未定义或不可表示的数值。

如`+inf - +inf`、`0.0 / 0.0`、`math.sqrt(-1)`、`NaN - NaN`的结果。

# 数据类型转换

`Int`、`Bool`、`String（数字字符串）`转`Int`：`math.toint()`。

`Int`、`Bool`、`String（数字字符串）`转`Float`：`math.tofloat()`。

`Int`、`Float`转`Bool`：`math.tobool()`。  
（0返回`true`，除0以外返回`true`）

任意数据类型直接转`String`：`任意数据类型 + ""`或`math.toString()`。

`Array`转`String`：`string.list2str()`

```bash showLineNumbers=false title="举例"
> string.list2str([1, 1, 1, 2])
1112
```

`String`转`Array`：`string.str2list()`

```bash showLineNumbers=false title="举例"
> string.str2list("1112")
[1, 1, 1, 2]
```

# 实战环节

> 不用if判断、三目运算符（?{}:{}），实现以下代码：

```
e.other._toubi ? {
    _aa = "已投币；"
} : {
    _aa = "未投币；"
};
e.other._dianzan ? {
    _cc = "已点赞；"
} : {
    _cc = "未点赞；"
};
e.other._shoucang ? {
    _bb = "已收藏；"
} : {
    _bb = "未收藏；"
};
```

1. 回顾[上次学的](/posts/algodoo-plus3/)，分别创建数组。

```js
["未投币；", "已投币；"]
["未收藏；", "已收藏；"]
["未点赞；", "已点赞；"]
```

2. 理解一下代码：我们要在`e.other._shoucang == true`时返回已收藏；  
`e.other._shoucang == false`时返回未收藏。

3. 注意到，`math.toint(true) == 1`；  
`math.toint(false) == 0`  
对应第1步中数组的两个下标。

4. 所以有：

```js
_aa = ["未投币；", "已投币；"](math.toint(e.other._toubi));
_bb = ["未收藏；", "已收藏；"](math.toint(e.other._shoucang));
_cc = ["未点赞；", "已点赞；"](math.toint(e.other._dianzan));
```

5. 完毕。