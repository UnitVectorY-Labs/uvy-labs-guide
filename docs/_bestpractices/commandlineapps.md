---
layout: default
title: Command Line Apps
---

# Command Line Apps

UnitVectorY Labs command line applications follow a consistent set of conventions to ensure tools are interoperable, easy to use, and friendly to both humans and AI agents.

## Language Choice

Prefer Go for command line applications. Go compiles to small, standalone binaries that work natively on macOS, Linux, and Windows without dependencies. This eliminates the need for users to install a runtime and keeps distribution simple.

## NO_COLOR Support

All command line tools should respect the [`NO_COLOR` environment variable convention](https://no-color.org). When `NO_COLOR` is set to any value, the application must disable all colored output. This supports accessibility, logging to files without escape codes, and users who prefer plain terminal output.

## Unix Conventions

Command line utilities should follow Unix conventions:

- **Standard streams** — Normal output goes to `stdout`. Errors and diagnostic messages go to `stderr`. Input can be read from `stdin` when appropriate.
- **Piping** — Design tools so their output can be piped into other commands. Avoid writing to `stderr` for normal data.
- **Configuration** — Accept configuration via environment variables or command-line flags, with sensible defaults. Environment variables take precedence over flags when both are provided.
- **Flag naming** — Use kebab-case for all flags (e.g., `--api-key`, `--config-file`, `--output-dir`). Short flags are reserved for common options like `-v` (version) and `-h` (help).

## Progress Bars

Tools that display progress or loading indicators should support a `--no-progress` flag to suppress all progress output. This is useful for scripting, CI pipelines, and when the tool's output is being consumed by another program.

## TUI Applications

For interactive terminal user interfaces, prefer [Bubble Tea](https://github.com/charmbracelet/bubbletea) by Charm. It is the organization's established TUI framework, providing a clean functional programming model and a rich ecosystem of components.

## Help Output

Every command line application must provide a `--help` flag that clearly describes how to use the tool, including available commands, flags, environment variables, and example usage. Clear help output is especially important for AI agents that need to understand how to invoke the tool correctly.

## Version Output

Every command line application must provide a `--version` flag that prints the version the binary was built with. Version should be injected at build time via linker flags and fall back to runtime build info inspection. The standard format is:

```
projectName version vX.Y.Z (goX.Y, os/arch)
```

## Exit Codes

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | General error or flag parse failure |
| 2 | Invalid usage or bad flags |

Domain-specific exit codes (3-255) may be used when there is a need to distinguish error types for consumers of the tool.
