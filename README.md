# terse-mcp

Purpose-built MCP tools that respect your context window.

## What is this?

A collection of token-efficient [Model Context Protocol](https://modelcontextprotocol.io/) tools designed for AI-augmented development. Each tool produces compact, structured output optimized for LLM consumption rather than human readability.

Every tool runs as both an MCP server (JSON-RPC 2.0 over stdio) and a standalone CLI.

## Philosophy

- **Token-efficient**: Minimal output without sacrificing information
- **MCP-first**: Native Model Context Protocol implementations
- **Domain-specific**: Purpose-built for specific workflows, not general-purpose
- **Pragmatic**: Fast enough (mostly Go-based), but token savings is the value proposition

## Tools

### Search & Replace

| Tool | Description | Language |
|------|-------------|----------|
| [checkfor](https://github.com/hegner123/checkfor) | Non-recursive multi-directory file search with compact JSON output. Designed for refactoring verification and progress tracking across multiple packages. | Go |
| [repfor](https://github.com/hegner123/repfor) | Safe multi-file string replacement. Exact string matching only (no regex), with dry-run preview. Built for systematic refactoring: rename functions, update imports, change constants. | Go |

### Web & Content

| Tool | Description | Language |
|------|-------------|----------|
| [webfetch-clean](https://github.com/hegner123/webfetch-clean) | Web fetcher and screenshotter with aggressive HTML cleaning. Two processing modes: clean (strips ads, scripts, nav, clutter) and scrape (light pass, preserves structure). Outputs Markdown or HTML. Runs as MCP server, CLI, or HTTP API with token auth. 90-96% token savings over raw HTML. | Go |
| [shakespeare](https://github.com/hegner123/shakespeare) | Headless browser automation via Playwright. Navigate pages, take screenshots, execute JavaScript, inspect computed CSS, and test responsive layouts. Persistent browser instance across tool calls. | Node.js |

### File System

| Tool | Description | Language |
|------|-------------|----------|
| [stump](https://github.com/hegner123/stump) | Token-efficient directory tree visualization. 50%+ token reduction over `tree`. Configurable depth, smart filtering, symlink handling. | Zig |
| [list](https://github.com/hegner123/list) | Single-depth directory listing with compact JSON. Optional metadata (size, mtime, perms, subdirectory counts). Replaces verbose `ls` output. | Go |

### File Recovery

Tools that let AI agents recover from files they can't read or edit.

| Tool | Description | Language |
|------|-------------|----------|
| [notab](https://github.com/hegner123/notab) | Replaces all tabs in a file with spaces so AI agents can edit it. Inverse mode converts leading spaces back to tabs for Makefiles and other tab-required formats. | Go |
| [utf8](https://github.com/hegner123/utf8) | Corrects malformed UTF-16 and UTF-8 files into readable UTF-8. Fixes null-laced ASCII, missing BOMs, and unpaired surrogates in-place with backup. | Go |

### RAG & Memory

| Tool | Description | Language |
|------|-------------|----------|
| [ingest](https://github.com/hegner123/ingest) | RAG document ingestion pipeline. Processes markdown into semantic vector embeddings stored in PostgreSQL+pgvector. Supports add, list, delete, and search operations. | Go |
| rag_search | Semantic search over RAG documents via pgvector cosine similarity. Query text is embedded via Ollama, matched against stored vectors, with optional language filtering. | Go |
| rag-writer | Offloads RAG doc generation to direct Anthropic API calls. Reads source files, generates markdown documentation, and ingests into the vector store. | Python |
| [mem](https://github.com/hegner123/mem) | Persistent memory store for AI agents. Key-value storage with tagging and full-text search, backed by SQLite. | Go |

### Agent Coordination

| Tool | Description | Language |
|------|-------------|----------|
| [hq](https://github.com/hegner123/hq) | Multi-agent coordination server. Atomic step claiming, dependency management, heartbeat monitoring, and crash recovery via SQLite. Enables concurrent AI agents working on shared projects. | Go |

### Execution & Scaffolding

| Tool | Description | Language |
|------|-------------|----------|
| [omni](https://github.com/hegner123/omni) | Parallel command execution. Runs commands across multiple arguments with flexible substitution patterns, configurable workers, and output buffering. | Go |
| [init](https://github.com/hegner123/init) | Lightweight project bootstrapper. Embeds and writes template files (LICENSE, CONTRIBUTING.md) at compile time. Refuses to overwrite existing files. | Go |

### Planned

| Tool | Description | Status |
|------|-------------|--------|
| chunker | JSON chunking for large files. Inspect structure, paginate by size, extract by path, search keys/values. Stateless size-based splitting for arrays and objects. | Planned |
| dewey | Claude-optimized document metadata format (`.claude` files). Hyper-terse indexing for navigating large documents that exceed token limits. | Spec |
| memory-mux | Tiered memory multiplexer across scratch (in-memory SQLite), short-term, and long-term (PostgreSQL) storage with soft deletes and LLM-driven maintenance. | Spec |

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
- **shakespeare**: Node.js + Playwright
- **rag-writer**: Python 3 + Anthropic SDK
- **ingest**, **rag_search**: PostgreSQL with pgvector, Ollama with `nomic-embed-text`
- **hq**, **mem**: No external dependencies (embedded SQLite)

## Platform Support

- macOS
- Linux

Windows is not supported.

## License

Each tool is independently licensed. See individual repositories for details.
