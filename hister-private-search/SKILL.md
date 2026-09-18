---
name: hister-private-search
description: "Deploy Hister — a self-hosted private search engine for your web pages and local files. Index and search through your browsing history and filesystem without leaking data to third parties."
version: 1.0.0
author: Johnson | GetClawCloud
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [hister, search, privacy, self-hosted, engine]
---

# Hister Private Search Engine

Hister is a self-hosted search engine for the pages you visit and the files you keep. It provides full-text search over your browser history and local filesystem with a clean web interface.

## When to Use

- Need to search through your browsing history locally
- Want to search your filesystem without cloud services
- Privacy-conscious users who don't want to leak search queries
- Developers who need quick access to code documentation and notes
- Teams needing a private search solution for internal resources

## Source

- GitHub: https://github.com/asciimoo/hister
- Website: https://hister.sh
- Blog: https://blog.hister.sh

## Key Features

- 🔒 **Privacy-first**: All data stays on your machine
- 🌐 **Browser integration**: Automatically indexes your browser history
- 📁 **File search**: Full-text search over your filesystem
- 🔄 **Real-time indexing**: Continuously updates as you browse
- 📊 **Metrics & monitoring**: Built-in observability
- 🔌 **API**: REST API for programmatic access
- 🎨 **Modern UI**: Clean, responsive web interface

## Installation

### Via Docker (Recommended)

```bash
docker run -d \
  --name hister \
  -p 8080:8080 \
  -v ~/.hister:/data \
  -e HISTER_AUTH_TOKEN=your-secret-token \
  asciimoo/hister:latest
```

### Via Go

```bash
go install github.com/asciimoo/hister/cmd/hister@latest
hister serve
```

### From Source

```bash
git clone https://github.com/asciimoo/hister.git
cd hister
make build
./hister serve
```

## Configuration

Default config location: `~/.hister/config.yaml`

```yaml
server:
  addr: ":8080"
  auth_token: "${HISTER_AUTH_TOKEN}"

database:
  path: "~/.hister/data/hister.db"

indexer:
  browsers:
    - chrome
    - firefox
  paths:
    - ~/Documents
    - ~/Projects
  exclude:
    - node_modules
    - .git
    - __pycache__
```

## Browser Integration

Hister automatically detects and indexes popular browsers:

| Browser | Platform | Status |
|---------|----------|--------|
| Chrome | Linux/macOS/Windows | ✅ Supported |
| Firefox | Linux/macOS/Windows | ✅ Supported |
| Edge | Windows/macOS | ✅ Supported |
| Brave | All | ✅ Supported |
| Safari | macOS | ⚠️ Manual export required |

### Browser History Location

- **Chrome**: `~/Library/Application Support/Google/Chrome/Default/History` (macOS)
- **Firefox**: `~/Library/Application Support/Firefox/Profiles/` (macOS)

## API Usage

Hister exposes a REST API for programmatic access:

```bash
# Search
curl -H "Authorization: Bearer $TOKEN" \
  "http://localhost:8080/api/v1/search?q=your+query"

# Get history stats
curl -H "Authorization: Bearer $TOKEN" \
  "http://localhost:8080/api/v1/stats"

# Export results
curl -H "Authorization: Bearer $TOKEN" \
  "http://localhost:8080/api/v1/export?format=json" \
  -o results.json
```

## CLI Commands

```bash
# Start the server
hister serve

# Index browsers manually
hister index browsers

# Index paths manually
hister index paths --paths ~/Documents

# Clear index
hister clear

# Show status
hister status
```

## Qutebrowser Integration

Hister provides a companion tool for qutebrowser users:

```bash
# Install the companion
hister companion qutebrowser

# This monitors browser tabs through the local Qt WebEngine DevTools endpoint
```

## Metrics & Monitoring

Built-in Prometheus metrics available at `/metrics`:

```
# Help
# TYPE hister_indexed_pages counter
hister_indexed_pages 12345
# HELP hister_index_duration_seconds
# TYPE hister_index_duration_seconds summary
hister_index_duration_seconds{quantile="0.5"} 0.234
```

## Security

- **Authentication**: Token-based auth via `Authorization` header
- **CORS**: Configurable CORS policies
- **HTTPS**: Recommended for production use
- **Data isolation**: All data stays in `~/.hister/`

## Pitfalls

1. **Safari limitation**: Safari doesn't expose history directly; export manually via Safari > Preferences > History.
2. **Large datasets**: Initial indexing of millions of pages can take hours. Use incremental indexing.
3. **Browser locks**: Chrome/Edge lock their History database when running. Close the browser before indexing or use SQLite's WAL mode.
4. **Path exclusions**: Always exclude large directories like `node_modules`, `.git`, and build artifacts.
5. **Token security**: Never commit auth tokens to version control. Use environment variables.

## Use Cases

### Developer Workflow
- Search through documentation you've bookmarked
- Find code snippets from Stack Overflow
- Locate blog posts about specific topics

### Research
- Find articles you read weeks ago
- Cross-reference notes with web sources
- Build reading lists from browsing history

### Personal Knowledge Management
- Never lose a useful link
- Rebuild context from browsing sessions
- Create searchable archive of web research

## Related Skills

- `web-discovery-techniques`: For web scraping workflows
- `research/arxiv`: For academic paper search
- `note-taking/obsidian`: For local note search integration

## Links

- [GitHub Repository](https://github.com/asciimoo/hister)
- [Documentation](https://hister.sh/docs)
- [Blog](https://blog.hister.sh)
