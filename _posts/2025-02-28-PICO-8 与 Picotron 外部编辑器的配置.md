---
layout: post
tags: 游戏 开发 PICO-8
title: PICO-8 与 Picotron 外部编辑器的配置
---

PICO-8 与 Picotron 都自带代码编辑器，但功能都比较基础。
好在作者预留了支持外部编辑器的特性，通过简单地配置就可以在外部编辑器中编写代码，并在 PICO-8 或 Picotron 中即时运行。

## 实现原理

PICO-8 和 Picotron 的原始卡带文件的本质都是文本文件，都可以在任何文本编辑器中打开并编辑。

但我并不推荐这样做，因为在外部编辑器和原生编辑器中对卡带都有改动，那么一旦运行就会因为冲突而报错。

将代码全部放到外部Lua文件中，美术音乐等资源在卡带文件中，两边分开编辑互不影响，运行时通过 `include` 功能从卡带调用外部代码，这样做才是更安全可靠的做法。

## 下载安装 VSCode 及其 Lua 扩展

https://code.visualstudio.com/

https://marketplace.visualstudio.com/items?itemName=sumneko.lua

## 下载安装 pico8 和 picotron 插件

https://github.com/ahai64/pico8

https://github.com/ahai64/picotron

下载，解压，并将对应的项目中的 `.vscode` 和 `library` 文件夹放到你项目所在的文件夹，就可以启用插件。

## 新建卡带和Lua文件

在VSCode的工作区中新建 `main.lua` 文件，同时通过 PICO-8/Picotron 的 `save` 命令在该位置新建一个卡带，并在卡带的代码编辑器中输入以下内容：

PICO-8:

```lua
#include main.lua
```

Picotron:

```lua
include("main.lua")
```

注意 Picotron 卡带的**运行的路径**并不是卡带**文件的路径**，读取 `main.lua` 文件是从运行路径出发的。

必须正确设置 Picotron 运行路径，并使用 `cd()` 命令导航到 `main.lua` 的路径才能正常运行。

Picotron 的运行路径一般在 `C:\Users\{UserName}\AppData\Roaming\Picotron\picotron_config.txt` 中设置。

## 开始玩耍！

按照上述步骤正确操作，你将在 VSCode 得到如下工作区：

```
|-.vscode
| |-settings.json
|-library
| |-audio.lua
| |-...
|-main.lua
|-mygame.p8
```

现在，你可以在 VSCode 的工作区中编写代码，并享受代码提示，格式，AI辅助等各种丰富的功能了！
