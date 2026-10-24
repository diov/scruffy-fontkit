# Scruffy FontKit（小邋遢字体工具）

[English](README.md)

激战 2 的 [Nexus](https://raidcore.gg/Nexus) 插件：让游戏开启 DPI 缩放后文字依然清晰，或者把游戏字体换成你指定的字体。

## 安装

1. 装好 [Nexus](https://raidcore.gg/Nexus)，关闭游戏。
2. 从 [Releases](https://github.com/diov/scruffy-fontkit/releases) 下载 `scruffy-fontkit.dll`，放进 `<游戏目录>\addons\`。
3. 启动游戏，打开插件的选项（Nexus → Addons → Scruffy FontKit）。
4. 选择 **The game's own fonts, sharper**（保持原版字体），或者 **My font** 并选一个字体文件（例如 `NotoSansSC-Medium.ttf`；字重由所选文件决定，例如 `-Medium`、`-Bold`），然后点 **Build font pack**。字体包在后台生成，需要几分钟，生成完马上生效，不用重启。想自己挑时机，就取消勾选 **Use the new font pack as soon as it is built**，之后在列表里点它旁边的 **Use**。同一局里生成过的字体包都留在这个列表里，可以来回切换，不用重新生成。

更换字体、调整 Windows 显示缩放，或者游戏里出现插件提示时，需要重新生成。

从 0.2.x 升级：Nexus 会自动更新插件，现有的字体包可以继续使用。`scruffy-fontkit-builder.exe` 可以删掉了。

## 已知问题

- 图标等界面图片仍然模糊。
- 使用指定字体时，粗体、衬线体也会显示为该字体。
- 少数带重音符号的字母会小一号。
- 字体集合文件（`.ttc`）只使用其中的第一个字体。

## 反馈问题

在 [Issues](https://github.com/diov/scruffy-fontkit/issues) 提交，附上 `addons\Nexus\Nexus.log`，以及 `addons\scruffy-fontkit\` 里的 `generate.log` 和 `font-report.tsv`。

如果遇到卡顿，请在插件的选项里打开 **Debug**（Nexus → Addons → Scruffy FontKit），它会把帧时间记到 `Nexus.log`，关掉之前一直有效。卡顿出现后，请在下次启动游戏前提交 `Nexus.log`，因为启动游戏时它会被覆盖。

## 说明

不要分享生成的字体包，里面有游戏文件的数据。使用风险自负，参见 ArenaNet 的[第三方程序政策](https://help.guildwars2.com/hc/en-us/articles/360013625034)。

[LICENSE](LICENSE) · [第三方声明](THIRD_PARTY_NOTICES.txt)
