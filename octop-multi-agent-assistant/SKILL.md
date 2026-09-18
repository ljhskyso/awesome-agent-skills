---
name: octop-multi-agent-assistant
description: "Deploy and configure Octop — a self-hosted multi-user, multi-agent AI assistant built on the Harness stack. Supports web dashboard, CLI, IM channels (Feishu, DingTalk, Discord, etc.), and cron automation."
version: 1.0.0
author: Johnson | GetClawCloud
license: MIT
platforms: [linux, macos]
metadata:
  hermes:
    tags: [octop, multi-agent, self-hosted, harness, assistant]
---

# Octop Multi-Agent Assistant

Octop is an open-source, self-hosted AI assistant platform by Tencent Cloud. It runs a single process serving a web dashboard, CLI, IM channels, and cron automation — all sharing one control-plane database.

## When to Use

- Setting up a personal or team AI assistant
- Need multi-user isolation with shared expert library
- Want IM integration (Feishu, DingTalk, WeChat Work, Discord, QQ)
- Require browser automation, remote desktop, or scheduled tasks
- Building a self-hosted alternative to commercial AI assistants

## Source

- GitHub: https://github.com/TencentCloud/Octop
- PyPI: https://pypi.org/project/octop/
- Discord: https://discord.gg/jPas5J8Ua

## Key Features

| Feature | Description |
|---------|-------------|
| 👥 Multi-user expert team | One admin, shared household; switch specialists per scenario |
| 🎭 MBTI personas | 16 personality templates + interactive quiz for agents |
| 🔒 Security built-in | JWT multi-user isolation, tool approval, shell command guardrails, PII redaction |
| 🔌 Connector ecosystem | Tencent suite (Docs, Weibo trends, News); OAuth and MCP gateway |
| 💾 Pluggable backends | Local disk, Docker containers, PostgreSQL, or COS/S3 |
| 🧠 Portable memory | Powered by harness-memory; memory migrates with workspace |
| 📚 Knowledge base | RAG over documents; semantic retrieval grounds agent answers |
| ↔️ ACP bidirectional | `octop acp` for IDE/terminal AI; delegate to OpenCode / Claude Code |
| 💻 Terminal AI+ | Interactive shell in browser with AI assistance |
| 🌐 Browser AI+ | Headless Chromium for web automation |
| 🖥️ Remote desktop | Live screen and input from dashboard |
| 🏠 Self-hosted | All data under `~/.octop/` — SQLite by default |

## Tech Stack

- **Language**: Python 3.12+
- **Web framework**: FastAPI + uvicorn
- **Agent runtime**: harness-agent
- **Gateway**: harness-gateway
- **Memory**: harness-memory
- **Browser**: harness-browser
- **Frontend**: React 18 + TypeScript + Vite + Ant Design
- **Scheduling**: APScheduler
- **ACP**: agent-client-protocol

## Quick Start

```bash
# Install via pip
pip install octop

# Initialize (first run wizard)
octop init

# Run the assistant
octop run
```

Access the web dashboard at `http://localhost:8000`.

## Configuration

Config file: `~/.octop/config.json`

Key settings:
```json
{
  "enable_api_docs": true,
  "database": {
    "type": "sqlite",
    "path": "~/.octop/data/octop.db"
  },
  "agents": {
    "experts_library": "infra/agents/experts/library/"
  }
}
```

## IM Channel Setup

Octop supports multiple IM channels through `harness-gateway`:

1. **Feishu/Lark**: Configure OAuth app and set webhook URL
2. **DingTalk**: Create custom robot and set access token
3. **WeCom**: Configure enterprise application
4. **Discord**: Set up bot token
5. **QQ**: Use official QQ Bot API

Each channel is configured in `~/.octop/channels.json`:
```json
{
  "feishu": {
    "app_id": "your_app_id",
    "app_secret": "your_app_secret",
    "verification_token": "your_token"
  }
}
```

## Agent Configuration

Agents are defined in `~/.octop/agents.json`:
```json
{
  "agents": [
    {
      "name": "research-assistant",
      "persona": "analyst",
      "model": "gpt-4o",
      "tools": ["web_search", "browser", "file_read"],
      "workspace_backend": "local"
    }
  ]
}
```

## Cron Automation

Set up scheduled tasks via natural language or config:
```bash
# Add cron job
octop cron add --name "daily-summary" --schedule "0 9 * * *" --prompt "Summarize yesterday's messages"

# List jobs
octop cron list
```

## Expert Library

Experts are YAML files in `infra/agents/experts/library/`:
```yaml
name: data-analyst
description: Expert in data analysis and visualization
persona: analyst
tools:
  - python_repl
  - file_read
  - web_search
system_prompt: |
  You are a data analysis expert. Help users with:
  - Data cleaning and transformation
  - Statistical analysis
  - Visualization recommendations
```

## Pitfalls

1. **Port conflicts**: Default port is 8000. If occupied, use `--port` flag.
2. **Database migration**: Always backup `~/.octop/data/` before upgrading.
3. **IM rate limits**: Some platforms (WeCom, Feishu) have strict rate limits.
4. **Memory isolation**: Each agent has its own workspace; don't share workspaces across agents.
5. **API docs**: Disabled by default for security. Enable only on trusted networks.

## Security Considerations

- JWT tokens are used for multi-user isolation
- Tool approval can be enabled to require confirmation
- Shell commands can be restricted with guardrails
- PII redaction is built-in for log privacy
- All data stays local by default

## Related Skills

- `hermes-agent`: For Hermes Agent configuration
- `mcp/native-mcp`: For MCP server integration
- `scheduled-tasks-cron`: For setting up cron jobs
- `devops/fork-maintenance`: For maintaining self-hosted instances

## Links

- [Official Documentation](https://github.com/TencentCloud/Octop#readme)
- [GitHub Repository](https://github.com/TencentCloud/Octop)
- [PyPI Package](https://pypi.org/project/octop/)
- [Discord Community](https://discord.gg/jPas5J8Ua)
