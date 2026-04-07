# Figma-Intelligence-Read-me
Figma Intelligence is an AI-powered toolkit that connects your AI assistant directly to Figma through 88 MCP (Model Context Protocol) tools — letting Claude, Cursor, or VS Code read, create, audit, and modify your designs in real time.
# Figma-Intelligence
Figma Intelligence is an AI-powered toolkit that connects your AI assistant directly to Figma through 88 MCP (Model Context Protocol) tools — letting Claude, Cursor, or VS Code read, create, audit, and modify your designs in real time.
# Figma Intelligence

> AI-powered design tools for Figma — 88 MCP tools that give your AI assistant the ability to read, create, audit, and modify Figma designs.

Works with **Claude**, **Cursor**, and **VS Code**.

---

## Prerequisites

- **Node.js 18+** — [download](https://nodejs.org/)
- **Figma Desktop** — [download](https://www.figma.com/downloads/)
- **Figma Personal Access Token** — [generate](https://www.figma.com/developers/api#access-tokens)

---

## Quick Start

### 1. Install

```bash
npx figma-intelligence@latest setup
```

Installs everything and registers MCP tools with Claude, Cursor, and VS Code automatically.

### 2. Start

```bash
npx figma-intelligence@latest start
```

### 3. Load the plugin

1. Open **Figma Desktop** and open any design file
2. Go to **Plugins → Development → Import plugin from manifest**
3. Select `~/.figma-intelligence/plugin/manifest.json`
4. Run the plugin — you should see **Connected**

### 4. Try it

```
"Audit this Figma page for accessibility issues"
"Clone this screenshot into Figma using the design system"
"Generate a React component from the selected Figma component"
```

---

## Commands

| Command | Description |
|---|---|
| `npx figma-intelligence@latest setup` | Install and configure |
| `npx figma-intelligence@latest start` | Start the relay |
| `npx figma-intelligence@latest stop` | Stop the relay |
| `npx figma-intelligence@latest status` | Check connection |

---

## How It Works

```
Your Machine                              Cloud
┌───────────────────┐                    ┌──────────────────┐
│   Figma Desktop   │                    │   88 MCP Tools   │
│  (plugin inside)  │                    │  (AI runs here)  │
│         │         │    encrypted       │        ▲         │
│         ▼         │──── tunnel ───────▶│   Tool Router    │
│   Local Relay     │                    └──────────────────┘
└───────────────────┘
         ▲
         │
   Claude / Cursor / VS Code
```

Your design files stay in Figma. No design data is stored on the server.

---

## Troubleshooting

**Plugin shows "Bridge offline"**
- Click **Reconnect** in the plugin, or restart the relay:
  ```bash
  npx figma-intelligence@latest stop && npx figma-intelligence@latest start
  ```

**Plugin shows "Not logged in"**
- Click **Log in** in the plugin, or run `claude login` in your terminal

**MCP tools not showing in your AI tool**
- Restart Claude / Cursor / VS Code after running setup
- Check status: `npx figma-intelligence@latest status`

**Relay won't start**
- Stop any existing relay: `npx figma-intelligence@latest stop`
- Check for port conflicts: `lsof -i :9001`

**Updating to the latest version**
- Re-run setup — your config is preserved:
  ```bash
  npx figma-intelligence@latest setup
  npx figma-intelligence@latest start
  ```

---

## License

[CC-BY-NC-ND-4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/)
