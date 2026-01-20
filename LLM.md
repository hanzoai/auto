# Hanzo Auto - AI Assistant Guide

## Overview
Hanzo Auto is a workflow automation platform (forked from Activepieces) that allows users to build automated workflows connecting various services through a visual flow builder. It's part of the Hanzo ecosystem, powered by Hanzo MQ and Hanzo KV.

**Version**: 0.77.4 (based on Activepieces)
**License**: MIT (core), Enterprise for ee/ packages
**Upstream**: [activepieces/activepieces](https://github.com/activepieces/activepieces)

## Hanzo Ecosystem Integration

### Product Lineup
- **Hanzo Flow** - Visual AI/LLM workflow builder (Langflow fork)
- **Hanzo Auto** - Automation platform: triggers, jobs, integrations (this repo)
- **Hanzo MQ** - Message queue infrastructure (BullMQ fork)
- **Hanzo KV** - Key-value store (Valkey/Redis fork)

### Infrastructure Dependencies
| Component | Package | Upstream |
|-----------|---------|----------|
| Message Queue | `@hanzo/mq` | taskforcesh/bullmq |
| KV Client | `@hanzo/kv-client` | valkey-io/iovalkey |
| KV Server | Hanzo KV | valkey-io/valkey |

## Architecture

### Monorepo Structure (Nx)
```
packages/
├── cli/           # CLI for piece development and worker management
├── engine/        # Flow execution engine (isolated-vm sandboxed)
├── ee/            # Enterprise features (SAML, audit logs, etc.)
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
| Flow Canvas | @xyflow/react (React Flow) |
| AI | @ai-sdk/* (Anthropic, OpenAI, Google, etc.) |
| MCP | @modelcontextprotocol/sdk |

## Development Commands

```bash
# Start development (all services)
npm run dev

# Start backend only
npm run dev:backend

# Create pieces
npm run create-piece     # New piece
npm run create-action    # Add action
npm run create-trigger   # Add trigger

# Testing
npm run test:e2e         # E2E tests
nx test <package>        # Unit tests
```

## Hanzo-Specific Changes

### Queue Integration
All queue operations use `@hanzo/mq` instead of `bullmq`:
```typescript
import { Queue, Worker, Job } from '@hanzo/mq'
```

### KV/Redis Client
For direct KV operations, use `@hanzo/kv-client`:
```typescript
import HanzoKV from '@hanzo/kv-client'
const client = new HanzoKV({ host: 'localhost', port: 6379 })
```

### Configuration
Hanzo Auto uses the same environment variables as Activepieces, with optional Hanzo-specific overrides:
- `AP_REDIS_*` → Works with Hanzo KV (Valkey-compatible)
- Queue configuration works with Hanzo MQ

## Syncing with Upstream

To merge upstream changes:
```bash
git remote add upstream https://github.com/activepieces/activepieces.git
git fetch upstream
git merge upstream/main
# Resolve conflicts, keeping Hanzo-specific changes
```

## Notes for AI Assistants

1. **Use Hanzo packages** - Import from `@hanzo/mq` and `@hanzo/kv-client`, not bullmq/ioredis
2. **Follow upstream patterns** - The codebase follows Activepieces conventions
3. **TypeBox for schemas** - Use @sinclair/typebox, not Zod
4. **Test locally** - Use `npm run cli` for piece development
5. **Document Hanzo changes** - Keep this LLM.md updated with Hanzo-specific modifications

## Related Repositories

- [hanzoai/mq](https://github.com/hanzoai/mq) - @hanzo/mq (BullMQ fork)
- [hanzoai/kv-client](https://github.com/hanzoai/kv-client) - @hanzo/kv-client (iovalkey fork)
- [hanzoai/kv](https://github.com/hanzoai/kv) - Hanzo KV server (Valkey fork)
