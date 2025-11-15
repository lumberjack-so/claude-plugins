---
description: Adopt an existing project into Dovetail workflow
allowed-tools: [Bash, Read, Grep, mcp__linear__*]
---

# Adopt Existing Project

Convert an existing project to use Dovetail workflow automation.

This will:
1. Create `.dovetail/state.json` with project configuration
2. Detect and save GitHub repository info
3. Connect to Linear team and project
4. Set up Supabase and Fly.io references (if applicable)
5. Enable Dovetail hooks via this plugin

## Usage

```
/adopt
```

## Prerequisites

### Required

1. **Dovetail CLI installed**:
   ```bash
   npm install -g @lumberjack-so/dovetail
   ```

2. **LINEAR_API_KEY environment variable** set:
   ```bash
   export LINEAR_API_KEY=lin_api_...
   ```
   Get your API key at: https://linear.app/settings/api

3. **Git repository initialized**:
   ```bash
   git init  # if not already done
   ```

### Optional

- **GitHub CLI** for PR creation: `brew install gh` (macOS) or `winget install GitHub.cli` (Windows)
- **Authenticated gh**: Run `gh auth login`

## Implementation

```bash
!dovetail adopt
```

## What This Creates

The command will interactively guide you through:
- Selecting your Linear team
- Choosing or creating a Linear project
- Detecting GitHub repository from git remote
- Optionally configuring Supabase and Fly.io

After completion, you'll have:
- `.dovetail/state.json` with full project configuration
- Dovetail workflow enforcement via plugin hooks
- Access to all Dovetail slash commands
- Autonomous agents (dovetail-sync, dovetail-finalize)

## Next Steps

After adoption:
1. Start work on an issue: `/start`
2. Check project status: `/status`
3. Make code changes (agents will handle workflow automatically)
