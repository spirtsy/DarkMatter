# G7External – menu UI design kit

Black-and-white menu UI for **G7External**, built from the SRC-style inspiration screenshots
(sidebar + tab bar + rounded setting panels) but restyled as a strict monochrome system
around the G7 eagle logo.

Live Figma file (component library + first screens already in place):
https://www.figma.com/design/ruDYOtjMHGaT4sTjUHYoHV

## Contents

| Path | What it is |
|------|------------|
| `plugin/` | A Figma **development plugin** that builds the whole kit into any file: component library, 12 screens, brand sheet. Free on every plan. |
| `preview/g7external-preview.html` | Self-contained HTML mock of every screen (open in a browser). Same layout, colours and copy as the Figma build. |
| `preview/*.png` | Rendered previews of each screen, the brand sheet and the component sheet. |
| `preview/logo-white.svg` | The traced vector version of the G7 eagle (white, for dark backgrounds). |

## Running the plugin (free)

1. Open Figma desktop, open the **G7External** file (or any blank design file).
2. Menu → **Plugins → Development → Import plugin from manifest…**
3. Pick `g7external-figma/plugin/manifest.json`.
4. Menu → **Plugins → Development → G7External Builder**.

It creates three pages: `G7 · Components`, `G7 · Screens` and `G7 · Brand`, and loads the
`Inter` font (bundled with Figma). Running it twice will add a second set of pages, so delete
the old ones first if you re-run.

## What gets built

**Components** – Logo mark, Toggle (On/Off), Badge (New/Soon), Keybind Mode Chip
(N/A / Hold / Toggle), Key Button, Dropdown, Button (Primary/Ghost), Color Swatch, Search Field,
User Card, Nav Item, Tab, Row samples and a 30-icon sheet.

**Screens** (1200×800, auto-layout throughout)

- Aimbot → Aimbot, Silent Aim, Triggerbot
- Visuals → ESP, Raycasting
- Misc → Defense (+ Movement, Weapon, Heal, Vehicle, Troll tabs)
- Players, Configs (Community), Keybinds
- Theme → Colors
- Settings, Settings with the account popover open

**Brand** – logo on black / on white, wordmark, 10-colour palette (also added as local
paint styles `G7/…`) and the type scale.

## Palette

| Token | Hex |
|-------|-----|
| Background | `#050505` |
| Shell | `#0B0B0B` |
| Sidebar | `#0E0E0E` |
| Panel | `#141414` |
| Control | `#1C1C1C` |
| Border | `#262626` |
| Text muted | `#6B6B6B` |
| Text secondary | `#9A9A9A` |
| Text primary / Accent | `#FFFFFF` |

Typography is Inter: Semi Bold 20 for section titles, Medium 14 for row labels, Regular 12
for descriptions and Medium 10 with 1.2 px tracking for overlines.

## Interactive version (v2)

`interactive/g7external-menu.html` is a working, clickable build of the menu. Open it in any
browser. Everything is live: toggles, sliders, dropdowns, keybind capture (click a key button,
press a key or mouse button, Esc clears), keybind mode chips (click to cycle N/A → Hold → Toggle),
the sidebar search (`/` to focus, results jump to the setting), the Players and Configs searches,
config loading, the music player, the display-layout picker and the account popover on the
profile picture. State is remembered in the browser between visits.

This version drops the rounded "mojo" shell for a hard-edged monochrome layout on a pure black
background: header bar with the eagle mark and build tag, left rail with a white active marker,
underlined tabs, hairline panels, mono-spaced labels and a status strip.
