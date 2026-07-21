---
title: Algodoo Plus：数组
published: 2026-06-27
updated: 2026-07-21
description: '登 神 长 阶'
image: './assets/cover/Algodoo-plus3.png'
tags: ["Algodoo","数据类型"]
category: 'Algodoo Plus'
draft: false 
lang: ''
path: 'algodoo-plus3'
---

# 数组的概念

> 数组是一种基本的数据结构，其中每个**元素**可以通过**下标/索引**来访问。

**元素**为数组的基本组成部分。  
**下标/索引**是用于标识数组中元素位置的数字。一般地，数组下标从0开始。

设数组`a`为`[1, 2, 3]`。  
其中`1`、`2`、`3`就是数组`a`中的**元素**。  
`1`为数组`a`的第0项。

# Algodoo中的数组

## 数组的读取

Algodoo中，同一数组的元素可以为不同的数据类型。

读取数组的下标采用`数组(下标)`。

例如：`a = [111,"laocha"]`。  
则`a(0)`返回`111`。

## 数组的修改

数组的元素不可以直接单独被修改。

例如：`a = [111, "laocha"]`。  
不能直接`a(0) = 222`.

```js title="正确格式"
a = [222, a(0)]
```

> 神人Thyme，这功能也不给。
> 
> 只能自己动手，丰衣足食了。

```js title="修改数组某一项的函数"
scene.my.changearray = (array, count, value)=>{
    arrayre = [];
    for(string.length(array), (i)=>{
        count == i ? {
            arrayre = arrayre ++ [value]
        } : {
            arrayre = arrayre ++ [array(i)]
        }
    });
    arrayre
};
```

其中  
- `array`：需要更改的数组  
- `count`：更改元素的下标  
- `value`：更改后该元素的值

最终该函数返回更改后的数组。

---

若需加减乘除数组的元素，需要一一对应。

例如：`a = [111, "laocha"]`。  
若需修改`111`为`222`，则应这么写：

```js title="正确格式"
a = a + [111, ""]
```

---

可以通过`++`向数组添加元素。


```bash showLineNumbers=false title="举例"
> a = ["array", "1"]
["array", "1"]
> a = a ++ [4]
[array, 1, 4]
```

# 数组的用法（实战环节）

> 在灰安教主的模板中，排行会根据该排行小球的`_teamcolor`而变化。  
> 那如何在只有`_team`（1-10之间的正整数），通过修改排行的`oncollide`来改变排行的颜色呢？

<details>
<summary>有一种实现方法如下所示（点击右边小三角展开）</summary>

```
(e)=>{
    e.other._team == 1 ? {
        textcolor = [1, 0, 0, 1]
    } : {
        e.other._team == 2 ? {
            textcolor = [1, 0.5, 0, 1]
        } : {
            e.other._team == 3 ? {
                textcolor = [1, 1, 0, 1]
            } : {
                e.other._team == 4 ? {
                    textcolor = [0, 0.5, 0, 1]
                } : {
                    e.other._team == 5 ? {
                        textcolor = [0, 1, 1, 1]
                    } : {
                        e.other._team == 6 ? {
                            textcolor = [0, 0, 1, 1]
                        } : {
                            e.other._team == 7 ? {
                                textcolor = [0.5, 0, 1, 1]
                            } : {
                                e.other._team == 8 ? {
                                    textcolor = [1, 0.5, 1, 1]
                                } : {
                                    e.other._team == 9 ? {
                                        textcolor = [1, 1, 1, 1]
                                    } : {
                                        poststep = (e)=>{
                                            textcolor = scene.my.rainbow
                                        }
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
```
</details>

但这种方法显然不够优雅，也不太适合人阅读（？），那如何用数组的方式处理呢？

## 首先处理非闪队（`_team`为1-9）部分

设变量

```js
_color = [[1, 0, 0, 1], [1, 0.5, 0, 1], [1, 1, 0, 1], [0, 0.5, 0, 1], [0, 1, 1, 1], [0, 0, 1, 1], [0.5, 0, 1, 1], [1, 0.5, 1, 1], [1, 1, 1, 1]]
```

也就是9个队按顺序的`_teamcolor`。

因为`_team`从1开始，而数组下标从0开始。
所以读取`_color`的元素时，下标为`e.other._team - 1`。

故有以下代码： 

```js
textcolor = _color(e.other._team - 1);
```

## 处理闪队（`_team == 10`）部分

当队伍为闪队时，我们采用彩虹的代码，即

```
poststep = (e)=>{
    textcolor = scene.my.rainbow
}
```

## 整合代码

判断小球是否为闪队，然后分别走对应的逻辑。

```
(e)=>{
    e.other._team != 10 ? {
        textcolor = _color(e.other._team - 1)
    } : {
        poststep = (e)=>{
            textcolor = scene.my.rainbow
        }
    }
}
```

最后，这个问题就被数组愉快地解决了。