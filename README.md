# Context7 Documentation Lookup Skill

Fetch up-to-date library documentation via Context7 REST API. Lightweight alternative to Context7 MCP with no persistent context overhead.

## Features

- **No MCP Overhead** - Uses REST API directly, no tool schemas consuming context
- **Current Documentation** - Fetches live docs from Context7's curated database
- **Topic Filtering** - Focus on specific areas (hooks, routing, middleware, etc.)
- **50+ Libraries** - React, Next.js, Vue, Express, Prisma, and more

## Installation

### Marketplace (Recommended)

Add the [Netresearch marketplace](https://github.com/netresearch/claude-code-marketplace) once, then browse and install skills:

```bash
# Claude Code
/plugin marketplace add netresearch/claude-code-marketplace
```

### npx ([skills.sh](https://skills.sh))

Install with any [Agent Skills](https://agentskills.io)-compatible agent:

```bash
npx skills add https://github.com/netresearch/context7-skill --skill context7
```

### Download Release

Download the [latest release](https://github.com/netresearch/context7-skill/releases/latest) and extract to your agent's skills directory.

### Git Clone

```bash
git clone https://github.com/netresearch/context7-skill.git
```

### Composer (PHP Projects)

```bash
composer require netresearch/context7-skill
```

Requires [netresearch/composer-agent-skill-plugin](https://github.com/netresearch/composer-agent-skill-plugin).

### npm (Node Projects)

```bash
npm install --save-dev \
  @netresearch/agent-skill-coordinator \
  github:netresearch/context7-skill
```

Requires [@netresearch/agent-skill-coordinator](https://github.com/netresearch/node-agent-skill-coordinator), which discovers the skill in `node_modules` and registers it in `AGENTS.md` via a `postinstall` hook. For pnpm, also allowlist the coordinator's postinstall:

```json
{
  "pnpm": {
    "onlyBuiltDependencies": ["@netresearch/agent-skill-coordinator"]
  }
}
```

## Usage

The skill triggers on keywords like:
- "how do I use [library]"
- "what's the API for [library]"
- "[library] documentation"
- "show me [library] patterns"

### Example Prompts

```
"How do I use React hooks?"
"What's the Next.js App Router API?"
"Show me Prisma query patterns"
"Express middleware documentation"
```

### Manual Script Usage

```bash
# Search for a library ID
scripts/context7.sh search "prisma"

# Fetch documentation with topic
scripts/context7.sh docs "/prisma/prisma" "queries"
```

## Structure

```
context7/
├── SKILL.md              # AI instructions
├── README.md             # This file
├── LICENSE-MIT           # Code license (MIT)
├── LICENSE-CC-BY-SA-4.0  # Content license (CC-BY-SA-4.0)
├── scripts/              # Automation scripts
│   └── context7.sh       # REST API wrapper
└── .github/
    └── workflows/
        └── release.yml   # Release packaging
```

## Why Use This Over Context7 MCP?

| Aspect | MCP Server | This Skill |
|--------|------------|------------|
| Context cost | ~500-2000 tokens always | ~100 tokens on-demand |
| Tool schemas | Always in context | None |
| Invocation | Model decides | Model decides |
| API access | Via MCP protocol | Direct REST API |

Best for: Users who occasionally need library docs but don't want persistent context overhead.

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `CONTEXT7_API_KEY` | No | API key for higher rate limits |

## Contributing

Contributions welcome! Please submit PRs for:
- Adding common library IDs
- Improving script error handling
- Documentation updates

## License

This project uses split licensing:

- **Code** (scripts, workflows, configs): [MIT](LICENSE-MIT)
- **Content** (skill definitions, documentation, references): [CC-BY-SA-4.0](LICENSE-CC-BY-SA-4.0)

See the individual license files for full terms.
## Credits

- Context7 API by [Upstash](https://upstash.com/)
- Skill developed by [Netresearch DTT GmbH](https://www.netresearch.de/)

---

**Made with love for Open Source by [Netresearch](https://www.netresearch.de/)**
