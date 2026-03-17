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

[https://help.ticktick.com/articles/7438129581631995904#claude-desktop](https://help.ticktick.com/articles/7438129581631995904#claude-desktop)

**Note:** The steps below are because Claude Desktop doesn't understand the `.mcp.json` file automatically.

#### 1. Go to Connectors in Claude Desktop

Open Claude Desktop and navigate in left panel to `Customize > Connectors`.

#### 2. Add Connector

Click "+" and select "Add custom connector..."

#### 3. Enter MCP Server Details

Enter the MCP server Name "TickTick" and URL [https://mcp.ticktick.com](https://mcp.ticktick.com).

#### 4. Connect to TickTick MCP Server

Click "TickTick" under "Connectors" and then click "Connect" button. Follow the on-screen prompts to complete OAuth sign-in and authorization.

## Claude Cowork Workflow

Open this repository in Claude Code or Claude Cowork and Claude will ask if you'd like to check for tasks, then guide you through reviewing, working on, and completing them.

Claude can:
- List your open tasks
- Read task descriptions and checklist items
- Update task descriptions and add checklist items
- Create new tasks
- Mark tasks as complete
