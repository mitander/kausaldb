# kausaldb

[![CI Status](https://github.com/mitander/kausaldb/actions/workflows/ci.yml/badge.svg)](https://github.com/mitander/kausaldb/actions)
[![LICENSE](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

> Code is a graph. Query it. Fast.

Your codebase is a network of dependencies, not a flat directory of text files. Traditional tools like `grep` and semantic search find text, not causality.

KausalDB is purpose-built graph database for fast and reliable context retrieval for LLMs and developers.

## Quick Start

```bash
# Install the required Zig toolchain
./scripts/install_zig.sh

# Build the project and run all tests
./zig/zig build test
```

## The Query

Model your code as a directed graph to enable queries that understand software structure.

For example, imagine in your code the function `main()` calls `helper_function()`. You can find this relationship directly:

```bash
# 1. Link your codebase to a workspace
kausal link --path /path/to/your-project --name myproject

# 2. Find what calls `helper_function`
kausal show --relation callers --target helper_function --workspace myproject

# 3. The causal link.
✓ Found 1 caller:
└─ main
```

## Design

Built from scratch in Zig with zero-cost abstractions, no hidden allocations, O(1) memory cleanup and no data races by design.

- **LSM-Tree Storage:** Fast write-heavy codebase ingestion.
- **Single-Threaded Core:** No data races by design for stability and simplicity.
- **Zero-Cost Abstractions:** Enforce ownership and arena models at compile time.
- **Deterministic Testing:** Uses Virtual File System to enable reproducible, simulation-based testing of complex failure scenarios.

## Documentation

See [`docs/`](docs/) for detailed design, development guide, and testing philosophy.
