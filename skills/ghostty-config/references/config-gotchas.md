# Ghostty Config Gotchas — Complete Reference

For quick summary see the "Critical Gotchas" section in SKILL.md. This file has full details and workarounds.

---

## scrollback-limit: bytes, not lines

- Unit is **bytes**, not lines. Default `10000000` = 10 MB.
- Setting `10000` gives ~10 KB — only a few hundred lines.
- For ~10,000 lines, use `1000000` (1 MB) or more depending on line width.
- Set `0` to disable scrollback entirely.
- **Memory issue**: high-throughput sessions (e.g. running build tools, Claude Code) can cause memory to grow far beyond the configured limit. The arena allocator does not return memory to the OS. One user reported 1 GB → 21 GB over 2.5 days. Workaround: periodically close and reopen tabs for long-running sessions.

## background-opacity: premultiplied alpha bugs

- Light themes + transparency produce wrong colors due to premultiplied alpha blending.
- On Linux GTK, tab bar appearance breaks when opacity < 1.
- `background-blur = macos-glass-regular` combined with `background-opacity` can break titlebar and quick terminal on macOS.
- Workaround: if colors look wrong with transparency, try a dark theme or set opacity to `1`.
- Config reload may not fix appearance — a full restart of Ghostty is sometimes required.

## macos-titlebar-style = transparent: dark background silently fails

- When background color ≤ `#0c0c0c`, `transparent` silently reverts to `native`.
- Users see no error — the titlebar just doesn't become transparent.
- Workaround: use a background color brighter than `#0c0c0c`, e.g. `#0d0d0d`.

## Config reload vs restart

- **Hot-reload** (automatic): most visual settings — colors, font-size, padding, theme (single theme).
- **New window required**: some structural settings.
- **Full restart required**:
  - `theme = light:X,dark:Y` dual syntax: after reload, tab bar may get stuck in wrong light/dark mode. Split overlay colors and titlebar colors can also break.
  - Appearance changes after setting `background-opacity`.
  - Any change that seems to partially apply — restart first before debugging.

## Font family: exact name required

- `font-family` requires the **exact** name from `ghostty +list-fonts`.
- Case-sensitive: `JetBrains Mono` works, `jetbrains mono` does not.
- For fallback chain, repeat the key on multiple lines.
- To clear and reset: `font-family = ""` then `font-family = NewFont`.

## macOS CJK font fallback: oversized characters

- Without an explicit CJK font, macOS fallback uses double-em-width estimation.
- CJK characters render comically large — much wider and taller than expected.
- Linux does not have this issue (system fontconfig handles fallback correctly).
- Workaround: explicitly add a CJK font to the fallback chain:
  ```
  font-family = JetBrains Mono
  font-family = PingFang SC
  ```

## Keybind gotchas

- **`keybind =` (empty value) removes ALL keybinds including defaults** — this does NOT reset to defaults. It leaves you with zero keybindings.
- **`ctrl+/`** must be written as `ctrl+slash` — `/` is parsed as a key table separator.
- **`performable:` prefix** in multi-split layouts: the action may still consume the key event even when the action cannot be performed in the focused split.

## selection-word-chars: escape sequences not parsed

- `\t` in `selection-word-chars` is treated as literal `\` and `t`, not as a tab character.
- This causes any word containing `t` to be incorrectly selected on double-click.
- Do not use escape sequences in this option.

## Linux fractional scaling: blurry fonts

- At 125%, 150%, 175% scaling, fonts will be blurry. Only 100% and 200% render sharply.
- `font-thicken = true` does not help.
- This is a renderer limitation — no config workaround exists.

## Theme vs manual color settings

- `theme = <name>` sets all colors from a theme file.
- Manually setting `background`, `foreground`, or `palette` **overrides** theme colors.
- If colors look wrong after setting a theme, check for conflicting manual color settings.
- Use `ghostty_show_current_config` with `changes_only=true` to see what's actually set.

## macOS dual config paths

- macOS path `~/Library/Application Support/com.mitchellh.ghostty/config` takes **priority** over XDG path `~/.config/ghostty/config`.
- Both paths can coexist, but macOS path always wins.
- Vim/Neovim filetype detection may not recognize the macOS path for syntax highlighting.
- If config changes seem to have no effect, check both paths.
