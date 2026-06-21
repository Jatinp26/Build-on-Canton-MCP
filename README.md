# Canton Network MCP Server

When developers use AI tools to learn Canton, they get recommended deprecated documentation links. This Local MCP Integration **solves** that. It provides a curated, remotely updated knowledge base covering Canton's Dev Stack and Guide Devs using Claude 0 to 100.

> **IMP NOTICE: MCP Plugin gives right links and context to LLM Models but DOEST NOT Garuntee any LLM generating 100% correct info due to their nature, in any case like this, kindly make a new Github issue with the same and we will update the MCP plugin.** 

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

### Prerequisites

- Node.js 18+
- `npm install` in the repo root (installs `@modelcontextprotocol/sdk`)

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

Users who want to contribute can submit a PR to update `knowledge-base.json`.