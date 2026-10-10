# Scruffy FontKit（小邋遢字体工具）

[English](README.md)

激战 2（Guild Wars 2）的 [Nexus](https://raidcore.gg/Nexus) 插件，替换游戏的位图字体。有两种用法：

- **指定字体**：所有字形，包括汉字和拉丁字母，都换成用你选的字体渲染的字形。
- **原版清晰化**：不需要字体。打开游戏的 *DPI Scaling*（DPI 缩放）后，游戏会把小号位图字体放大，文字发虚。builder 按你的 Windows 显示缩放，重新渲染原版字形所用的字体：拉丁字母用它在 `Gw2.dat` 里找到的字体，汉字用 Windows 的黑体（SimHei）和宋体（SimSun）。字形和原版一样，但是清晰。

字体包在你自己的电脑上、用你自己的游戏数据生成，不分发任何字体包。

## 需要什么

- 装好 [Nexus](https://raidcore.gg/Nexus) 的激战 2。
- 只有*指定字体*需要：一个 TrueType/OpenType 字体（`.ttf`、`.otf` 或 `.ttc`）。推荐 **思源黑体 Medium**（`NotoSansSC-Medium.ttf`，SIL Open Font License），粗细和原版字形接近。请只使用你有权使用的字体。

从 [Releases](https://github.com/diov/scruffy-fontkit/releases) 下载 `scruffy-fontkit-vX.Y.Z.zip`。zip 里有：

| 文件 | 用途 |
|---|---|
| `scruffy-fontkit.dll` | Nexus 插件 |
| `scruffy-fontkit-builder.exe` | 从 `Gw2.dat`（和你的字体）生成字体包 |
| `README.md`、`README.zh-CN.md`、`LICENSE`、`THIRD_PARTY_NOTICES.txt` | 说明和许可 |

## 安装

1. 关闭游戏。
2. 把 `scruffy-fontkit.dll` 复制到 `<游戏目录>\addons\`。
3. 新建文件夹 `<游戏目录>\addons\scruffy-fontkit\`，把 `scruffy-fontkit-builder.exe` 复制进去。
4. 生成字体包（见下一节）。

游戏目录取决于你怎么安装的游戏；Steam 版通常是 `C:\Program Files (x86)\Steam\steamapps\common\Guild Wars 2`。就是放着 `Gw2.dat` 的那个文件夹。

发布新版本后，Nexus 会自动更新插件，但不会更新 builder：插件提示字体包过时的时候，下载最新的 zip，替换两个文件，再重新生成字体包。

## 生成字体包

先关闭游戏：builder 要读 `Gw2.dat`，而游戏运行时会一直占用 `font.pack`。

- **原版清晰化**：双击 `scruffy-fontkit-builder.exe`。
- **指定字体**：把字体文件拖到 `scruffy-fontkit-builder.exe` 上。

builder 在自己上两级目录里找 `Gw2.dat`，把 `font.pack` 和 `font-report.tsv` 写在自己旁边，结束后等你按回车再关窗口。之后再启动游戏。换了字体或 Windows 显示缩放后，要重新生成字体包。

字体包按你当前的 Windows 显示缩放生成。*指定字体*在 100% 下要一到两分钟，写出约 265 MiB；每多一档缩放多几分钟、几百 MiB（175% 多约 525 MiB）。*原版清晰化*的拉丁字母一次覆盖 125% 到 350% 的所有缩放（约 280 MiB），所以改 Windows 缩放不用为它重新生成；汉字只按当前缩放生成（175% 时约 530 MiB）。

### 命令行

要用其它设置，在 builder 所在的文件夹打开 PowerShell，运行

```powershell
.\scruffy-fontkit-builder.exe [--gw2 <游戏目录>] [--font <文件> [--face <n>]] [--dpi-scale <百分比>[,<百分比>...]]
```

- `--gw2`：游戏目录，builder 不在 `<游戏目录>\addons\scruffy-fontkit\` 里时用。字体包仍然写到 `<游戏目录>\addons\scruffy-fontkit\font.pack`。
- `--font`：*指定字体*用的字体；不填就是*原版清晰化*。
- `--face`：字体文件里的第几个字体。`.ttc` 字体集里有多个字体，从 `0` 开始编号；默认是 `0`。
- `--dpi-scale`：打开游戏的 *DPI Scaling* 后，游戏按 Windows 显示缩放放大文字，所以会发虚；builder 会额外按这个缩放渲染字形，插件用这些字形来画。默认是这台电脑当前的缩放（例如 175% 就是 `175`）。要自己指定，例如几台显示器缩放不同时，用百分比列出来：`--dpi-scale 150,175`；`--dpi-scale 100` 只生成标准的一套。

### *原版清晰化*是怎么做的

- builder 把游戏的每种字体和 `Gw2.dat` 里存的字体比较，拉丁字母能对上的就重新渲染。汉字按样式和 Windows 字体目录里的黑体、宋体比较（游戏正文用黑体，标题用加粗的宋体），也重新渲染。`font-report.tsv` 开头是这两份比较结果，builder 也会列出每种汉字样式用了哪个字体。只有黑体和宋体都装了才会重新渲染汉字：所有 Windows 都带宋体，但黑体在可选功能 *Chinese (Simplified) Supplemental Fonts*（设置 > 系统 > 可选功能）里，添加中文语言时 Windows 会自动装上。缺一个时，汉字按*已知局限*里说的方式放大。
- 100% 时用游戏自己的字形。只有打开游戏的 *DPI Scaling* 才有区别。

## 确认是否生效

需要重新生成字体包时，插件每局会在屏幕上提示一次，例如 `Scruffy FontKit: no font pack.` 或 `Scruffy FontKit: the font pack has no glyphs for 150% display scale.`。关掉游戏，重新运行 builder。

详细情况看 Nexus 日志。应该能看到 Scruffy FontKit 的这些行：

- `font pack loaded: scales …`（字体包包含的缩放）
- `font hooks installed`
- `display-scale hooks installed`
- 打开 *DPI Scaling* 时：`display scale 175%: drawing fonts with the 175 glyph variant`（数字是你的缩放）
- *原版清晰化*时，字体包没覆盖的文字第一次出现（例如聊天里的中文）：`upscaled file … at scale …`

如果看到 `no font pack loaded` 或 `invalid font pack`，检查 `font.pack` 是否在 `<游戏目录>\addons\scruffy-fontkit\` 里；旧版本生成的字体包要重新生成。如果看到 `the pack was built for other scales`，按当前的 Windows 缩放重新生成。如果看到 `game functions not resolved` 或 `font hooks not installed`，说明游戏有了这个版本不支持的变化，插件不会改动字体。

## 游戏更新之后

- 如果更新改了游戏的字体数据，受影响的字形会变回原版，插件提示 `the game has been updated since the font pack was built`，日志里有 `differs from the pack's source (game updated?)`。重新生成字体包。
- 如果更新改了游戏程序，插件找不到它要的函数，请等插件的新版本。

## 已知局限

- 打开游戏的 *DPI Scaling* 时，只有字体包里有当前 Windows 缩放的字形，文字才是清晰的。改了 Windows 缩放，或者把游戏挪到缩放不同的显示器上，要重新生成字体包（或用 `--dpi-scale` 加上那一档）；在那之前文字和原版一样发虚。图标和其它界面图片仍然由游戏放大。
- 打开 *DPI Scaling* 时，你的字体里没有的几个标点符号保持原版大小。
- 打开 *DPI Scaling* 时，中文和日文每行可能比关掉时少放一个字：放大后字宽要取整到整像素。
- 带重音的拉丁字母和一些符号会小一号，因为原版字体在大写字母上方留的空间很少。
- 中英混排时，拉丁大写字母和汉字差不多高，而且比汉字低几个像素。原版字体就是这样画的，两种模式都保持原版的字号和基线。聊天框里最后一行的下半部分（例如 `g` 的尾巴）可能被输入栏挡住，不装插件也一样。
- 启动器窗口（进游戏前登录账号的窗口）用的是它自己的字体，不会改变。
- *指定字体*时，所有样式（粗体、衬线体）都用你选的那一个字体。斜体样式和原版一样倾斜：拉丁字母倾斜，汉字保持直立，和游戏里一样。少数装饰字体的源字体不在 `Gw2.dat` 里，保持直立。
- *原版清晰化*时：
  - 界面和剧情字体里，拉丁字母能和 `Gw2.dat` 里的字体对上的会重新渲染；少数其它字体族和不装插件时一样发虚；
  - 汉字只在生成字体包时的 Windows 缩放下清晰；改了 Windows 缩放要重新生成；
  - 字体包没覆盖的文字（西里尔字母、大部分符号、韩文，以及其它缩放下的汉字）在第一次出现时平滑放大，游戏可能会短暂卡一下，每种字体占用几十 MiB 内存，直到退出游戏；
  - 少数圆形字母会窄一点，带重音的大写字母会小一点，为了放进原版的字距；
  - 有些装饰字体的原版字形混用了两种汉字字体，重新渲染后统一成一种。

## 合理使用

不要分享生成的字体包：里面有游戏文件的数据。

这个插件只改变文字的绘制方式。ArenaNet 的[第三方程序政策](https://help.guildwars2.com/hc/en-us/articles/360013625034)说，不会让一个玩家比其他玩家占优势的工具一般不会被处理，但这由 ArenaNet 决定。使用风险自负。

## 报告问题

提交一个 [issue](https://github.com/diov/scruffy-fontkit/issues)，附上 `<游戏目录>\addons\Nexus\Nexus.log` 和 `<游戏目录>\addons\scruffy-fontkit\font-report.tsv`；问题能看出来的话再附一张截图。不要附 `font.pack`。

## 许可

免费使用；可以分享未经修改的发布 zip。条款见 [LICENSE](LICENSE)。第三方组件及其许可列在 [THIRD_PARTY_NOTICES.txt](THIRD_PARTY_NOTICES.txt)。
