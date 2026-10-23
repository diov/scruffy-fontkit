# Scruffy FontKit（小邋遢字体工具）

[English](README.md)

激战 2 的 [Nexus](https://raidcore.gg/Nexus) 插件：让游戏开启 DPI 缩放后文字依然清晰，或者把游戏字体换成你指定的字体。

## 安装

1. 装好 [Nexus](https://raidcore.gg/Nexus)，关闭游戏。
2. 从 [Releases](https://github.com/diov/scruffy-fontkit/releases) 下载 `scruffy-fontkit-vX.Y.Z.zip`。
3. `scruffy-fontkit.dll` 放进 `<游戏目录>\addons\`，`scruffy-fontkit-builder.exe` 放进 `<游戏目录>\addons\scruffy-fontkit\`。
4. 运行 builder 生成字体包：
   - 双击：保持原版字体；
   - 把字体文件拖到它上面：换成这个字体（例如 `NotoSansSC-Medium.ttf`）。

更换字体、调整 Windows 显示缩放，或者游戏里出现插件提示时，需要重新运行 builder。如果提示字体包过时，先下载最新版本再运行。

## 已知问题

- 图标等界面图片仍然模糊。
- 使用指定字体时，粗体、衬线体也会显示为该字体。
- 少数带重音符号的字母会小一号。

## 反馈问题

在 [Issues](https://github.com/diov/scruffy-fontkit/issues) 提交，附上 `addons\Nexus\Nexus.log` 和 `addons\scruffy-fontkit\font-report.tsv`。

如果遇到卡顿，请在插件的选项里打开 **Debug**（Nexus → Addons → Scruffy FontKit），它会把帧时间记到 `Nexus.log`，关掉之前一直有效。卡顿出现后，请在下次启动游戏前提交 `Nexus.log`，因为启动游戏时它会被覆盖。

## 说明

不要分享生成的字体包，里面有游戏文件的数据。使用风险自负，参见 ArenaNet 的[第三方程序政策](https://help.guildwars2.com/hc/en-us/articles/360013625034)。

[LICENSE](LICENSE) · [第三方声明](THIRD_PARTY_NOTICES.txt)
