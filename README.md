<h1 align="center">
  <a target="_blank" href="https://hanzo.ai">
    <img
      align="center"
      alt="Hanzo Auto"
      src="https://hanzo.ai/logo.png"
      style="width:200px;"
    />
  </a>
</h1>

<h2 align="center">Hanzo Auto</h2>

<p align="center">
  <a href="/LICENSE" target="_blank"><img src='https://img.shields.io/badge/license-MIT-green?style=for-the-badge' /></a>&nbsp;
  <a href='https://github.com/hanzoai/auto'><img src='https://img.shields.io/github/stars/hanzoai/auto?style=for-the-badge' /></a>&nbsp;
  <a href='https://hanzo.ai/discord'><img src='https://img.shields.io/badge/Discord-Join-blue?style=for-the-badge' /></a>
</p>

<p align="center">
   Workflow automation platform powered by Hanzo AI infrastructure
</p>

<p align="center">
  <a href="https://hanzo.ai/docs/auto" target="_blank"><b>Documentation</b></a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="https://hanzo.ai/docs/auto/pieces" target="_blank"><b>Create a Piece</b></a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="https://hanzo.ai/docs/auto/deploy" target="_blank"><b>Deploy</b></a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="https://hanzo.ai/discord" target="_blank"><b>Join Discord</b></a>
</p>

<br>

## Overview

Hanzo Auto is an all-in-one AI workflow automation platform that is:

- **Extensible** through a type-safe pieces framework written in TypeScript
- **AI-First** with native AI pieces for various providers
- **Enterprise-Ready** with self-hosting, branding, and control options
- **Powered by Hanzo Infrastructure** using @hanzo/mq and @hanzo/kv-client

This project is based on [Activepieces](https://github.com/activepieces/activepieces) and is part of the [Hanzo AI](https://hanzo.ai) ecosystem.

## Hanzo Product Ecosystem

| Product | Description |
|---------|-------------|
| **[Hanzo Auto](https://github.com/hanzoai/auto)** | Workflow automation (this repo) |
| **[Hanzo Flow](https://github.com/hanzoai/flow)** | Visual AI/LLM workflow builder |
| **[@hanzo/mq](https://github.com/hanzoai/mq)** | Message queue (BullMQ fork) |
| **[@hanzo/kv-client](https://github.com/hanzoai/kv-client)** | KV client for Node.js |
| **[Hanzo KV](https://github.com/hanzoai/kv)** | High-performance KV server |

## Features

### Builder Features
- Loops and Branches
- Auto Retries
- HTTP requests
- Code with NPM
- AI-assisted code generation
- Flow versioning
- Language translations
- Customizable templates
- 280+ Pieces (integrations)

### Why Hanzo Auto

- **Intuitive Interface**: Great experience for both technical and non-technical users
- **Open Ecosystem**: All pieces are open source and on npmjs.com
- **MCP Support**: All pieces available as MCP servers for LLMs
- **TypeScript Pieces**: Full customization with hot reloading for local development
- **AI-First**: Native AI pieces with support for various providers
- **Enterprise-Ready**: Self-hosted with full branding customization
- **Secure by Design**: Self-hosted and network-gapped options
- **Human in the Loop**: Approval workflows and delayed execution
- **Human Input Interfaces**: Chat and Form interfaces built-in

## Quick Start

### Prerequisites

- Node.js 20+
- Docker and Docker Compose

### Development

```bash
# Install dependencies
npm install

# Start development (all services)
npm run dev

# Start backend only
npm run dev:backend

# Start frontend only
npm run serve:frontend
```

### Docker

```bash
# Production-like setup
docker compose up

# Development
docker compose -f docker-compose.dev.yml up
```

## Creating Pieces

Pieces are modular integrations that can be created with the CLI:

```bash
# Create a new piece
npm run create-piece

# Add action to existing piece
npm run create-action

# Add trigger to existing piece
npm run create-trigger

# Sync piece metadata
npm run sync-pieces
```

## Architecture

### Monorepo Structure (Nx)

```
packages/
├── cli/           # CLI for piece development
├── engine/        # Flow execution engine
├── ee/            # Enterprise features
├── pieces/        # Integrations (community + custom)
├── react-ui/      # Frontend (React 18 + Vite)
├── server/        # Backend services
│   ├── api/       # Fastify REST API
│   ├── shared/    # Server utilities
│   └── worker/    # Background job workers
├── shared/        # Common types and utilities
└── tests-e2e/     # Playwright E2E tests
```

### Technology Stack

| Layer | Technology |
|-------|------------|
| Package Manager | Bun (via Nx) |
| Frontend | React 18, Vite, TailwindCSS 4, Radix UI |
| Backend | Fastify 5, Node.js |
| Database | PostgreSQL (TypeORM) |
| Queue | @hanzo/mq (BullMQ-compatible) |
| Cache | @hanzo/kv-client (Valkey/Redis-compatible) |
| Flow Canvas | @xyflow/react |
| AI | @ai-sdk/* (Anthropic, OpenAI, Google, etc.) |
| MCP | @modelcontextprotocol/sdk |

## Configuration

### Environment Variables

Copy `.env.example` to `.env` for local development.

Key variables:
- `AP_POSTGRES_*` - PostgreSQL connection
- `AP_REDIS_*` - Redis/Hanzo KV connection
- `AP_ENCRYPTION_KEY` - Encryption key for secrets
- `AP_JWT_SECRET` - JWT signing secret
- `AP_EXECUTION_MODE` - `SANDBOX` or `UNSANDBOX`
- `AP_PIECES_SOURCE` - `DB`, `FILE`, or `CLOUD_AND_DB`

## Testing

```bash
# E2E tests
npm run test:e2e

# Unit tests for specific package
nx test server-api
nx test shared
```

## Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## Syncing with Upstream

To merge upstream Activepieces changes:

```bash
git remote add upstream https://github.com/activepieces/activepieces.git
git fetch upstream
git merge upstream/main
# Resolve conflicts, keeping Hanzo-specific changes
```

## License

MIT (core), Enterprise license for ee/ packages

## Credits

- Based on [Activepieces](https://github.com/activepieces/activepieces)
- Built with [Hanzo AI](https://hanzo.ai) infrastructure
