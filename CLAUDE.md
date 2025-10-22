# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is the documentation repository for Shannon - a production-grade AI agent orchestration platform. The docs are built with Mintlify and deployed to docs.shannon.dev.

Shannon itself is a distributed microservices system built with:
- Go (Gateway, Orchestrator)
- Rust (Agent Core)
- Python (LLM Service)
- Temporal for workflow orchestration
- PostgreSQL, Redis, Qdrant for data storage

## Documentation Development

### Running the Docs Locally

```bash
# Install Mintlify CLI (if not installed)
npm i -g mint

# Start local development server
mint dev

# The site will be available at http://localhost:3000 (or next available port)
```

### Project Structure

```
docs/
├── mint.json              # Main configuration (navigation, theme, tabs)
├── api/                   # API Reference documentation
│   ├── overview.mdx
│   ├── authentication.mdx
│   ├── event-types.mdx
│   ├── endpoints/         # Legacy API endpoint docs
│   └── rest/              # REST API documentation
├── quickstart/            # Getting Started guides
│   ├── index.mdx          # Welcome page
│   ├── installation.mdx
│   ├── quickstart.mdx
│   ├── configuration.mdx
│   ├── troubleshooting.mdx
│   └── concepts/          # Core concepts (agents, workflows, etc.)
├── sdk/                   # SDK documentation
│   └── python/            # Python SDK docs
├── tutorials/             # Tutorial content
├── deployment/            # Production deployment guides
├── architecture/          # System architecture docs
└── logo/                  # Brand assets
```

## Shannon Architecture Context

When working on documentation, understanding Shannon's architecture helps create accurate content:

### Core Components

1. **Gateway** (Port 8080) - Go REST API layer
   - Authentication and rate limiting
   - HTTP/JSON interface
   - SSE streaming support

2. **Orchestrator** (Port 50052) - Go + Temporal
   - Central workflow coordination
   - Task routing and decomposition
   - Cognitive pattern selection (CoT, ToT, ReAct)
   - Budget and token enforcement

3. **Agent Core** (Port 50051) - Rust
   - WASI sandboxing for secure code execution
   - Tool registry and execution
   - Circuit breakers

4. **LLM Service** (Port 8000) - Python + FastAPI
   - Multi-provider LLM gateway (OpenAI, Anthropic, Google, etc.)
   - Intelligent caching
   - MCP tool integration

5. **Data Stores**
   - PostgreSQL: Task metadata, sessions, history
   - Redis: Caching and pub/sub
   - Qdrant: Vector database for semantic memory
   - Temporal: Workflow state

### Key Concepts

- **Agents**: AI agents with specific roles and capabilities
- **Workflows**: Durable Temporal workflows that orchestrate agent execution
- **Cognitive Patterns**: CoT (Chain-of-Thought), ToT (Tree-of-Thoughts), ReAct
- **WASI Sandboxing**: Secure Python code execution in WebAssembly
- **Budget Control**: Token limits and cost management (85-95% cost savings)
- **Multi-tenancy**: Session-based isolation

### API Structure

- **REST API**: `/api/v1` base path
  - Task submission: `POST /tasks`
  - Task status: `GET /tasks/{id}`
  - Task streaming: `GET /tasks/{id}/stream` (SSE)
  - List tasks: `GET /tasks`

- **gRPC API**: Direct access to Orchestrator (50052) and Agent Core (50051)

- **Authentication**: Disabled by default (`GATEWAY_SKIP_AUTH=1`), API key-based when enabled

## Documentation Guidelines

### Adding New Pages

1. Create `.mdx` file in appropriate directory
2. Add frontmatter with `title` and `description`:
   ```mdx
   ---
   title: "Page Title"
   description: "Short description for SEO"
   ---
   ```
3. Reference page in `mint.json` navigation
4. Test locally with `mint dev`

### Navigation Structure

The `mint.json` file defines:
- **Tabs**: Top-level sections (Quick Start, API Reference, SDKs, etc.)
- **Navigation Groups**: Sidebar organization within each tab
- **Page Order**: Sequence matters for navigation

Key tabs:
- `quickstart/` - Getting Started and Core Concepts
- `api/` - API Reference (REST and gRPC)
- `sdk/` - SDK documentation (Python, future: Go, JS)
- `tutorials/` - Tutorial content
- `deployment/` - Production deployment guides
- `architecture/` - System design and deep dives

### Content Best Practices

1. **Use Mintlify Components**:
   - `<Card>`, `<CardGroup>` for navigation blocks
   - `<Note>`, `<Warning>`, `<Tip>` for callouts
   - `<Steps>` for sequential instructions
   - `<Accordion>`, `<AccordionGroup>` for collapsible content
   - Code blocks with syntax highlighting

2. **Code Examples**: Include curl, Python SDK, and raw HTTP examples where applicable

3. **Mermaid Diagrams**: Use for architecture and flow visualization

4. **Cross-linking**: Link to related pages using relative paths

5. **Consistency**:
   - Port numbers: Gateway (8080), Orchestrator (50052), Agent Core (50051), LLM Service (8000)
   - Default auth state: `GATEWAY_SKIP_AUTH=1` for development
   - Repository: `https://github.com/Kocoro-lab/Shannon`

### Common Patterns

**Installation commands**:
```bash
git clone https://github.com/Kocoro-lab/Shannon.git
cd Shannon
make setup
echo "OPENAI_API_KEY=sk-your-key-here" >> .env
./scripts/setup_python_wasi.sh
make dev
```

**API Request Example**:
```bash
curl -X POST http://localhost:8080/api/v1/tasks \
  -H "Content-Type: application/json" \
  -d '{"query": "Your task here"}'
```

**Python SDK Example**:
```python
from shannon import Client

client = Client(base_url="http://localhost:8080")
result = client.submit_task("Your task here")
```

## Theme and Branding

- Primary color: `#0070F3`
- Light accent: `#00A3FF`
- Dark accent: `#0051C3`
- Topbar style: gradient
- Logo files: `/logo/dark.svg`, `/logo/light.svg`
- Favicon: `/favicon.svg`

## External Links

- Main Shannon repo: https://github.com/Kocoro-lab/Shannon
- Company site: https://kocoro.ai
- Discord community: https://discord.gg/NB7C2fMcQR
- Twitter: https://x.com/shannon_agents

## Development Status

Shannon is in active development. Documentation phases:
- Phase 1: Core documentation (Complete)
- Phase 2: API Reference and SDK docs (Complete)
- Phase 3: Deployment guides and tutorials (In Progress - marked with 🚧)

When documenting Phase 3 content, include appropriate warnings about active development status.
