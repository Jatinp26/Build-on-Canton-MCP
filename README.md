# Canton Network MCP Server

When developers use AI tools to learn Canton, they get recommended deprecated documentation links. This Local MCP Integration **solves** that. It provides a curated, remotely updated knowledge base covering Canton's Dev Stack and Guide Devs using Claude 0 to 100.

> **New Release:** Extended Info on LayerZero LIVE on Canton and CIP-103 & Wallet Components including dApp SDK, dApp API, Wallet Gateway and More.

## How does it do this?

The server fetches its knowledge base from this repo on startup, then caches it locally. If and When we push an update here, every MCP user gets it automatically on their next restart, no manual pulls needed.

## Quick Install for Claude Desktop

Add to your Claude Desktop config (`../Claude/claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "canton-dev": {
      "command": "node",
      "args": ["/path/to/Build-on-Canton-MCP/index.js"]
    }
  }
}
```
Then restart Claude Desktop. You should see the Canton tools in the tools menu.

## Quick Install for Codex

Add this MCP server to Codex:

```bash
codex mcp add canton-dev -- node /path/to/Build-on-Canton-MCP/index.js
```

Then start a new Codex session. You can confirm the server is configured with:

```bash
codex mcp list
```

### Prerequisites

- Node.js 18+
- `npm install` in the repo root (installs `@modelcontextprotocol/sdk`)

## What Context Tools Does this MCP Possess?

The server exposes 7 tools that Claude (or any MCP client) calls automatically based on the developers question.

### `canton_get_started`

Personalized quickstart based on developer background. Triggers on "how to build on Canton" and similar. Asks the developer to select their background first then generates a guide.

Backgrounds: `evm` · `solana` · `sui_move` · `web_dev` · `enterprise` · `new_to_blockchain`

### `canton_lookup`

Search across all Canton docs, tools, concepts, and APIs in the Knowledge base. Returns accurate versioned links and automatically surfaces deprecation warnings.

### `canton_check`

Deprecation checker to use before recommend. any tool to a developer.

```
"daml-assistant"  - DEPRECATED
"dpm"   - CURRENT.
```

### `canton_faq`
FAQs with code snippets that has installation, party creation, contracts, PQS, Scan API, transfers, deployment, traffic fees, multi-package projects, and more.

### `canton_api_ref`
Detailed reference for all available canton APIs

`json_ledger_api`,
`grpc_ledger_api`,
`scan_api`,
`validator_api`,
`token_standard`,
`admin_api`

### `canton_compare_evm`
EVM concepts to Canton equivalents and covers smart contracts, wallets, gas, ERC20, Hardhat, ABI, deploy, events, and more.

### `canton_network_info`
Basic network details for `local`, `devnet`, `testnet`, `mainnet` and includes URLs, setup commands, and xReserve bridge info.

## Updating the Knowledge Base

Edit `knowledge-base.json` at the repo root. This is the file that gets fetched remotely by every MCP user.

Structure:
```
DEPRECATED[]     — Tools/commands to warn against
TOOLS{}          — Current tools with install commands
DOCS{}           — Versioned documentation links
CONCEPTS{}       — Architecture and concept explanations
NETWORKS{}       — LocalNet/DevNet/TestNet/MainNet details
COMMUNITY{}      — Slack, Discord, mailing lists
VERSIONS{}       — Current SDK and Splice versions
ZENITH{}         — Zenith EVM info
FAQ[]            — Developer questions with code-snippet answers
```

Users who want to contribute can submit a PR to update `knowledge-base.json`. The bundled knowledge base file lives at the repo root.

PRs welcome for `knowledge-base.json` updates. When contributing:

1. Keep links versioned (e.g., `/build/3.4/` not `/build/latest/`)
2. Add deprecation entries for any tool being replaced
3. Include install commands and code snippets in FAQ answers
4. Test locally: `npx @modelcontextprotocol/inspector node index.js`
