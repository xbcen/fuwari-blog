---
title: Algodoo警示录
published: 2026-01-21
description: ''
image: ''
tags: ["Algodoo","Bug"]
category: 'Algodoo'
draft: false
lang: ''
---

好的不知道多久了，更新一下。

>[!CAUTION]
>本章的内容可能存在使你的 Algodoo 出现丢失数据等问题，请谨慎尝试。
>如果造成数据丢失等问题，我方概不负责。

# Algodoo 自带的：

1. 按下 Ctrl+Q—— 退出 Algodoo 快捷键。

2. 在控制台或其他地方输入 `sim.exit`—— 退出 Algodoo 代码。

3. 在控制台或其他地方输入`scene.clear`——清空所有物件（可以Ctrl+z撤回）

# Algodoo Bug：

1. 在 poststep 或其他地方输入：`zDepth=a`（其中a为已经出现过的整数），恭喜你，闪退了。

# 电脑：这把高端局

1. 在 poststep/update 直接写：`scene.addxxx ({})`。

2. 一直不保存（这个在哪里都是大忌）。