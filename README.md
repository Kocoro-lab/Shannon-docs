# Shannon Documentation

Official documentation for [Shannon](https://github.com/Kocoro-lab/Shannon) - Production AI Agent Orchestration Platform.

## Documentation Site

This repository contains the Mintlify-based documentation for Shannon. Visit the live site at [docs.shannon.dev](https://docs.shannon.dev) (coming soon).

## Local Development

### Prerequisites

- Node.js 18+ and npm
- Mintlify CLI

### Setup

```bash
# Install Mintlify CLI globally
npm i -g mint

# Start local development server
mint dev

# The site will be available at http://localhost:3000 (or next available port)
```

## Project Documents

- **[CLAUDE.md](./CLAUDE.md)**: Claude Code development guidelines for this repo

## Configuration

### mint.json

Main configuration file for the Mintlify site:

- Theme and branding
- Navigation structure
- Tab configuration
- External links

## Contributing to Documentation

### Adding New Pages

1. Create a new `.mdx` file in the appropriate directory
2. Add frontmatter with `title` and `description`
3. Reference the page in `mint.json` navigation
4. Test locally with `mint dev`

Example:

```mdx
---
title: "Page Title"
description: "Short description for SEO"
---

## Content starts here

Your markdown and MDX components...
```

