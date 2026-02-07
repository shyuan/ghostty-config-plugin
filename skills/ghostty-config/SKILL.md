---
name: ghostty-config
description: >
  Manage and troubleshoot Ghostty terminal emulator configuration.
  Triggers: customize Ghostty settings, troubleshoot Ghostty config,
  explore Ghostty options, change Ghostty theme/font/keybindings,
  ghostty config, ghostty 設定.
---

# Ghostty Config Management

## Config File Location

- **macOS**: `~/Library/Application Support/com.mitchellh.ghostty/config`
- **Linux**: `$XDG_CONFIG_HOME/ghostty/config` (usually `~/.config/ghostty/config`)

## Config Syntax Rules

- Format: `key = value` (spaces around `=` are optional)
- Comments: `#` must be at the **beginning of the line** — inline comments are NOT supported
- Empty value resets to default: `key =`
- Multi-value options: repeat the key on separate lines (e.g. `font-family`)
- To clear a multi-value and set a new one: first set `key = ""` then set the new value
- Boolean values: `true` / `false`
- Hot-reload: most settings apply immediately; some require a new window or full restart

## MCP Tools Reference

Use the `ghostty-config` MCP server tools for accurate, up-to-date information:

| Tool | When to Use |
|------|------------|
| `ghostty_search_config_docs` | User asks about config options by topic (e.g. "padding", "cursor", "scroll") |
| `ghostty_get_config_option` | User asks about a specific config key — **always check docs before advising** |
| `ghostty_show_current_config` | User wants to see current settings; use `changes_only=true` for modified values |
| `ghostty_validate_config` | User reports config errors or asks to check their config |
| `ghostty_list_fonts` | User wants to pick or check available fonts |
| `ghostty_list_themes` | User wants to browse or switch themes |
| `ghostty_list_actions` | User wants to set up keybindings |
| `ghostty_list_keybinds` | User wants to see or modify keybindings |
| `ghostty_list_colors` | User needs named color values |
| `ghostty_show_face` | User wants to check which font renders specific characters |
| `ghostty_version` | Check installed Ghostty version |

## Standard Workflows

### Changing a Config Option

1. Use `ghostty_get_config_option` to read the **full docs** for the option
2. Pay attention to the **value type and unit** (bytes, not lines!)
3. Edit the config file
4. Use `ghostty_validate_config` to verify
5. Ghostty hot-reloads most settings automatically

### Switching Themes

1. `ghostty_list_themes` with optional `color="dark"` or `color="light"` filter
2. Set `theme = <name>` in config
3. Note: manually set colors override theme colors

### Switching Fonts

1. `ghostty_list_fonts` to browse available fonts
2. Set `font-family = <exact name>` — name must match exactly
3. For fallback chain, repeat `font-family` on multiple lines
4. Use `ghostty_show_face` to verify character rendering

### Setting Up Keybindings

1. `ghostty_list_actions` to see available actions
2. `ghostty_list_keybinds` to see current bindings
3. Format: `keybind = modifiers+key=action:params`
4. Modifiers: `super`, `ctrl`, `alt`, `shift` (joined with `+`)
5. Unbind: `keybind = keys=unbind`

## Common Gotchas

See `references/config-gotchas.md` for detailed pitfalls and their solutions.

**Critical**: Always use `ghostty_get_config_option` to check documentation before giving advice about any config option. This prevents unit/type mistakes.
