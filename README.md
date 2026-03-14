# ticktick-claude

Command-line tool for reading and managing TickTick tasks via the [TickTick Open API](https://developer.ticktick.com). Designed for integration with Claude cowork — tag tasks with `claude` in TickTick to surface them for AI-assisted completion.

## Requirements

- **Python >= 3.10** — [python.org/downloads](https://www.python.org/downloads/)
- A [TickTick account](https://ticktick.com)

## Setup

### 1. Register a TickTick app

Go to <https://developer.ticktick.com/manage>, sign in, and create an app. Set the redirect URI to `http://localhost:8080/callback`. Note your **Client ID** and **Client Secret**.

### 2. Configure credentials

```bash
cp .env.example .env
# Edit .env with your Client ID and Client Secret
```

### 3. Install

```bash
pip install -e .
```

### 4. Authorize

```bash
ticktick auth
```

This opens your browser to authorize the app. Tokens are saved to `~/.ticktick_token.json`.

If this command fails, the directory where pip installs scripts may not be in your `PATH`. Run `pip show pip` and look at the `Location` field to find where pip packages are installed, then add the corresponding `Scripts` directory to your `PATH` — or provide the full path to the executable directly (e.g. `C:\Users\Jesse\AppData\Local\Python\pythoncore-3.14-64\Scripts\ticktick.exe auth`).

### 5. Copy TickTick Token (Required for Claude Cowork)

Copy `~/.ticktick_token.json` from your home directory (e.g. `C:\Users\<user_name>` on Windows) into the root of this repository. Claude Cowork runs in a VM and will copy this file to the expected location on startup.

## Usage

```bash
# List all open tasks
ticktick tasks

# List tasks tagged "claude" (for Claude cowork)
ticktick claude-tasks

# List all projects
ticktick projects

# Filter by tag
ticktick tasks --tag work

# Filter by project ID
ticktick tasks --project <project-id>

# Include completed tasks
ticktick tasks --all

# Verbose output (IDs, content, due dates)
ticktick tasks --verbose
ticktick claude-tasks --verbose

# JSON output (useful for piping to other tools)
ticktick tasks --json
ticktick claude-tasks --json
```

## Task Mutation Commands

These commands let you modify tasks directly from the CLI — useful as building blocks for Claude cowork or any automation.

```bash
# Append text to a task's description
ticktick append-description <project-id> <task-id> "Notes from research..."

# Append text AND add checklist items in a single atomic write
# (avoids stale-read race condition when doing both in the same session)
ticktick append-description <project-id> <task-id> "Notes..." --checklist "Step 1" "Step 2" "Step 3"

# Add checklist items to a task
ticktick add-checklist <project-id> <task-id> "Step 1" "Step 2" "Step 3"

# Create separate daily repeating tasks at one or more times of day
# --project accepts a project name (case-insensitive) or project ID
ticktick add-daily-tasks "Take medication" --project "Health" --times 7am 3pm 11pm
ticktick add-daily-tasks "Check metrics" --project <project-id> --times 09:00 17:00

# Mark a task as completed
ticktick complete-task <project-id> <task-id>
```

Use `ticktick tasks --verbose` or `ticktick tasks --json` to find task and project IDs.

> **Note on `append-description --checklist`**: When appending a description and adding checklist items in the same session, always use the `--checklist` flag rather than running `append-description` and `add-checklist` as separate commands. Separate commands trigger a stale-read race condition where the second fetch returns data that doesn't yet reflect the first write, causing the checklist to overwrite the description.

## Claude Cowork Integration

Tag any task in TickTick with `claude` and it will appear when running:

```bash
ticktick claude-tasks --json
```

This JSON output is designed to be consumed by Claude cowork to assist with or complete the tagged tasks. Claude can then use `append-description`, `add-checklist`, and `complete-task` to update tasks as it works on them.
