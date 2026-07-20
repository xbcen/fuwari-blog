---
title:  Algodoo plus：数据类型
published: 2026-07-20
description: '最没底的一集。。。。'
image: './assets/cover/Algodoo-plus4.png'
tags: ["Algodoo","Algodoo plus"]
category: 'Algodoo'
draft: false 
lang: ''
path: Algodoo-plus4
pinned: false
---

# 数据类型

Algodoo中定义变量并不需要声明变量的数据类型。  
直接`变量=值`即可。

## 整数（Int）

在$-2^{31}$到$2^{31}-1$范围内的整数。

例如`-1`、`20260720`、`1e10`。

## 浮点数（Float）

有小数部分的实数，提供6到9位有效数字的精度。

例如`1.1`、`5.0`、`3.1415927`、`+inf`。

> `+inf`、`-inf`为的数据类型为`float`。  
> `正数 / 0.0=+inf`  
> `负数 / 0.0=-inf`  
> `0.0 / 0.0=NaN`  
> `整数 / 0`会报错。

## 字符串（String）

表示文本信息。

例如`"Hello, World!"`、`"111"`。

## 布尔值（Bool）

只有`true`（真）与`false`（假）。

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

表示未定义或不可表示的值。

如`+inf - +inf`、`0.0 / 0.0`、`math.sqrt(-1)`、`NaN - NaN`的结果。

# 数据类型转换

# 实战环节