# Ghostty Config Recipes — Practical Patterns & Combos

Curated config patterns learned from community configs. Use these as starting points, not copy-paste solutions — always verify options via MCP tools first.

---

## macOS 視覺優化組合

These settings work together for the best visual experience on Apple displays.

```
window-colorspace = display-p3
font-thicken = true
background-opacity = 0.9
```

- `display-p3` unlocks the wide color gamut on Apple screens — colors appear more vibrant and saturated.
- `font-thicken` compensates for thin strokes on dark/transparent backgrounds.
- These are **macOS-only** settings. On Linux, `font-thicken` has no effect and `window-colorspace` is unsupported.

**Note**: Switching to `display-p3` changes how hex colors are interpreted. Existing palette colors will look slightly different (more saturated). This is most noticeable with high-saturation colors like `#FE5F86` or `#8056FF`.

## 字體微調技巧

### Light weight + font-thicken 組合

Use a Light weight font as the base, then thicken it for a custom stroke weight between Light and Regular:

```
font-family = JetBrains Mono Light
font-family-bold = JetBrains Mono Bold
font-family-italic = JetBrains Mono Italic
font-family-bold-italic = JetBrains Mono Bold Italic
font-thicken = true
```

This gives finer control over stroke weight than simply using the Regular weight. Especially effective on Retina displays.

### 字元間距與游標粗細

```
adjust-cell-width = -4%
adjust-cursor-thickness = 175%
```

- `adjust-cell-width = -4%` tightens character spacing — fits more columns in the same window width. Good for coding. Don't go below `-8%` or characters may overlap.
- `adjust-cursor-thickness = 175%` makes the bar cursor more visible. Helpful on high-DPI displays where the default 1px cursor can be hard to spot.
- Values are relative adjustments (percentage or pixel offset), NOT absolute values.

### 行高微調

```
adjust-cell-height = 2
```

- Adds 2px to each cell height for more breathing room between lines.
- The font is centered vertically within the taller cell.
- Powerline glyphs auto-adjust with cell height.

## macOS 體驗設定

### 非原生全螢幕

```
macos-non-native-fullscreen = true
keybind = super+f=toggle_fullscreen
```

- Skips the macOS fullscreen animation — instant toggle.
- The window fills the screen without creating a new Space.
- Trade-off: no swipe-between-spaces gesture for the fullscreen window.

### Window padding

```
window-padding-x = 12
window-padding-y = 10
window-padding-balance = true
```

- Adds visual breathing room around the terminal content.
- `window-padding-balance = true` centers content when the window is larger than needed, distributing extra space evenly.

## 常見組合模式

### 暗色半透明 + 背景模糊 + 高可讀性

```
background = #171717
background-opacity = 0.8
background-blur = 20
font-thicken = true
window-colorspace = display-p3
```

- Dark background with transparency + blur so the content behind is not directly visible.
- `background-blur` accepts an integer for intensity. Default recommended: `20`. Higher values (e.g. `90`) produce heavier blur but may cause rendering artifacts or performance issues.
- On macOS 26.0+, special values `macos-glass-regular` and `macos-glass-clear` use native glass effects.
- Supported on macOS and some Linux DEs (KDE Plasma). Other Linux DEs may need third-party plugins.
- `font-thicken` prevents thin strokes from becoming hard to read against the blurred background.

### 緊湊 coding 排版

```
font-size = 16
adjust-cell-width = -4%
window-padding-x = 12
window-padding-y = 10
```

Tighter character spacing with padding for a clean, dense layout that maximizes visible code.

## Quick Terminal（全域快捷終端機）

Quake-style dropdown terminal accessible from any app — one of Ghostty's most powerful features.

```
keybind = global:cmd+escape=toggle_quick_terminal
quick-terminal-position = top
quick-terminal-animation-duration = 0.2
```

- `global:` prefix makes the keybind work **system-wide**, not just when Ghostty is focused.
- The terminal slides in from the configured position. Press again to dismiss.
- `quick-terminal-position` supports: `top`, `bottom`, `left`, `right`, `center`.
- Set `quick-terminal-animation-duration = 0` to disable the slide animation entirely.
- Changing `quick-terminal-position` requires a **full restart** of Ghostty on macOS.
- There is **no default keybind** — you must explicitly bind `toggle_quick_terminal` to enable this feature.

## 視窗狀態與啟動行為

### 視窗狀態持久化

```
window-save-state = always
```

- Restores window position, size, tabs, and splits when Ghostty is reopened.
- Default is `default` (macOS only saves on force-quit). Set to `always` to save on every exit.
- Requires shell integration for preserving working directories in tabs/splits.
- macOS only — no effect on Linux.

### 啟動最大化

```
maximize = true
```

- New windows start maximized automatically. Applies to all new windows, not tabs/splits.
- Available since Ghostty v1.1.0.

## Keybind 實用模式

### Split 操作與 Vim 風格導航

```
keybind = super+d=new_split:right
keybind = super+shift+d=new_split:down
keybind = super+ctrl+h=goto_split:left
keybind = super+ctrl+l=goto_split:right
keybind = super+ctrl+k=goto_split:top
keybind = super+ctrl+j=goto_split:bottom
```

- `super+d` / `super+shift+d` for horizontal/vertical splits mirrors VS Code and iTerm2 conventions.
- `super+ctrl+hjkl` for Vim-style directional navigation between splits.

### 設定開發快捷鍵

```
keybind = super+r=reload_config
```

- Manually trigger config reload. Useful when tweaking settings to see changes instantly.
- Most visual settings hot-reload automatically, but having an explicit keybind gives certainty.
