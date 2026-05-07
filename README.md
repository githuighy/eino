# Eino

A fork of [cloudwego/eino](https://github.com/cloudwego/eino) — a powerful LLM application development framework for Go.

## Overview

Eino provides a clean, composable framework for building LLM-powered applications in Go. It offers:

- **Component Abstractions**: Standardized interfaces for LLMs, retrievers, tools, and more
- **Graph-based Orchestration**: Build complex AI pipelines using a directed graph model
- **Streaming Support**: First-class support for streaming responses
- **Type Safety**: Strongly typed components with Go generics
- **Observability**: Built-in tracing and callback hooks

## Installation

```bash
go get github.com/your-org/eino
```

## Quick Start

```go
package main

import (
    "context"
    "fmt"
    "log"

    "github.com/your-org/eino/compose"
)

func main() {
    ctx := context.Background()

    // Build a simple chain
    chain, err := compose.NewChain[string, string]()
    if err != nil {
        log.Fatal(err)
    }

    result, err := chain.Invoke(ctx, "Hello, Eino!")
    if err != nil {
        log.Fatal(err)
    }

    fmt.Println(result)
}
```

## Project Structure

```
eino/
├── compose/        # Graph and chain orchestration
├── components/     # Core component interfaces
│   ├── model/      # LLM model interfaces
│   ├── retriever/  # Document retriever interfaces
│   ├── tool/       # Tool/function call interfaces
│   └── prompt/     # Prompt template interfaces
├── schema/         # Shared data types and schemas
└── utils/          # Utility helpers
```

## Personal Notes

> **Fork purpose**: I'm using this fork to experiment with custom retriever implementations and to learn how the graph-based orchestration works under the hood. The upstream repo moves fast, so I periodically sync from `cloudwego/eino`.

### My Experiments

- `components/retriever/` — working on a custom BM25 retriever backed by a local SQLite index
- `compose/` — adding debug logging to graph execution to better understand node traversal order

### Sync Log

| Date | Synced from upstream | Notes |
|------|----------------------|-------|
| 2025-06-10 | `cloudwego/eino@main` | Initial fork |
| 2025-07-01 | `cloudwego/eino@main` | Picked up streaming fixes |

## Contributing

We welcome contributions! Please see our [Pull Request Template](.github/PULL_REQUEST_TEMPLATE.md) and review the [contribution guidelines](.github/ISSUE_TEMPLATE) before submitting.

### Development

```bash
# Run all tests
go test ./...

# Run tests with race detector
go test -race ./...

# Run linter
golangci-lint run
```

## License

This project is licensed under the Apache License 2.0 — see the [LICENSE](LICENSE) file for details.

## Acknowledgements

This project is a fork of [cloudwego/eino](https://github.com/cloudwego/eino), originally developed by the CloudWeGo team at ByteDance.
