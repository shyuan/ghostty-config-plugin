# Ghostty Config Plugin for Claude Code

AI-powered Ghostty terminal configuration management — 11 MCP tools + domain knowledge skill.

## Installation

### Via Marketplace (Recommended)

```bash
/plugin marketplace add shyuan/shyuan-marketplace
/plugin install ghostty-config@shyuan-marketplace
```

### Direct Install

```bash
/plugin marketplace add shyuan/ghostty-config-plugin
/plugin install ghostty-config@ghostty-config-dev
```

## What You Get

### MCP Tools (11 tools)

| Tool | Description |
|------|-------------|
| `ghostty_search_config_docs` | Search config documentation by keyword |
| `ghostty_get_config_option` | Get full docs for a specific config option |
| `ghostty_show_current_config` | Show active configuration |
| `ghostty_validate_config` | Validate config file for errors |
| `ghostty_list_fonts` | List available font families |
| `ghostty_list_themes` | List available themes (dark/light filter) |
| `ghostty_list_actions` | List bindable actions |
| `ghostty_list_keybinds` | List current keybindings |
| `ghostty_list_colors` | List named colors |
| `ghostty_show_face` | Check which font renders specific characters |
| `ghostty_version` | Show Ghostty version info |

### Skill: `ghostty-config`

Domain knowledge for accurate Ghostty configuration advice:

- Config syntax rules and gotchas
- Standard workflows (change options, switch themes/fonts, set keybindings)
- Common pitfalls (e.g. `scrollback-limit` is in bytes, not lines)

## Requirements

- [Ghostty](https://ghostty.org/) installed and available in PATH
- Node.js 18+

## Standalone MCP Server

If you only need the MCP tools without the Claude Code plugin:

```bash
npx ghostty-config-mcp
```

See [ghostty-config-mcp](https://github.com/shyuan/ghostty-config-mcp) for details.

## License

MIT
