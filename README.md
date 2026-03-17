# ticktick-claude

TickTick integration for Claude Code and Claude Cowork using the [TickTick MCP server](https://help.ticktick.com/articles/7438129581631995904). Surface tasks for AI-assisted completion directly inside Claude.

## How It Works

This project uses TickTick's official MCP server (`https://mcp.ticktick.com/`), configured in `.mcp.json`. When you open this repository in Claude Code or Claude Cowork, Claude can read and manage your TickTick tasks directly through the MCP integration — no separate CLI or API setup required.

## Setup

### Claude Code

[https://help.ticktick.com/articles/7438129581631995904#claude-code](https://help.ticktick.com/articles/7438129581631995904#claude-code)

#### 1. Open in Claude Code

Open this repository in Claude Code. The `.mcp.json` file automatically configures the TickTick MCP server.

#### 2. Authorize TickTick

On first use, run `/mcp` in your Claude Code session. Claude will prompt you to complete OAuth authorization in your browser.

### Claude Cowork

#### 1. Install Node.js

The MCP connection requires Node.js. Download it from [nodejs.org](https://nodejs.org) if you don't have it.

_TODO: Add Claude Cowork setup steps._

## Claude Cowork Workflow

Open this repository in Claude Code or Claude Cowork and Claude will ask if you'd like to check for tasks, then guide you through reviewing, working on, and completing them.

Claude can:
- List your open tasks
- Read task descriptions and checklist items
- Update task descriptions and add checklist items
- Create new tasks
- Mark tasks as complete
