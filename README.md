# 🪓 Lumberjack Plugins for Claude Code

Official Claude Code plugin marketplace from Lumberjack Software.

## About Lumberjack

Lumberjack builds AI-native development tools that enforce best practices through deterministic automation instead of suggestions. Our philosophy: **workflows should be enforced, not suggested**.

## Available Plugins

### 🔗 [Dovetail](./plugins/dovetail)
**Category:** Productivity
**Version:** 2.0.18
**Status:** ✅ Stable

AI-native issue-driven development workflow with deterministic hooks and native CLI delegation.

**Features:**
- 🎯 Enforces Linear issue tracking for all work
- 🌿 Automatic feature branch management
- 🤖 Autonomous pre/post-work agents (dovetail-sync, dovetail-finalize)
- 🔗 Native CLI delegation (GitHub, Linear, Supabase, Fly.io)
- 📊 Stateful project management
- ✅ Conventional commit enforcement

[Learn more →](./plugins/dovetail)

### 🔄 Linear Sync _(Coming Soon)_
**Category:** Productivity
**Status:** 🚧 Planned

Bi-directional synchronization between Linear issues and GitHub pull requests.

### ⚙️ GitHub Automator _(Coming Soon)_
**Category:** DevOps
**Status:** 🚧 Planned

Advanced GitHub workflow automation with PR templates, issue triage, and release notes generation.

## Installation

### Quick Start

```bash
# Add Lumberjack marketplace
/plugin marketplace add lumberjack-so/claude-plugins

# Browse and install plugins
/plugin

# Or install directly
/plugin install dovetail
```

### Team Setup

Add to your repository's `.claude/settings.json` to auto-install for all team members:

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

## Plugin Philosophy

All Lumberjack plugins follow these principles:

1. **Deterministic over Suggestive**: Hooks enforce workflow, agents don't ask permission
2. **CLI Delegation over API Wrappers**: Use native tools (gh, linearis) instead of reimplementing APIs
3. **Stateful over Stateless**: Track project state in `.dovetail/state.json` or similar
4. **Autonomous over Interactive**: Agents make intelligent decisions without user confirmation
5. **Conventional over Custom**: Follow established patterns (conventional commits, semver, etc.)

## Support

- 📖 [Documentation](https://github.com/lumberjack-so/claude-plugins/wiki)
- 🐛 [Report Issues](https://github.com/lumberjack-so/claude-plugins/issues)
- 💬 [Discussions](https://github.com/lumberjack-so/claude-plugins/discussions)
- 📧 [Email Support](mailto:alfred@lumberjack.so)

## Contributing

We welcome plugin proposals and contributions! See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

### Plugin Proposal Template

Have an idea for a Lumberjack plugin? Open an issue with:
- Plugin name and category
- Problem it solves
- Native CLIs it would use
- How it follows Lumberjack philosophy

## License

All Lumberjack plugins are released under the [MIT License](./LICENSE).

---

**Built with ❤️ by [Lumberjack Software](https://lumberjack.so)**
