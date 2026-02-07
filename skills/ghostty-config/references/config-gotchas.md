# Ghostty Config Gotchas

## scrollback-limit is in BYTES, not lines

`scrollback-limit` specifies the scrollback buffer size in **bytes**, not lines.
- Default: `10000000` (10 MB)
- Setting it to `10000` gives you ~10 KB, which is only a few hundred lines
- For "10,000 lines", you'd need roughly `1000000` (1 MB) or more depending on line width
- The value includes the active screen size, with leftover used for scrollback
- Set to `0` for no scrollback, or a very large value like `100000000` for ~100 MB

## Font family name must match exactly

- `font-family` requires the **exact** family name as shown by `ghostty +list-fonts`
- It is NOT case-insensitive — `"JetBrains Mono"` works, `"jetbrains mono"` does not
- For fallback chains, repeat the key:
  ```
  font-family = JetBrains Mono
  font-family = Fira Code
  font-family = monospace
  ```
- To reset a previously set chain: `font-family = ""` then set new values

## Comments only at line start

```
# This is a valid comment
font-size = 14  # THIS IS NOT A COMMENT — it becomes part of the value!
```

The `#` is only treated as a comment when it's the first non-whitespace character on a line.

## Theme vs manual color overrides

- `theme = <name>` sets all colors from a theme
- Manually setting `background`, `foreground`, `palette` etc. **overrides** theme colors
- If you set a theme and colors look wrong, check for manual color settings that conflict
- To see what's different from defaults: `ghostty +show-config --changes-only`

## Hot-reload vs new window vs full restart

- **Hot-reload** (automatic): most visual settings (colors, font-size, padding, theme)
- **New window required**: some structural settings
- **Full restart required**: settings that affect the rendering backend or process model
- When in doubt, open a new window to test changes

## Keybind syntax details

- Format: `keybind = modifier+key=action` or `keybind = modifier+key=action:param`
- Chord bindings: `keybind = ctrl+a>ctrl+b=action` (press ctrl+a then ctrl+b)
- Multiple modifiers: `super+shift+c` (joined with `+`)
- To unbind: `keybind = keys=unbind`
- To see all bindable actions: `ghostty +list-actions`
- Physical vs logical keys: by default uses logical (layout-dependent) keys

## Config file paths by OS

| OS | Path |
|----|------|
| macOS | `~/Library/Application Support/com.mitchellh.ghostty/config` |
| Linux | `$XDG_CONFIG_HOME/ghostty/config` (default: `~/.config/ghostty/config`) |

The config file does not have an extension — it's just named `config`.

## Multi-value config options

Some options accept multiple values by repeating the key:
- `font-family` (fallback chain)
- `keybind` (multiple bindings)
- `palette` (color palette entries)

For these, each line adds to the list rather than replacing.

## Empty values reset to default

Setting a key with no value resets it to the default:
```
font-size =
```
This is different from not having the key at all (which also uses the default) — it's useful for overriding values set earlier in the config or in imported configs.
