---
name: trailofbits-security-skills
description: "Use Trail of Bits' curated security skills marketplace for AI-assisted security research, vulnerability detection, smart contract auditing, and code review workflows. Compatible with Claude Code, Codex, and ChatGPT Workspace."
version: 1.0.0
author: Johnson | GetClawCloud
license: MIT
platforms: [linux, macos]
metadata:
  hermes:
    tags: [security, audit, vulnerability, smart-contract, trail-of-bits]
---

# Trail of Bits Security Skills

A curated marketplace of security-focused skills from Trail of Bits, a leading cybersecurity research firm. Provides capabilities for AI-assisted security analysis, vulnerability detection, and audit workflows.

## When to Use

- Security auditing of smart contracts
- Code review for vulnerabilities
- Analyzing GitHub Actions workflows for security issues
- Binary analysis and reverse engineering
- Building security testing pipelines

## Source

- GitHub: https://github.com/trailofbits/skills
- Related: https://github.com/trailofbits/claude-code-config
- Related: https://github.com/trailofbits/codex-config

## Installation

### Claude Code Marketplace

```bash
/plugin marketplace add trailofbits/skills
```

### Codex

```bash
codex plugin marketplace add trailofbits/skills
codex plugin list
codex plugin add <plugin-name>@trailofbits
```

### ChatGPT Workspace

Use the `.claude-plugin/marketplace.json` file for workspace imports.

### Local Development

```bash
cd /path/to/parent
/plugins marketplace add ./skills
```

## Available Skills

### Smart Contract Security

| Skill | Description |
|-------|-------------|
| `building-secure-contracts` | Smart contract security toolkit with vulnerability scanners for 6 blockchains and 5 development guideline assistants |
| `entry-point-analyzer` | Identify state-changing entry points in smart contracts for security auditing |

### Code Auditing

| Skill | Description |
|-------|-------------|
| `agentic-actions-auditor` | Audit GitHub Actions workflows for AI agent security vulnerabilities |
| `audit-context-building` | Understand a codebase before looking for bugs in it, one function at a time |
| `burpsuite-project-parser` | Search and extract data from Burp Suite project files |
| `c-review` | Comprehensive C/C++ security code review, with coverage verified against a parse of the source |
| `differential-review` | Security-focused differential review of code changes with git history analysis |
| `dimensional-analysis` | Annotate codebases with dimensional analysis comments to detect unit mismatches and formula bugs |
| `fp-check` | Systematic false positive verification for security bug analysis with mandatory gate reviews |

### How to Use

When working on a security task, the agent will automatically load relevant skills from the marketplace. For manual invocation:

```
> Use the c-review skill to audit this C codebase
> Run the agentic-actions-auditor on these GitHub Actions workflows
> Apply the building-secure-contracts skill to this Solidity contract
```

## Supported Platforms

- **Claude Code**: Full marketplace support
- **OpenAI Codex**: Direct plugin marketplace compatibility
- **ChatGPT Workspace**: Via `.claude-plugin/marketplace.json`
- **Hermes Agent**: Via MCP or direct skill import

## Security Best Practices

1. **Review before deploy**: Always review generated findings before taking action
2. **Isolate sensitive code**: Don't share proprietary code with external models
3. **Verify results**: Automated audits are supplemental, not replacement for manual review
4. **Stay updated**: Regularly update skills to get latest vulnerability patterns

## Pitfalls

1. **Over-reliance**: These skills augment but don't replace professional security auditors
2. **Context limits**: Large codebases may exceed context windows; use incremental analysis
3. **False positives**: FP-check skill helps but some manual triage is still needed
4. **Platform compatibility**: Some features may vary between Claude Code, Codex, and other platforms

## Related Skills

- `skill-inspector`: For analyzing and understanding skill behavior
- `red-teaming/godmode`: For offensive security testing
- `social-engineering-defense`: For defending against social engineering

## Links

- [GitHub Repository](https://github.com/trailofbits/skills)
- [Claude Code Config](https://github.com/trailofbits/claude-code-config)
- [Codex Config](https://github.com/trailofbits/codex-config)
