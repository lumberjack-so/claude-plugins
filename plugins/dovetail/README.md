# 🔗 Dovetail - AI-Native Issue-Driven Workflow

**Part of the [Lumberjack Plugin Ecosystem](../../README.md)**

Dovetail enforces issue-driven development through deterministic hooks and autonomous agents. Every code change is tied to a Linear issue with proper branch management, conventional commits, and automated PR creation.

## Philosophy

> **Workflows should be enforced, not suggested.**

Dovetail doesn't remind you to create an issue—it blocks writes until you do. It doesn't suggest commit formats—it generates them automatically. It's deterministic automation that eliminates workflow friction.

## Features

### 🎯 **Issue Enforcement**
- Blocks Write/Edit operations until active Linear issue exists
- Auto-selects or creates issues via hooks
- Maintains project state in `.dovetail/state.json`

### 🌿 **Branch Management**
- Automatic feature branch creation: `feat/[key]-[slug]`
- Syncs with main before starting work
- Updates Linear issue to "In Progress"

### 🤖 **Autonomous Agents**

**dovetail-sync** (pre-work validation):
- Validates task matches active issue
- Auto-switches to relevant issue or creates new one
- Ensures correct git branch
- Shows git status and recent commits
- **Fully autonomous** - no confirmations

**dovetail-finalize** (post-work automation):
- Generates conventional commit messages
- Commits and pushes to remote
- Creates PR with detailed description
- Updates Linear with commit/PR references
- Scans for TODOs and creates issues
- Finds related issues and adds insights
- **Fully autonomous** - no confirmations

### 🔗 **Native CLI Delegation**
- GitHub: `gh` CLI for PRs, secrets
- Linear: Direct GraphQL API
- Supabase: `supabase` CLI
- Fly.io: `flyctl` CLI

### 📊 **Stateful Workflow**
- Tracks active issue across commands
- Remembers service configurations
- Persists in `.dovetail/state.json`

## Installation

### 1. Install Dovetail CLI

The CLI is required for hooks and background operations:

```bash
npm install -g @lumberjack-so/dovetail
```

### 2. Set LINEAR_API_KEY

