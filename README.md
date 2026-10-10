# pi-kanso-themes

The four [Kanso](https://github.com/webhooked/kanso.nvim) themes for the
[pi](https://pi.dev) coding agent — Ink, Zen, Mist and Pearl.

This is a themes-only extraction of
[`@haispeed/pi-deck`](https://github.com/hisea/pi-deck). The upstream package
bundles a two-line status-line extension; that footer is deliberately **not**
included here. The theme JSON files themselves are unmodified.

| Theme         | Appearance | Background | Foreground | Accent    |
| ------------- | ---------- | ---------- | ---------- | --------- |
| `kanso-ink`   | dark       | `#14171d`  | `#C5C9C7`  | `#8992a7` |
| `kanso-zen`   | dark       | `#090E13`  | `#C5C9C7`  | `#8992a7` |
| `kanso-mist`  | dark       | `#22262D`  | `#C5C9C7`  | `#8992a7` |
| `kanso-pearl` | light      | `#f2f1ef`  | `#22262D`  | `#624c83` |

## Install

```bash
pi install git:github.com/sergio-agosti/pi-kanso-themes
```

Or from a local checkout:

```bash
pi install /path/to/pi-kanso-themes
```

Then pick a theme with `/settings` → Theme, or in `~/.pi/agent/settings.json`:

```json
{
  "theme": "kanso-ink"
}
```

Package themes are loaded at startup; run `/reload` after editing them. (Only
themes placed directly in `~/.pi/agent/themes/<name>.json` hot-reload on their
own.)

## The four themes

Ink, Zen and Mist share the same foreground and syntax palette — they differ
only in how dark the background stack is. Pearl is the light counterpart and
overrides a handful of slots (heading, error, diff and number colours) with
purpose-built light values.

|                | Ink                  | Zen                  | Mist                 | Pearl                |
| -------------- | -------------------- | -------------------- | -------------------- | -------------------- |
| Background     | `#14171d`            | `#090E13`            | `#22262D`            | `#f2f1ef`            |
| Float / panel  | `#1f1f26`            | `#1C1E25`            | `#2a2c35`            | `#e2e1df`            |
| Muted surface  | `#22262D`            | `#22262D`            | `#393B44`            | `#dddddb`            |
| Foreground     | `#C5C9C7`            | `#C5C9C7`            | `#C5C9C7`            | `#22262D`            |
| Muted text     | `#A4A7A4`            | `#A4A7A4`            | `#A4A7A4`            | `#545464`            |
| Comment        | `#75797f`            | `#75797f`            | `#75797f`            | `#6D6D69`            |
| Border / line  | `#5C6066`            | `#5C6066`            | `#5C6066`            | `#9F9F99`            |
| Accent         | `#8992a7`            | `#8992a7`            | `#8992a7`            | `#624c83`            |
| Green / string | `#8a9a7b`            | `#8a9a7b`            | `#8a9a7b`            | `#6f894e`            |
| Yellow         | `#c4b28a`            | `#c4b28a`            | `#c4b28a`            | `#77713f`            |
| Orange         | `#b6927b`            | `#b6927b`            | `#b6927b`            | `#cc6d00`            |
| Red / error    | `#C34043`            | `#C34043`            | `#C34043`            | `#c84053`            |
| Diff add bg    | `#2B3328`            | `#2B3328`            | `#2B3328`            | `#b7d0ae`            |
| Diff del bg    | `#43242B`            | `#43242B`            | `#43242B`            | `#d9a594`            |

## Pairing dark and light

Pearl is the light half of a pair with any of the three dark themes. Pi has
built-in automatic pairing: store the light theme first and the dark theme
second, separated by `/`, in `~/.pi/agent/settings.json`.

```json
{
  "theme": "kanso-pearl/kanso-ink"
}
```

Pi then decides light or dark from your terminal's reported background (and
re-checks when the terminal reports an appearance change). Override for a
single run with:

```bash
pi --use-theme kanso-pearl/kanso-ink
```

The upstream theme files set no `appearance` field, so the pairing is driven
entirely by the setting above — the names carry no light/dark metadata.

## Palette

Every colour resolves to an entry in kanso.nvim's `lua/kanso/colors.lua`. The
three dark themes differ only in which background stack they draw from; the
foreground, accent and syntax palette is shared across all three.

| Theme | kanso.nvim background stack                                            |
| ----- | ---------------------------------------------------------------------- |
| Ink   | `inkBg0` `#14171d` · `inkBg1` `#1f1f26` · `inkBg2` `#22262D`            |
| Zen   | `zenBg0` `#090E13` · `zenBg1` `#1C1E25` · `zenBg2` `#22262D`            |
| Mist  | `mistBg0` `#22262D` · `mistBg1` `#2a2c35` · `mistBg2` `#393B44`         |
| Pearl | `pearlWhite0` `#f2f1ef` · `pearlWhite1` `#e2e1df` · `pearlWhite2` `#dddddb` |

The shared dark palette comes from `violet2` (`#8992a7`), `gray2`
(`#A4A7A4`), `gray4` (`#75797f`), `gray5` (`#5C6066`), `blue3` (`#8ba4b0`),
`blue4`/`aqua` (`#8ea4a2`), `green5` (`#7AA89F`), `green3` (`#8a9a7b`),
`yellow3` (`#c4b28a`), `yellow` (`#DCA561`), `orange` (`#b6927b`), `red`
(`#C34043`), `red3` (`#c4746e`), `pink` (`#a292a3`) and the
`diffGreen`/`diffRed` backgrounds.

Pearl's overrides map onto `pearlViolet4`, `pearlBlue4`, `pearlAqua`,
`pearlTeal3`, `pearlGreen`/`pearlGreen2`/`pearlGreen3`, `pearlYellow`/
`pearlYellow2`, `pearlOrange`/`pearlOrange2`, `pearlRed`/`pearlRed2`/
`pearlRed3`/`pearlRed4` and `pearlPink`.

## Validation

All four themes pass pi's own `validateThemeJson`: every required colour slot
is present, every `vars` reference resolves, and no slot falls back to the
terminal default. The files are byte-identical to their upstream originals.

## Credits and licence

Theme definitions are taken unmodified from
[`@haispeed/pi-deck`](https://github.com/hisea/pi-deck) v0.1.5 (MIT,
Copyright © 2025 hai), which in turn derives its colours from
[`kanso.nvim`](https://github.com/webhooked/kanso.nvim) (MIT, Copyright © 2025
Webhooked). Kanso is itself a port of
[Kanagawa](https://github.com/rebelot/kanagawa.nvim). All theme design credit
belongs to those authors; this package only packages the themes for pi without
the upstream footer extension. See [NOTICE](NOTICE) for full attributions.

Released under the [MIT licence](LICENSE).
