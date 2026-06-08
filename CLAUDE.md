# Agent Skills for Light Protocol

AI agent skills for rent-free Solana development using Light Protocol primitives.

## Structure

```
agent-skills/
├── skills/                      # 5 domain skills
│   ├── ask-mcp/
│   ├── compressed-pda/
│   ├── compressed-token/
│   ├── testing/
│   └── zk/
├── prompts/                     # Agent prompts (compressed-PDA programs + clients)
├── openclaw.plugin.json         # Plugin manifest
└── README.md
```

## Skills

| Name | Description |
|------|-------------|
| compressed-token | For compressed token operations on Solana ~400x cheaper than SPL: create mints with interface PDAs, mint, transfer, approve, revoke, compress, decompress, merge, Token-2022, and token distribution (airdrops). Compressed token accounts are always rent-free. @lightprotocol/compressed-token (TypeScript). |
| compressed-pda | For program development on Solana for per-user state, DePIN registrations, nullifiers, or custom compressed accounts ~160x cheaper and without rent-exemption. Programs invoke the Light System Program with a validity proof. Create, update, close, burn, and reinitialize compressed accounts. |
| zk | For custom ZK Solana programs and privacy-preserving applications to prevent double spending. Guide to integrate rent-free nullifier PDAs for double-spend prevention. |
| testing | For testing with Light Protocol programs and clients on localnet, devnet, and mainnet validation. |
| ask-mcp | For questions about compressed accounts, Light SDK, Solana development, Claude Code features, or agent skills. AI-powered answers grounded in repository context via DeepWiki MCP. |

## Adding a New Skill

1. Create skill directory:
```bash
mkdir skills/your-skill-name
```

2. Create `skills/your-skill-name/SKILL.md` with frontmatter:
```markdown
---
name: your-skill-name
description: "One-line description of what this skill does"
---

# Your Skill Title

Instructions and workflow...
```

3. Add to `openclaw.plugin.json`:
```json
"skills": [
  "skills/your-skill-name"
]
```

4. Optional: Add `scripts/`, `references/`, `assets/` subdirectories as needed.

## Conventions

- SKILL.md frontmatter requires `name` and `description` fields
- Use sentence case for headings
- MIT license for all contributions
- Skills follow Agent Skills Specification (https://agentskills.io)
