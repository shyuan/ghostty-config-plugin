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

See [ghostty-config-mcp](https://github.com/shyuan/ghostty-config-mcp) for details.

## License

MIT

---

# Ghostty Config Plugin for Claude Code（中文說明）

AI 驅動的 Ghostty 終端模擬器設定管理 — 11 個 MCP 工具 + 領域知識 Skill。

## 安裝方式

### 透過 Marketplace 安裝（推薦）

```bash
/plugin marketplace add shyuan/shyuan-marketplace
/plugin install ghostty-config@shyuan-marketplace
```

### 直接安裝

```bash
/plugin marketplace add shyuan/ghostty-config-plugin
/plugin install ghostty-config@ghostty-config-dev
```

## 安裝後你會得到

### MCP 工具（11 個）

| 工具 | 說明 |
|------|------|
| `ghostty_search_config_docs` | 用關鍵字搜尋設定文件 |
| `ghostty_get_config_option` | 取得特定設定項的完整文件 |
| `ghostty_show_current_config` | 顯示目前生效的設定 |
| `ghostty_validate_config` | 驗證設定檔語法 |
| `ghostty_list_fonts` | 列出可用字型家族 |
| `ghostty_list_themes` | 列出可用主題（可篩選深色/淺色） |
| `ghostty_list_actions` | 列出可綁定的動作 |
| `ghostty_list_keybinds` | 列出目前快捷鍵綁定 |
| `ghostty_list_colors` | 列出具名顏色 |
| `ghostty_show_face` | 查詢特定字元使用的渲染字型 |
| `ghostty_version` | 顯示 Ghostty 版本資訊 |

### Skill：`ghostty-config`

提供 Ghostty 設定的領域知識，讓 AI 給出正確建議：

- 設定檔語法規則與常見陷阱
- 標準操作流程（修改選項、切換主題/字型、設定快捷鍵）
- 常見錯誤（例如 `scrollback-limit` 的單位是 bytes 不是行數）

## 環境需求

- [Ghostty](https://ghostty.org/) 已安裝且在 PATH 中
- Node.js 18+

## 獨立 MCP Server

如果你只需要 MCP 工具，不需要 Claude Code plugin：

請參考 [ghostty-config-mcp](https://github.com/shyuan/ghostty-config-mcp)。

## 授權條款

MIT
