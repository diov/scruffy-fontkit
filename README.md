# Scruffy FontKit

[中文说明](README.zh-CN.md)

A [Nexus](https://raidcore.gg/Nexus) addon for Guild Wars 2 that keeps text sharp with the game's DPI Scaling on, or replaces the game font with one you choose.

## Installation

1. Install [Nexus](https://raidcore.gg/Nexus) and close the game.
2. Download `scruffy-fontkit-vX.Y.Z.zip` from [Releases](https://github.com/diov/scruffy-fontkit/releases).
3. Put `scruffy-fontkit.dll` in `<Guild Wars 2>\addons\`, and `scruffy-fontkit-builder.exe` in `<Guild Wars 2>\addons\scruffy-fontkit\`.
4. Run the builder to generate the font pack:
   - double-click it to keep the stock font, or
   - drag a font file onto it to use that font (for example `NotoSansSC-Medium.ttf`).

Run the builder again after changing the font or the Windows display scale, or when the addon shows a message in game. If the message says the font pack is outdated, download the latest release first.

## Known issues

- Icons and other UI images stay blurry.
- With your own font, bold and serif text use that same font.
- A few accented letters are one size smaller.

## Reporting problems

Open an [issue](https://github.com/diov/scruffy-fontkit/issues) with `addons\Nexus\Nexus.log` and `addons\scruffy-fontkit\font-report.tsv`.

For stutter, turn on **Debug** in the addon's options (Nexus → Addons → Scruffy FontKit). It logs frame times to `Nexus.log` and stays on until you turn it off. After it stutters, attach `Nexus.log` before you start the game again, since the game overwrites it.

## Notes

Do not share your font pack, because it contains data from the game files. Use this addon at your own risk; see ArenaNet's [third-party program policy](https://help.guildwars2.com/hc/en-us/articles/360013625034).

[LICENSE](LICENSE) · [Third-party notices](THIRD_PARTY_NOTICES.txt)
