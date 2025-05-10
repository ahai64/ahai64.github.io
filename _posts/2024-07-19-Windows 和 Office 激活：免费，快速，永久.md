---
layout: post
tags: 技术 windows
title: Windows 和 Office 激活：免费，快速，永久
---
**通过 Microsoft Activation Scripts (MAS) 项目提供的激活脚本，仅需一条命令就可以激活 Windows 和 Office！**

1. 右键点击开始按钮，打开 PowerShell（注意不是cmd）
2. 复制以下代码并粘贴进去，按回车。

```shell
irm https://get.activated.win | iex
```

3. 你会看到一系列激活选项
    ![](/assets/20240719.png)
4. 按你需要激活的选项就行了：
    1. 扣1~~送地狱火~~永久激活 Windows
    2. 扣2永久激活Office
    3. 扣3激活Windows到2038年（哈哈，前提是你电脑能用到那个时候）
    4. 扣4同时激活Windows+Office（半年有效期）
5. 就这样

该脚本的原理大致是：通过伪装成微软官方的认证服务器，欺骗你的系统【这台电脑已经被激活啦！】，然后你的系统就相信了，并把你的主板标记为已经激活，以后重装这台电脑的系统也会自动激活 Windows。

从此，主题可以自定义了，右下角不会显示水印了，生活变得更加美好了。

这里是该项目的 Github 仓库和主页：

[massgravel/Microsoft-Activation-Scripts](https://github.com/massgravel/Microsoft-Activation-Scripts)

[Microsoft Activation Scripts (MAS)](https://massgrave.dev/)