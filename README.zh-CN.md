# Scruffy FontKit（小邋遢字体工具）

[English](README.md)

激战 2 的 [Nexus](https://raidcore.gg/Nexus) 插件：开启 DPI 缩放后文字依然清晰，或者把游戏字体换成你喜欢的字体。

![DPI 缩放 175% 下的文字：左边是原版，右边是 Scruffy FontKit](images/compare-175.jpg)

## 安装

1. 装好 [Nexus](https://raidcore.gg/Nexus)，关闭游戏。
2. 从 [Releases](https://github.com/diov/scruffy-fontkit/releases/latest) 下载 `scruffy-fontkit.dll`，放进 `<游戏目录>\addons\`。之后 Nexus 会自动更新插件。

## 使用

在 Nexus → Addons → Scruffy FontKit 里：

1. 选 **Game font**（DPI 缩放下让原版字体清晰），或者选 **My font** 和一个字体文件。
2. 点 **Build font pack**。生成需要几分钟，完成后不用重启就生效。

英文字母和原版一样大，汉字不小于原版。调整 Windows 显示缩放后，或者插件提示时，需要重新生成。

## 国服：界面大小 4 档

国服的界面大小只有两档。在插件选项里勾上 **4 interface sizes (CN client)**（默认关闭）并重启游戏，就有小、普通、大、更大四档。代价是全角标点（，：！（）等）会变宽，普通档的部分汉字会比原来小一点。取消勾选并重启就恢复；如果游戏选项里的界面大小显示空白，重新选一次即可。

## 已知问题

- 图标等界面图片仍然模糊。
- 使用自己的字体时，粗体、衬线体也会显示为该字体。
- 字体集合文件（`.ttc`）只使用其中的第一个字体。

## 反馈问题

在 [Issues](https://github.com/diov/scruffy-fontkit/issues) 提交，附上 `addons\Nexus\Nexus.log`，以及 `addons\scruffy-fontkit\` 里的 `generate.log` 和 `font-report.tsv`。如果遇到卡顿，先在插件选项里打开 **Debug**，卡顿出现后在下次启动游戏前提交 `Nexus.log`，因为启动游戏时它会被覆盖。

## 免责声明

不要分享生成的字体包，里面有游戏文件的数据。使用风险自负，参见 ArenaNet 的[第三方程序政策](https://help.guildwars2.com/hc/en-us/articles/360013625034)。

[LICENSE](LICENSE) · [第三方声明](THIRD_PARTY_NOTICES.txt)
