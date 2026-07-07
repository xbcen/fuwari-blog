---
title: Algodoo警示录
published: 2026-01-21
updated: 2026-06-28
description: 'Algodoo好像有点似了……'
image: ''
tags: ["Algodoo","Bug"]
category: 'Algodoo'
draft: false
lang: ''
path: 'algodoo-die'
---

好的不知道多久了，更新一下。

:::caution
本章的内容可能存在使你的Algodoo出现丢失数据等问题，请谨慎尝试。  
如果造成数据丢失等问题，我方概不负责。
:::

# Algodoo自带的：

1. 按下 <kbd>ctrl</kbd>+<kbd>Q</kbd>——退出Algodoo快捷键。

2. 在控制台或其他地方输入 `sim.exit`—— 退出Algodoo代码。

3. 在控制台或其他地方输入`scene.clear`——清空所有物件（可以<kbd>ctrl</kbd>+<kbd>Z</kbd>撤回）

# Algodoo Bug：

1. 在poststep或其他地方输入：`zDepth=a`（其中`a`为已经出现过的整数），恭喜你，闪退了。

# 电脑：这把高端局

1. 在 poststep/update直接写：`scene.addxxx ({})`。

2. 一直不保存（这个在哪里都是大忌）。