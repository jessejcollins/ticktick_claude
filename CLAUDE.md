# CLAUDE.md

Guide for AI assistants working on the ticktick-claude project.

## Project Overview

**ticktick-claude** is a Claude Code and Claude Cowork integration that uses the [TickTick MCP server](https://mcp.ticktick.com) (documentation at [https://help.ticktick.com/articles/7438129581631995904](https://help.ticktick.com/articles/7438129581631995904)) to let Claude read and manage TickTick tasks directly.

## MCP Setup

This project uses TickTick's official MCP server at `https://mcp.ticktick.com`, configured in `.mcp.json`. Claude Code and Claude Cowork connect via Streamable HTTP and authenticate with OAuth.

To authorize on first use (or re-authorize), run `/mcp` in your Claude Code session and follow the OAuth prompts in your browser.

## Workflow

When running inside Claude Code or Claude Cowork in this repository, if the user's opening message is not clearly about a specific coding task or file, ask if they would like to check TickTick for tasks. If the user's first message is about something unrelated to TickTick (e.g. a question about the codebase), answer it first — then offer to check TickTick afterward. Do not automatically fetch tasks — wait for the user to confirm before proceeding.

Advertise the following capabilities to the user as ideas of what they can do:

1. Find a specific task to work on - ask the user for the task name or project it is in, then search for it
2. List tasks tagged with "claude" tag - this helps me find tasks that I can work on
3. Research a specific task and update the description with the findings - search the internet for information about the task
4. Breakdown a specific task into smaller parts which are added to the task as checklist items - search the internet for information to help create the checklist items
5. Add a new tasks for something that reoccurs daily and happens multiple times per day (e.g. take meds at 7am, 3pm, 11pm) - these are separate tasks at different times of the day
6. Plan my day - look at non-recurring tasks that are due today and don't have a time set, and move them to open time slots in the day, only schedule between 8am and 8pm
6. Roll the dice - get a random task to work on

Or anything else that the user asks for that is related to TickTick tasks.

## Limitations/Restrictions

- If someone has this repo checked out and you are using this CLAUDE.md file to guide them, then you should ONLY focus on interacting with TickTick tasks. For example, if they ask about getting ideas of what you can do, only suggest ideas related to TickTick tasks.
