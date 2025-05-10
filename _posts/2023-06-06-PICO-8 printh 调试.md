---
layout: post
tags: 游戏 开发 PICO-8
title: PICO-8 printh 调试
---

`printh` 与 `print` 是两个完全不同的打印函数。`print` 将内容输出到 PICO-8 自身的控制台，而 `printh` 将内容输出到外部控制台，或者保存为文本文档。这对于游戏调试来说更加方便，因为在游戏运行时，游戏界面和内部控制台无法同时显示。

## printh 简介

`printh` 接受的参数如下：

```
printh(str, [filename], [overwrite], [save_to_desktop])
```

str 参数是必须的，后三个参数是可选的。

- str 输出的信息
- filename 有此参数时信息将被保存到宿主系统的文件中（默认路径为当前目录，使用 folder 命令查看）
- overwrite 设置为 true 时，该文件的内容在每次输出时被覆盖，而不是附加。
- save_to_desktop 设置为 true 时，会保存到宿主系统的桌面，而不是当前目录。

## 系统设置

在 Linux 或者 Mac 上通过 shell 启动 PICO-8 时，不使用 filename 参数即可在外部 shell 里看到 printh 实时打印的内容。

而在 Windows 上一般只能通过 PICO-8 的 exe 程序运行，所以需要进行一些额外的设置：

- 创建一个 PICO-8 的快捷方式；
- 在快捷方式的“属性-快捷方式-目标”中，将路径修改为 `cmd /c 原路径` （注意空格）；
- （可选）点击更改图标，找到原路径下的exe文件并点击，将此快捷方式的图标改回PICO-8 的图标；
- 通过此快捷方式启动 PICO-8，就会在启动PICO-8时打开一个外部控制台；
- 此后使用 printh 打印的信息会显示在随之启动的控制台里；

![cmd /c](/assets/20230707a.png)

## 测试

在 PICO-8 的代码编辑器中输入如下代码：

```
printh('world')
```

运行以上代码，则可见 printh 输出到外部控制台。

![printh](/assets/20230707b.png)

## 使用 VSCode 编辑器的简便方法

如果你使用 VSCode 编辑器，你还可以直接将 PICO-8 的快捷方式拖放到 VSCode 的终端里，使 printh 直接输出到 VSCode 终端：

![printh with vscode](/assets/20230707c.gif)