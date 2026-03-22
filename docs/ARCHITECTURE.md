# Architecture — Context7 Skill

## Purpose

The Context7 Skill provides AI agents with on-demand access to current library documentation via the Context7 REST API. It is a lightweight alternative to the Context7 MCP server, avoiding persistent context overhead from tool schemas.

## Component Map

```
┌──────────────────────────────────────────────┐
│  SKILL.md (entry point)                      │
│  Triggers: "how to use library", "API docs", │
│  "framework pattern", import statements      │
└──────────┬───────────────────────────────────┘
           │
           ▼
┌──────────────────────┐
│  context7.sh         │
│  (REST API wrapper)  │
└──────┬───────┬───────┘
       │       │
       ▼       ▼
   search    docs
   command   command
       │       │
       ▼       ▼
┌──────────────────────┐
│  Context7 REST API   │
│  (api.context7.com)  │
└──────────────────────┘
```

## Key Components

### SKILL.md (`skills/context7/SKILL.md`)
Entry point for AI agents. Defines triggers, workflow steps, and script invocation patterns.

### context7.sh (`skills/context7/scripts/context7.sh`)
Bash wrapper around the Context7 REST API with two subcommands:
- **search** — Queries the API for library IDs matching a name. Returns `/vendor/library` formatted IDs.
- **docs** — Fetches documentation for a given library ID with optional topic filter and mode selection (`code` for API refs, `info` for guides).

## Integration Points

- **AI Agent** — Reads SKILL.md, invokes context7.sh via Bash tool
- **Context7 REST API** — `api.context7.com` provides curated documentation for 50+ libraries
- **Composer** — Installable as a PHP package via `netresearch/composer-agent-skill-plugin`

## Data Flow

1. User asks about a library (e.g., "How do I use React hooks?")
2. SKILL.md triggers activation
3. Agent runs `context7.sh search "react"` to find library ID
4. Agent runs `context7.sh docs "/facebook/react" "hooks"` to fetch docs
5. Agent applies returned documentation to answer the question

## Context Efficiency

| Aspect | MCP Server | This Skill |
|--------|------------|------------|
| Idle cost | ~500-2000 tokens (tool schemas) | ~100 tokens (SKILL.md) |
| Invocation | Via MCP protocol | Direct REST via Bash |
| Dependencies | MCP runtime | curl, jq |
