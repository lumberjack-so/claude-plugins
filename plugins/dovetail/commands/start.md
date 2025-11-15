---
description: Start work on a Linear issue with proper branch setup
allowed-tools: [Bash, Read, mcp__linear__*]
argument-hint: [issue-key]
---

# Start Work on Linear Issue

Start work on a Linear issue by:
- Fetching issue details from Linear
- Creating feature branch: `feat/[key]-[slug]`
- Checking out the branch
- Moving issue to "In Progress" status
- Saving to project state

## Usage

```
/start PRJ-123        # Start specific issue
/start                # Interactive issue selection
```

## Implementation

This command requires the Dovetail CLI to be installed:

```bash
npm install -g @lumberjack-so/dovetail
```

Then execute:

```bash
!dovetail start $ARGUMENTS
```

## Prerequisites

- Dovetail CLI installed globally
- LINEAR_API_KEY environment variable set
- Git repository initialized
- Inside a Dovetail project (`.dovetail/state.json` exists)

If not yet initialized, run `/dovetail-adopt` first.
