# DEVELOPMENT

A practical overview of the development workflow, code structure, and debugging tools.

## 1. Setup

First, clone the repository and run the setup script. This will install the correct version of the Zig toolchain into a local `./zig/` directory.

```bash
git clone https://github.com/mitander/kausaldb
cd kausaldb
./scripts/install_zig.sh
```

The project includes Git hooks that automate formatting and testing before each commit.

## 2. Workflow

The build system (`build.zig`) provides several targets to support a fast and reliable development cycle.

- **Run fast tests (dev loop):**
  This is your main command during development. It runs all unit tests and fast integration tests.

  ```bash
  ./zig/zig build test
  ```

- **Format code:**
  We use `zig fmt` to maintain a consistent code style.

  ```bash
  ./zig/zig build fmt
  ```

- **Check for style violations:**
  The `tidy` checker enforces project-specific naming and style conventions.

  ```bash
  ./zig/zig build tidy
  ```

- **Run the full validation suite (before PR):**
  This command runs the complete test suite, including longer scenario and E2E tests.
  ```bash
  ./zig/zig build test-all
  ```

## 4. Code Structure

The source code is organized by functionality in the `src/` directory:

- `src/core/`: Fundamental data structures (`types.zig`), memory management (`memory.zig`, `arena.zig`), and the VFS abstraction (`vfs.zig`).
- `src/storage/`: The LSM-Tree implementation, including the WAL (`wal/`), memtable (`block_index.zig`), SSTables (`sstable.zig`), and compaction logic.
- `src/query/`: The query engine, graph traversal algorithms, and caching.
- `src/cli/`: The command-line interface, including the parser, client, and renderer.
- `src/server/`: The TCP server daemon and connection manager.
- `src/testing/`: The core simulation framework, including the test harness, workload generator, and property checkers.
- `src/sim/`: The deterministic simulation components, including the `SimulationVFS`.
