# Scruffy FontKit

[中文说明](README.zh-CN.md)

A [Nexus](https://raidcore.gg/Nexus) addon for the bitmap fonts of Guild Wars 2. It works in one of two ways:

- **Your own font**: every glyph, CJK and Latin, is replaced with glyphs rendered from a font you choose. Latin and Chinese share one size and baseline, so mixed text follows the proportions of your font; in chat and body text, Latin letters come out smaller than the stock ones.
- **Sharper stock text**: no font needed. With the game's *DPI Scaling* option on, the game enlarges its small bitmap fonts and the text looks blurry. The builder re-renders the fonts the stock glyphs were drawn from at your Windows display scale, so the text keeps its look but stays sharp: the Latin font it finds in `Gw2.dat`, and for Chinese text, SimHei and SimSun from Windows.

The font pack is generated on your own PC from your own game data. No font pack is distributed.

## What you need

- Guild Wars 2 with [Nexus](https://raidcore.gg/Nexus) installed.
- For *your own font* only: a TrueType/OpenType font (`.ttf`, `.otf` or `.ttc`). We recommend **Noto Sans SC Medium** (`NotoSansSC-Medium.ttf`, SIL Open Font License), which is close to the stock glyphs in weight. Only use fonts you are licensed to use.

Download `scruffy-fontkit-vX.Y.Z.zip` from [Releases](https://github.com/diov/scruffy-fontkit/releases). The zip contains:

| File | Purpose |
|---|---|
| `scruffy-fontkit.dll` | The Nexus addon |
| `scruffy-fontkit-builder.exe` | Generates the font pack from `Gw2.dat` (and your font) |
| `README.md`, `README.zh-CN.md`, `LICENSE`, `THIRD_PARTY_NOTICES.txt` | Documentation and licenses |

## Install

1. Close the game.
2. Copy `scruffy-fontkit.dll` into `<game folder>\addons\`.
3. Create the folder `<game folder>\addons\scruffy-fontkit\` and copy `scruffy-fontkit-builder.exe` into it.
4. Generate the font pack (next section).

Nexus updates the addon by itself when a new version is released. It does not update the builder: when the addon says the font pack is outdated, download the latest zip, replace both files and generate the pack again.

The game folder depends on how you installed the game; for Steam it is usually `C:\Program Files (x86)\Steam\steamapps\common\Guild Wars 2`. It is the folder that contains `Gw2.dat`.

## Generate the font pack

Close the game first: the builder reads `Gw2.dat`, and the game keeps `font.pack` open while it runs.

- **Sharper stock text**: double-click `scruffy-fontkit-builder.exe`.
- **Your own font**: drag the font file onto `scruffy-fontkit-builder.exe`.

The builder finds `Gw2.dat` two folders above itself, writes `font.pack` and `font-report.tsv` next to itself, and waits for Enter before its window closes. Start the game afterwards. Generate the pack again after changing the font or the Windows display scale.

The pack is built for your current Windows display scale. With *your own font* it takes one to two minutes at 100% and writes about 265 MiB; each extra scale adds several minutes and several hundred MiB (175% adds about 525 MiB). With *sharper stock text*, Latin text covers the Windows display scales 125% to 350% at once (about 280 MiB), so changing the Windows scale needs no new pack for it; Chinese text is rendered for your current scale only (about 530 MiB at 175%).

### Command line

To use other settings, open PowerShell in the builder's folder and run

```powershell
.\scruffy-fontkit-builder.exe [--gw2 <game folder>] [--font <file> [--face <n>]] [--dpi-scale <percent>[,<percent>...]]
```

- `--gw2`: the game folder, when the builder is not in `<game folder>\addons\scruffy-fontkit\`. The pack still goes to `<game folder>\addons\scruffy-fontkit\font.pack`.
- `--font`: the font for *your own font*; without it you get *sharper stock text*.
- `--face`: the face inside the font file. A `.ttc` collection holds several faces, numbered from `0`; the default is `0`.
- `--dpi-scale`: with the game's *DPI Scaling* option on, the game enlarges text by your Windows display scale, which makes it blurry, so the builder also renders the glyphs at that scale and the addon uses them. By default that is this PC's current scale (for example `175` for 175%). To pick the scales yourself, for example for monitors with different scales, list them as percents: `--dpi-scale 150,175`; `--dpi-scale 100` renders only the standard set.

### How *sharper stock text* works

- The builder compares each of the game's fonts with the fonts stored in `Gw2.dat` and re-renders those whose Latin letters it can match. It compares the Chinese characters with SimHei and SimSun from your Windows font folder, style by style (the game uses SimHei for body text and an emboldened SimSun for titles), and re-renders them too. `font-report.tsv` starts with both comparisons, and the builder lists which font each Chinese style got. Chinese text is re-rendered only when both are installed: every Windows has SimSun, but SimHei comes with the optional feature *Chinese (Simplified) Supplemental Fonts* (Settings > System > Optional features), which Windows adds with the Chinese language. Without both, Chinese text stays enlarged as described under *Known limitations*.
- At 100% the game's own glyphs are used. It only matters with the game's *DPI Scaling* option on.

## Check that it works

When the font pack needs to be generated again, the addon says so on screen once per session, for example `Scruffy FontKit: no font pack.` or `Scruffy FontKit: the font pack has no glyphs for 150% display scale.` Close the game and run the builder again.

For details, open the Nexus log. You should see, from Scruffy FontKit:

- `font pack loaded: scales …` (the scales the pack was built for)
- `font hooks installed`
- `display-scale hooks installed`
- with *DPI Scaling* on: `display scale 175%: drawing fonts with the 175 glyph variant` (with your scale)
- with *sharper stock text*, when text the pack does not cover appears for the first time (for example Chinese in chat): `upscaled file … at scale …`

If you see `no font pack loaded` or `invalid font pack`, check that `font.pack` is in `<game folder>\addons\scruffy-fontkit\`; packs from older versions must be generated again. If you see `the pack was built for other scales`, generate the pack again at your current Windows scale. If you see `game functions not resolved` or `font hooks not installed`, the game has changed in a way this version does not support; the addon leaves the fonts alone.

## After a game update

- If the update changes the game's font data, the affected glyphs show the stock font again, the addon says `the game has been updated since the font pack was built`, and the log says `differs from the pack's source (game updated?)`. Generate the pack again.
- If the update changes the game executable so that the addon can no longer find its functions, wait for a new addon version.

## Known limitations

- With the game's *DPI Scaling* enabled, text is sharp only if the pack has the variant for the current Windows scale. After changing the Windows scale or moving the game to a monitor with a different scale, generate the pack again (or add that scale with `--dpi-scale`); until then text looks blurry, like the stock fonts. Icons and other UI images are still enlarged by the game.
- With *DPI Scaling*, a few punctuation symbols that your font does not have stay at their stock size.
- With *DPI Scaling*, Chinese and Japanese lines may hold one character fewer than without it: glyph widths are rounded to whole pixels at the larger size.
- Some accented Latin letters and symbols are drawn one size smaller, because the stock fonts leave little room above capitals (fewer with *your own font*).
- Korean text keeps the stock glyphs.
- With *sharper stock text*, Latin capitals stay about as tall as Chinese characters in mixed text, as in the stock fonts. Where the stock Latin sits lower (chat and body text), Latin moves up and Chinese moves down by a few pixels so that both share a baseline. Chinese players who prefer balanced mixed text can use *your own font*.
- In the chat window, the bottom of the last line can be cut off by the input line, with or without the addon.
- The launcher window (account login before the game starts) draws with its own fonts and is not changed.
- With *your own font*, all styles (bold, serif) use the single font you choose. Italic styles are slanted like the stock ones: Latin letters lean, Chinese characters stay upright, as in the game. A few decorative fonts whose source fonts are not in `Gw2.dat` stay upright.
- With *sharper stock text*:
  - Latin text is re-rendered in the UI and story fonts whose letters match a font in `Gw2.dat`; a few other font families stay as blurry as without the addon;
  - Chinese text is sharp only at the Windows scale the pack was built for; after changing the Windows scale, generate the pack again;
  - text the pack does not cover (Cyrillic, most symbols, Korean, and Chinese at other scales) is enlarged smoothly when it first appears, which can pause the game briefly and uses tens of MiB per font until the game exits;
  - a few round letters are drawn slightly narrower, and accented capitals slightly smaller, so that they fit the stock spacing;
  - some decorative fonts mix two Chinese typefaces in the stock glyphs; the re-rendered text uses one.

## Fair use

Do not share generated font packs: they contain data from the game files.

This addon only changes how text is drawn. ArenaNet's [third-party program policy](https://help.guildwars2.com/hc/en-us/articles/360013625034) says that utilities that do not give one player an advantage over another are generally not acted upon, but this is at ArenaNet's discretion. Use it at your own risk.

## Reporting problems

Open an [issue](https://github.com/diov/scruffy-fontkit/issues) and attach `<game folder>\addons\Nexus\Nexus.log` and `<game folder>\addons\scruffy-fontkit\font-report.tsv`, with a screenshot if the problem is visible. Do not attach `font.pack`.

## License

Free to use; you may share the unmodified release zip. See [LICENSE](LICENSE) for the terms. Third-party components and their licenses are listed in [THIRD_PARTY_NOTICES.txt](THIRD_PARTY_NOTICES.txt).
