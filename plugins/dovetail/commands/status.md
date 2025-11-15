---
description: Display current Dovetail project state and configuration
allowed-tools: [Bash]
---

# Dovetail Project Status

Display the current project state including:
- Active Linear issue
- Current git branch
- GitHub repository info
- Linear team and project
- Supabase configuration
- Fly.io deployments

## Usage

```
/status            # Human-readable output
/status --json     # Machine-readable JSON output
```

## Implementation

```bash
!dovetail status $ARGUMENTS
```

## Prerequisites

- Dovetail CLI installed: `npm install -g @lumberjack-so/dovetail`
- Inside a Dovetail project directory

## Output

Shows comprehensive project snapshot with service links and current work status.
