# terse-mcp

Purpose-built MCP tools that respect your context window.

## What is this?

A collection of token-efficient [Model Context Protocol](https://modelcontextprotocol.io/) tools designed for AI-augmented development. Each tool produces compact, structured output optimized for LLM consumption rather than human readability.

Every tool runs as both an MCP server (JSON-RPC 2.0 over stdio) and a standalone CLI (`--cli` flag).

## Philosophy

- **Token-efficient**: Minimal output without sacrificing information
- **MCP-first**: Native Model Context Protocol implementations
- **Domain-specific**: Purpose-built for specific workflows, not general-purpose
- **Pragmatic**: Fast enough (Go-based), but token savings is the value proposition

## Tools

### Search & Replace

| Tool | Description | Language |
|------|-------------|----------|
| [checkfor](https://github.com/hegner123/checkfor) | Non-recursive multi-directory file search with compact JSON output. Designed for refactoring verification and progress tracking across multiple packages. | Go |
| [repfor](https://github.com/hegner123/repfor) | Safe multi-file string replacement. Exact string matching only (no regex), with dry-run preview. Built for systematic refactoring: rename functions, update imports, change constants. | Go |

### Web & Content

| Tool | Description | Language |
|------|-------------|----------|
| [webfetch-clean](https://github.com/hegner123/webfetch-clean) | Web fetcher that strips ads, scripts, navigation, and clutter. Outputs clean Markdown or HTML. 90-96% token savings over raw HTML fetching. | Go |

### File System

| Tool | Description | Language |
|------|-------------|----------|
| [stump](https://github.com/hegner123/stump) | Token-efficient directory tree visualization. 50%+ token reduction over `tree`. Configurable depth, smart filtering, symlink handling, performance metrics. | Zig |
| [list](https://github.com/hegner123/list) | Single-depth directory listing with compact JSON. Optional metadata (size, mtime, perms, subdirectory counts). Replaces verbose `ls` output. | Go |
| [notab](https://github.com/hegner123/notab) | Whitespace normalizer. Replaces tabs with spaces or vice versa. Inverse mode for Makefiles and other tab-required formats. | Go |

### RAG & Memory

| Tool | Description | Language |
|------|-------------|----------|
| [ingest](https://github.com/hegner123/ingest) | RAG document ingestion pipeline. Processes markdown into semantic vector embeddings stored in PostgreSQL+pgvector. Supports add, list, delete, and search operations. | Go |
| [mem](https://github.com/hegner123/mem) | Persistent memory store for AI agents. Key-value storage with tagging and full-text search, backed by SQLite. | Go |

### Encoding & Text

| Tool | Description | Language |
|------|-------------|----------|
| [utf8](https://github.com/hegner123/utf8) | Detects and fixes corrupted UTF-16 files (null-laced ASCII, missing BOMs, unpaired surrogates). Converts to clean UTF-8 in-place with backup. | Go |

### Execution & Scaffolding

| Tool | Description | Language |
|------|-------------|----------|
| [omni](https://github.com/hegner123/omni) | Parallel command execution. Runs commands across multiple arguments with flexible substitution patterns, configurable workers, and output buffering. | Go |
| [init](https://github.com/hegner123/init) | Lightweight project bootstrapper. Embeds and writes template files (LICENSE, CONTRIBUTING.md) at compile time. Refuses to overwrite existing files. | Go |

## Installation

Each tool builds to a single binary. Most use a `justfile` for build/test/install:

```bash
git clone https://github.com/hegner123/<tool>.git
cd <tool>
just install
```

## Requirements

Most tools need only Go 1.23+. Exceptions:

- **stump**: Zig 0.15.2+
- **ingest**: PostgreSQL with pgvector, Ollama with `nomic-embed-text`

## License

Each tool is independently licensed. See individual repositories for details.
