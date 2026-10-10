# G7External menu – implementation handoff

Paste this file (and `preview/aimbot-direction-b.png`) to whichever AI or developer builds the
real menu. It describes the UI only: layout, sizes, colours, components and screens. It says
nothing about what the features do.

## Target

Dear ImGui (C++), DirectX 11 backend, one 1200×800 window. Everything below is in pixels at
1× scale; expose a global menu scale that multiplies all of it.

## Colours (RGB hex)

| Token | Hex | Used for |
|-------|-----|----------|
| bg | `#000000` | window and sidebar background |
| panel | `#0A0A0A` | setting panels, user card, popover |
| raised | `#111111` | config cards |
| control | `#121212` | dropdowns, key buttons, chips, ghost buttons |
| control border | `#242424` | border of the above |
| hairline | `#161616` | row separators, sidebar right edge, header underline |
| panel border | `#1C1C1C` | panel border, panel header underline |
| ink | `#FFFFFF` | primary text, active states, toggle on, slider fill |
| ink2 | `#B5B5B5` | row labels |
| ink3 | `#8A8A8A` | secondary text, inactive tab text, dropdown chevron |
| ink4 | `#6B6B6B` | muted text, toggle-off knob, "Soon" items |
| ink5 | `#5A5A5A` | section overlines, N/A chip text |

Only black, white and greys. No colour accent anywhere.

## Type

Inter. Sizes: page title 20 semibold; panel title 14 semibold; row label 14 medium; nav item 14
medium; tab 13 medium; description 12 regular; control text 12–13 medium; overlines 10 semibold
with 1.4 px letter spacing, uppercase.

## Layout

```
┌────────────┬──────────────────────────────────────────────────┐
│ Sidebar    │ Main                                             │
│ 250 wide   │ padding 22 top, 26 sides, 26 bottom              │
│            │ ┌ Head: [icon] Title ............ [tab][tab][tab]│
│            │ └ 1px hairline, 18 below                         │
│            │ Panels in 1, 2 or 3 columns, 16 gap              │
│            │ (3 cols = 290 each, 2 cols = 443 each)           │
│            │ Faint eagle watermark bottom-right, 4.5 % opacity│
└────────────┴──────────────────────────────────────────────────┘
```

**Sidebar** (padding 22 top, 14 sides, 14 bottom; 1 px hairline on its right edge)
- Brand row: eagle mark 64 wide, then wordmark "G7" bold 17 + "External" regular 17 grey.
- Search field: 36 high, radius 8, fill `#0D0D0D`, border `#1E1E1E`, magnifier icon, placeholder
  "Search functions". Typing filters every setting in the menu by name.
- Sections "MAIN", "SUPPORT", "OTHER" as overlines (margin 12 above, 6 below).
- Nav items: 40 high, radius 9, padding 12 sides, icon 17 + label, gap 12.
  Inactive: label `#9A9A9A`, icon `#7A7A7A`, no fill.
  Active: fill white, label and icon black, small chevron on the right.
- Spacer, then the user card: 62 high, radius 12, fill panel, border panel-border, padding 10:
  avatar 40×40 radius 10 (image), name 14 semibold, "Lifetime" 11 grey, 8 px white dot on the
  right. Clicking it opens the account popover above it (Language, Scale, Menu style, Badge
  toggle, Unload).

**Head**: left = page icon 18 + title 20 semibold. Right = tabs, 32 high, radius 8, padding 16
sides, gap 4. Inactive: text `#8A8A8A`, no fill. Active: text white, fill `#0F0F0F`, border
`#2A2A2A`.

**Panel**: fill panel, border panel-border, radius 10, padding 10 top, 14 sides, 12 bottom.
Header 36 high: icon 16 white + title 14 semibold white, hairline under it. Body rows follow.

**Row**: min height 42, label left, control right, 1 px hairline between rows (none after the
last). Label `#B5B5B5`; white when the row's toggle is on; `#6B6B6B` when disabled ("Soon").
Rows with a description are 60 high: label line then 12 px grey description. Optional badge after
the label: 10 px semibold, 1 px border, radius 6, padding 2×7 ("New" white, "Soon" grey).

## Controls

- **Toggle**: 40×22, radius 6. Off: fill `#262626`, 16×16 knob radius 4 `#6B6B6B` at left.
  On: fill white, black knob at right. Animate the knob 150 ms.
- **Slider**: value box (white fill, radius 7, 24 high, min width 44, black 12 semibold text)
  then a 110×4 track `#2A2A2A` radius 2, white fill up to the value, 14 px white round thumb with
  a 2 px panel-coloured ring. Draggable.
- **Dropdown**: 30 high, min width 104, radius 7, fill control, border control-border, label 13
  medium white, chevron 14 grey. Opens a menu below (fill `#0F0F0F`, border control-border,
  radius 7, padding 4, items 12 medium, hovered/selected item fill `#1A1A1A`).
