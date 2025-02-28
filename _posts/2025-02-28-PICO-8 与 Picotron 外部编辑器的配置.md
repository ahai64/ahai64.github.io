---
layout: post
tags: 游戏 开发 PICO-8
title: PICO-8 与 Picotron 外部编辑器的配置
---

PICO-8 与 Picotron 都自带代码编辑器，但是功能都比较基础。好在作者预留了支持外部编辑器的 feature，通过一点配置，就可以在外部编辑器中编写代码，同时在 PICO-8 或 Picotron 中即时运行。

## 实现原理

PICO-8 和 Picotron 的原始卡带文件本质都是文本文件，都可以在任何文本编辑器中打开并编辑。

但是我并不推荐这样做，因为在其他编辑器和原生编辑器中如果都有修改，那么在运行卡带时就会因为改动冲突而报错。

将代码全部放到外部Lua文件中，美术音乐等资源在卡带文件中，两边分开编辑，运行时通过 `include` 功能调用外部代码，这样做才是更安全可靠的做法。

PICO-8（Lua 文件和 p8 文件须在同一目录）:

```lua
#include main.lua
```

Picotron（相比PICO-8，Picotron可以通过 `cd` 命令将工作目录切换到 Lua 文件所在目录）:

```lua
cd("/myproj")
include("main.lua")
```

## 下载安装 VSCode 和 Lua 扩展

https://code.visualstudio.com/

https://marketplace.visualstudio.com/items?itemName=sumneko.lua

## 下载 pico8 和 picotron 插件

https://github.com/ahai64/pico8

https://github.com/ahai64/picotron

下载，解压，并将对应的项目中的 `.vscode` 和 `library` 文件夹放到你项目所在的文件夹，就可以启用插件。

> 后续将会支持通过 Lua Addon Manager 一键安装启用，但这要取决于 LLS 官方何时能修复无法加载设置的问题。

## 开始玩耍！

现在，你可以在VSCODE的工作区中编写代码，并享受代码提示，格式，AI副词等各种丰富的功能了！
