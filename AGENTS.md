# Context7 Skill — Agent Index

## Repo Structure

```
├── skills/context7/               # Skill definition and content
│   ├── SKILL.md                   # Skill metadata, triggers, workflow
│   └── scripts/
│       └── context7.sh            # REST API wrapper (search + docs)
├── evals/                         # Skill evaluation tests
├── Build/                         # Build artifacts
├── .github/workflows/             # CI: lint, release, auto-merge-deps, harness-verify
├── composer.json                  # Composer package (ai-agent-skill type)
├── docs/                          # Architecture and execution plans
│   └── ARCHITECTURE.md
└── scripts/                       # Repo-level scripts (verify-harness.sh)
```

## Commands

No Makefile or npm scripts. Key commands:

- `skills/context7/scripts/context7.sh search "library-name"` — search for a library ID
- `skills/context7/scripts/context7.sh docs "<library-id>" "[topic]" "[mode]"` — fetch library docs
- `bash scripts/verify-harness.sh --format=text --status` — verify harness maturity

## Rules

- Use REST API directly, not MCP protocol (avoids persistent context overhead)
- Library IDs follow `/vendor/library` format (e.g., `/facebook/react`)
- Two fetch modes: `code` (API references, default) and `info` (conceptual guides)
- Optional `CONTEXT7_API_KEY` env var for higher rate limits
- Dependencies: curl or fetch, jq
- Split license: MIT for code, CC-BY-SA-4.0 for content

## References

- [skills/context7/SKILL.md](skills/context7/SKILL.md) — skill definition, triggers, workflow
- [skills/context7/scripts/context7.sh](skills/context7/scripts/context7.sh) — REST API wrapper script
- [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) — architecture overview
- [README.md](README.md) — installation, usage, comparison with MCP