- **Key button**: 96×30, radius 7, fill control, border control-border, 12 medium. Idle shows the
  key name in grey ("None"). Click → "Press a key" in white with a white border, next key or
  mouse button binds, Esc clears.
- **Keybind mode chip**: 76×30, radius 7, 11 bold, letter spacing 0.5. N/A: fill control, text
  `#5A5A5A`. Hold: fill control, border `#3A3A3A`, white text. Toggle: white fill, black text.
  Click cycles N/A → Hold → Toggle.
- **Buttons**: 36 high, radius 8, padding 18 sides, 13 semibold. Primary: white fill, black
  text. Ghost: fill control, border control-border, grey text (white on hover).
- **Segmented control**: items 34 high, radius 8, gap 8, fill control / white when selected.
- **Colour swatch**: 20 px circle, 1 px `#333333` border.
- **Config card**: 66 high, fill raised, border panel-border, radius 10, 3 px white bar on the
  left edge, name 14 semibold, meta 11 grey, "Load" primary button 84 wide on the right.

## Screens (channel → tabs → panels → rows)

**Aimbot**
- Aimbot (3 columns): General (Aimbot toggle, Aimbot key, Type dropdown, FOV slider, Aim mode,
  Aim bone, Smoothing, Smooth slider, Roll boost, Curve, Easing, Aim wheels) · Targeting (Require
  ADS, Ignore NPCs, Ignore knocked, Target dead, Sticky aim, Only visible, Vis mode dropdown, Set
  HP, Dead check, Prediction) · Range (Show FOV, Distance slider, Closest FOV).
- Silent Aim (3): General (Enable, key, Visible only, Target NPC, Magic bullet, MB mode, Humanize,
  Closest FOV, Dynamic FOV, Force driver, Skip godmode, Skip dead) · Settings (FOV circle, FOV,
  Oval FOV, Distance, Aim bone) · Miss chance (slider).
- Triggerbot (2): General (Enable, key, Visible only, Target NPC, Ignore dead, Only head) ·
  Tuning (Input mode, Delay, Max distance, Min click, Max click).

**Visuals**
- ESP (2): General ("Open ESP preview" ghost button, Enable, key, Mode, Only visible, ESP
  distance, Show NPC, Show dead, Show local player, Show observers, Anti headshot detect) ·
  Options (Box, Curved box, Filled box, Snaplines, Skeleton, Head circle, Head dot, Name, Distance,
  Health bar, Armor bar; several have a "…" settings icon before the toggle).
- Raycasting (1): rows with descriptions and New/Soon badges: Enabled, Intersect vehicles (Soon),
  Intersect peds (New), Intersect objects (Soon), Intersect water (Soon), Intersect foliage (Soon).

**Misc**: tabs Defense, Movement, Weapon, Heal, Vehicle, Troll, each two panels of toggles,
sliders, dropdowns and buttons (see `plugin/code.js`, `buildScreens`, for the exact rows).

**Players**: Nearby players (search + list: name, badge, distance) · Detail (key/value list and
Teleport / Spectate / Unfriend buttons) · Friend marker (Draw marker, "FRIENDS LIST" overline,
Sort by dropdown).

**Configs**: Community (Auto load toggle, search, config cards) · Mine (cards + "New config"
ghost button) · Upload (name field, Public listing, Allow forks, Upload button).

**Keybinds**: "Active keybinds" bar, then Combat / Movement / Defense / Weapon panels; each row =
label, mode chip, key button.

**Music**: Now playing (title, artist, Prev/Pause/Next segmented, Volume, Loop, Shuffle) ·
Playlist.

**Theme**: Colors (Palette: Gradient background, Shell opacity, five swatches; Presets: Menu
scale, Preset dropdown, Reset to defaults) · Effects · Cover · Logo.

**Settings**: Panel (Feature notifications, Streamproof, Menu crosshair, VSync, Keybind list,
Full-screen exclusive, Auto inject, Auto-load last session, Menu outline, Menu scale, Menu
keybind = Insert) · Updates (Auto-update, Check for updates) · Screen sharing (Off / Projector /
DXGI segmented, Projector FPS, Display layout mode segmented, three clickable monitor tiles,
legend).

## Assets

- `preview/logo-white.svg` – the eagle mark as a single SVG path (white). Rasterise it at 64 px
  for the sidebar and ~520 px at 4.5 % opacity for the watermark.
- Icons are 24-unit stroke icons (1.8 px stroke, round caps). The SVG paths are in
  `plugin/code.js` under `const ICONS`; convert them to textures or use an icon font with the
  same shapes.

## Suggested prompt for the other AI

> Build a Dear ImGui (C++, DirectX 11) menu that matches the attached spec exactly. Use custom
> drawing with ImDrawList for the toggle, slider, dropdown, key button, chip and tabs so they
> look like the spec, not like default ImGui widgets. Put all colours and sizes in one style
> struct, support a global scale, load Inter from a TTF, and build the sidebar, header tabs and
> every screen listed. Leave all feature callbacks as empty stubs that I will fill in.
