# Figma Intelligence

[![Node.js](https://img.shields.io/badge/node-%3E%3D18-brightgreen)](https://nodejs.org)
[![npm](https://img.shields.io/npm/v/@sarjallab09/figma-intelligence)](https://www.npmjs.com/package/@sarjallab09/figma-intelligence)
[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-nd/4.0/)
[![MCP Tools](https://img.shields.io/badge/MCP%20tools-90-blue)]()

> **90 AI-powered design tools for Figma.**  
> Works with your Claude, OpenAI Codex, GitHub Copilot, or Gemini CLI subscription. One command to set up.

```
You (chat in Figma plugin) ◀──▶ Local Relay ◀──▶ Claude / OpenAI Codex / Gemini CLI / GitHub Copilot
```

---

## ✨ What does this do?

Type something like *"Make a login screen with a blue button"* and the AI will actually **create the components and layers** in your Figma file — not just describe how to do it.

The plugin exposes **90 MCP tools** across 6 phases:

| Phase | Tools | Examples |
|---|---|---|
| **Visual Intelligence** | 7 | Screen cloning, visual audit, accessibility audit, sketch-to-design |
| **Design System Accuracy** | 6 | Intent translation, layout intelligence, variant expansion, linting |
| **Generation & Scaffolding** | 14 | Page architect, swarm build, prototype wiring, composition builder |
| **Sync & Bidirectionality** | 9 | Token export (16 formats), component code gen, handoff specs |
| **Governance & Health** | 15 | Health reports, token docs, design system scaffolding, DTCG validation |
| **Node Operations** | 38 | Create, read, update, delete nodes, variables, styles, components |

---

## 🚀 Quick Start

### Step 1 — Install an AI CLI and log in

You need at least one. All four use your **existing subscription** — no extra API costs.

| Provider | Install | Log in |
|---|---|---|
| **Claude** | [claude.ai/download](https://claude.ai/download) | `claude login` |
| **OpenAI Codex** | `npm install -g @openai/codex` | `codex login` |
| **Google Gemini** | `npm install -g @google/gemini-cli` | `gemini` (opens Google sign-in) |
| **GitHub Copilot** | `npm install -g @github/copilot` | `copilot` then `/login` |

---

### Step 2 — Run setup

```bash
npx @sarjallab09/figma-intelligence setup
```

This will:
- Install dependencies and build the MCP server
- Detect which AI CLIs you have and check their login status
- Ask for your **Figma Personal Access Token** ([how to get one](#-figma-personal-access-token))
- Register the MCP server with your detected providers
- Start the local relay server
- Copy the Figma plugin files to your **Documents folder**
- Automatically copy the plugin path to your clipboard
- Optionally install as a background service *(macOS)*

---

### Step 3 — Load the plugin in Figma *(one-time)*

> **Note:** Requires Figma Desktop app — the browser version won't work.

The setup command copies the plugin path to your clipboard. Just follow these steps:

1. **Open any file** in Figma Desktop *(the plugin menu only works when a file is open)*
2. Press **Shift + I** to open the Resources panel *(or click the grid icon in the toolbar)*
3. Click the **Plugins** tab → click the **`···`** menu in the top-right → select **"Import plugin from manifest..."**
4. In the file picker, paste the path:
   - **Mac:** `Cmd + Shift + G` → `Cmd + V` → `Enter`
   - **Windows:** `Ctrl + L` → `Ctrl + V` → `Enter`
5. Navigate to **Documents → Figma Intelligence → manifest.json** and click **Open**

> 💡 **Pro tip:** Right-click the plugin name and select **"Save to favorites"** to pin it to the top of your Plugins menu.

---

### Step 4 — Open the plugin

- **Right-click** anywhere on the canvas → **Plugins** → **Figma Intelligence**
- Or press **Shift + I** → Plugins tab → search **"Figma Intelligence"**

**That's it.** The plugin auto-connects to the relay server. Start chatting!

---

## 🔑 Figma Personal Access Token

Required so the plugin can read and edit your Figma files.

1. Open Figma Desktop
2. Click your **profile photo** (top-left) → **Settings** → **Security**
3. Scroll to **Personal access tokens** → **Generate new token**
4. Give it any name (e.g. `Figma Intelligence`)
5. Copy the token — **Figma only shows it once**

---

## 💬 Using the chat

Once connected, the plugin panel has a chat box at the bottom. Just type what you want:

```
"Create a login screen with email and password fields"
"Add a navigation bar with 4 menu items"
"Design a card component with a photo, title, and a blue button"
```

To attach a screenshot: click the **paperclip icon** next to the chat box.

---

### Three modes

| Tab | What it does |
|---|---|
| **Chat** | Ask questions — the AI answers but does **not** change your Figma file |
| **Code** | The AI builds and edits your Figma design directly using MCP tools |
| **Design + Code** | Same as Code, but also generates component source code (React / Vue / Svelte) and writes it to your VS Code workspace |

---

### Design + Code mode *(dual output)*

The most powerful mode. From a single prompt in Figma, the AI:

1. **Creates the component in Figma** — with proper auto layout, variants, properties, and design tokens
2. **Generates matching code** — component file, CSS module, and Storybook story
3. **Writes the code to your VS Code workspace** — files appear in `src/components/` automatically

The VS Code bridge extension (installed automatically by setup) connects in the background. A status indicator in the plugin header shows whether VS Code is connected. If VS Code is not running, code output still appears in the Figma chat as text.

---

### Switching providers

Use the **provider badge** in the plugin header to switch between Claude, OpenAI, Gemini, and Copilot.

- **Claude** — uses the account logged into the Claude CLI
- **OpenAI** — uses the account logged into `codex`
- **Gemini** — uses the authenticated Gemini CLI account; falls back to API key mode if unavailable

Setup registers the same Figma MCP server for all providers, so switching reuses the running bridge and MCP connection automatically.

---

## ⚙️ Commands

After setup, manage the relay with these commands:

```bash
npx @sarjallab09/figma-intelligence start    # Start the relay server
npx @sarjallab09/figma-intelligence stop     # Stop the relay server
npx @sarjallab09/figma-intelligence status   # Show relay + provider status
npx @sarjallab09/figma-intelligence doctor   # Diagnose issues
npx @sarjallab09/figma-intelligence setup    # Full setup (first time or reconfigure)
npx @sarjallab09/figma-intelligence update   # Update plugin files to latest version
```

---

## 🔄 Every time you restart your computer

If you installed the **background service** during setup *(macOS)*, the relay starts automatically — no action needed.

Otherwise, just run:

```bash
npx @sarjallab09/figma-intelligence start
```

Then open the Figma plugin — it reconnects automatically.

---

## ⬆️ Updating to a new version

```bash
npx @sarjallab09/figma-intelligence@latest update
```

This copies the latest plugin files to your local folder. Figma automatically picks up the changes — just close and reopen the plugin.

---

## 🛠️ Troubleshooting

| Problem | Fix |
|---|---|
| **"npm: command not found"** | Node.js is not installed — download from [nodejs.org](https://nodejs.org) |
| **Plugin shows "Server offline"** | Run `npx @sarjallab09/figma-intelligence start` in your terminal |
| **Plugin shows setup guide** | Follow the on-screen steps — run the setup command in your terminal |
| **Plugin not found in Figma** | Import it: `Shift+I` → Plugins tab → `···` menu → "Import plugin from manifest..." → navigate to **Documents → Figma Intelligence → manifest.json** |
| **Can't find the plugin folder** | It's in `~/Documents/Figma Intelligence/`. On Mac, use `Cmd+Shift+G` in the file picker and paste the path. |
| **Not sure what is broken** | Run `npx @sarjallab09/figma-intelligence doctor` for full diagnostics |
| **Chat does nothing / no response** | Run `claude login` / `codex login` / `gemini` to re-authenticate your AI provider |
| **Gemini doesn't build in Figma** | Install Gemini CLI: `npm i -g @google/gemini-cli`, run `gemini` to sign in, then re-run setup |
| **Wrong Figma token / token expired** | Re-run `npx @sarjallab09/figma-intelligence setup` and paste your new token |
| **Port 9001 already in use** | Run `npx @sarjallab09/figma-intelligence stop` then `start` again |

---

## 🤝 Contributing

1. Fork the repo and create a feature branch
2. Run `npx @sarjallab09/figma-intelligence setup` to install all dependencies
3. Make your changes
4. Run `npx @sarjallab09/figma-intelligence doctor` to verify everything works
5. Open a pull request

---

## 📄 License

This project is licensed under [CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/) — you are free to use it, but you may not distribute modified versions or use it commercially.  
See [LICENSE](./LICENSE) for details.