Get your API key from [Linear Settings](https://linear.app/settings/api):

```bash
export LINEAR_API_KEY=lin_api_...
```

Add to your shell profile (`.zshrc`, `.bashrc`) to persist.

### 3. Install Plugin

The Lumberjack marketplace should already be added. If not:

```bash
/plugin marketplace add lumberjack-so/claude-plugins
```

Then install Dovetail:

```bash
/plugin install dovetail
```

Restart Claude Code to activate the plugin.

### 4. Adopt Your Project

Inside your project directory:

```bash
/adopt
```

This will:
- Create `.dovetail/state.json`
- Connect to Linear team and project
- Detect GitHub repository
- Optionally configure Supabase and Fly.io
- Enable Dovetail hooks

## Usage

### Starting Work

```bash
/start PRJ-123        # Start specific issue
/start                # Select issue interactively
```

This creates a feature branch and moves the issue to "In Progress".

### Checking Status

```bash
/status              # Show project state
/status --json       # Machine-readable output
```

### Making Changes

Just write code! The workflow is automatic:

1. **Pre-write**: `pre-tool-use` hook invokes `dovetail-sync` agent
   - Validates task relevance to active issue
   - Ensures correct branch
   - Shows git status

2. **Post-write**: `post-tool-use` hook invokes `dovetail-finalize` agent
   - Commits with conventional message
   - Creates PR
   - Updates Linear with references
   - Analyzes impact on other issues

## Slash Commands

| Command | Description |
|---------|-------------|
| `/start [issue-key]` | Start work on a Linear issue |
| `/status [--json]` | Display project state |
| `/adopt` | Adopt existing project into Dovetail |

## Agents

| Agent | When It Runs | Purpose |
|-------|--------------|---------|
| **dovetail-sync** | Before writes | Validates workflow state |
| **dovetail-finalize** | After writes | Commits, creates PR, updates Linear |

Both agents run **autonomously** without user confirmation.

## Hooks

| Hook | Trigger | Action |
|------|---------|--------|
| **session-start** | Claude Code opens | Show project snapshot |
| **user-prompt-submit** | Before prompt | Ensure active issue exists |
| **pre-tool-use** | Before Write/Edit | Invoke dovetail-sync |
| **post-tool-use** | After Write/Edit | Invoke dovetail-finalize |

## Project State

Dovetail maintains state in `.dovetail/state.json`:

```json
{
  "name": "my-project",
  "slug": "my-project",
  "activeIssue": {
    "key": "PRJ-123",
    "id": "uuid",
    "title": "Build login feature",
    "branch": "feat/prj-123-build-login-feature",
    "url": "https://linear.app/..."
  },
  "github": {
    "owner": "username",
    "repo": "my-project",
    "url": "https://github.com/username/my-project"
  },
  "linear": {
    "teamId": "uuid",
    "teamKey": "PRJ",
    "projectId": "uuid",
    "projectUrl": "https://linear.app/..."
  },
  "supabase": {
    "projectRef": "ref",
    "url": "https://....supabase.co"
  },
  "flyio": {
    "staging": "app-staging",
    "production": "app-production",
    "region": "iad"
  }
}
```

## Configuration

### Required

- **LINEAR_API_KEY**: Get from https://linear.app/settings/api
- **Git**: Repository initialized
- **Dovetail CLI**: Installed globally via npm

### Optional

- **GitHub CLI (`gh`)**: For PR creation - `brew install gh` or `winget install GitHub.cli`
- **gh Authentication**: Run `gh auth login`

## Team Setup

Add to `.claude/settings.json` in your repository:

```json
{
  "extraKnownMarketplaces": [
    "lumberjack-so/claude-plugins"
  ],
  "requiredPlugins": [
    "dovetail"
  ]
}
```

Team members will automatically get Dovetail when they trust the repository.

## Architecture

**CLI** (`@lumberjack-so/dovetail`):
- Executes commands (`start`, `status`, `check-issue`)
- Used by hooks (bash scripts)
- Direct Linear GraphQL API integration
- State management

**Plugin** (this package):
- Slash commands (invoke CLI)
- Autonomous agents (use Linear MCP or CLI)
- Hook orchestration (hooks.json)
- Claude Code integration

## Troubleshooting

### "dovetail command not found"

Install the CLI:
```bash
npm install -g @lumberjack-so/dovetail
```

### "LINEAR_API_KEY not set"

Export your Linear API key:
```bash
export LINEAR_API_KEY=lin_api_...
```

### "Not a Dovetail project"

Run `/adopt` to initialize the project.

### Hooks not triggering

1. Check plugin is installed: `/plugin`
2. Restart Claude Code after installation
3. Verify you're in project directory with `.dovetail/state.json`

## Version History

**2.0.18** (Current)
- Initial plugin release
- Converted from standalone CLI to Claude Code plugin
- Added autonomous agents (dovetail-sync, dovetail-finalize)
- Linear GraphQL API integration
- Full hook system implementation

See [CHANGELOG.md](https://github.com/lumberjack-so/dovetail/blob/main/CHANGELOG.md) for complete history.

## Support

- 📖 [Full Documentation](https://github.com/lumberjack-so/dovetail)
- 🐛 [Report Issues](https://github.com/lumberjack-so/claude-plugins/issues)
- 💬 [Discussions](https://github.com/lumberjack-so/claude-plugins/discussions)
- 📧 [Email Support](mailto:alfred@lumberjack.so)
- 🪓 [More Lumberjack Plugins](../../README.md)

## License

MIT - see [LICENSE](../../LICENSE)

---

**Built with ❤️ by [Lumberjack Software](https://lumberjack.so)**
