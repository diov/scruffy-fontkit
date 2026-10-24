# Scruffy FontKit

[中文说明](README.zh-CN.md)

A [Nexus](https://raidcore.gg/Nexus) addon for Guild Wars 2 that keeps text sharp with the game's DPI Scaling on, or replaces the game font with one you choose.

## Installation

1. Install [Nexus](https://raidcore.gg/Nexus) and close the game.
2. Download `scruffy-fontkit.dll` from [Releases](https://github.com/diov/scruffy-fontkit/releases) and put it in `<Guild Wars 2>\addons\`.
3. Start the game and open the addon's options (Nexus → Addons → Scruffy FontKit).
4. Choose **The game's own fonts, sharper**, or **My font** and pick a font file (for example `NotoSansSC-Medium.ttf`; the file decides the weight, such as `-Medium` or `-Bold`), then click **Build font pack**. It builds in the background in a few minutes and is used as soon as it is built, without a restart. To choose when, untick **Use the new font pack as soon as it is built** and click **Use** next to it later. Packs built in the same session stay in that list, so you can switch between them without building again.

Build again after changing the font or the Windows display scale, or when the addon shows a message in game.

Upgrading from 0.2.x: Nexus updates the addon, and your font pack keeps working. You can delete `scruffy-fontkit-builder.exe`.

## Known issues

- Icons and other UI images stay blurry.
- With your own font, bold and serif text use that same font.
- A few accented letters are one size smaller.
- From a font collection (`.ttc`), only the first font is used.

## Reporting problems

Open an [issue](https://github.com/diov/scruffy-fontkit/issues) with `addons\Nexus\Nexus.log`, and `generate.log` and `font-report.tsv` from `addons\scruffy-fontkit\`.

For stutter, turn on **Debug** in the addon's options (Nexus → Addons → Scruffy FontKit). It logs frame times to `Nexus.log` and stays on until you turn it off. After it stutters, attach `Nexus.log` before you start the game again, since the game overwrites it.

## Notes

Do not share your font pack, because it contains data from the game files. Use this addon at your own risk; see ArenaNet's [third-party program policy](https://help.guildwars2.com/hc/en-us/articles/360013625034).

[LICENSE](LICENSE) · [Third-party notices](THIRD_PARTY_NOTICES.txt)
