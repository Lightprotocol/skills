# Agent Skills for Light Protocol

AI agent skills for rent-free Solana development using Light Protocol primitives.

## Structure

```
agent-skills/
├── skills/                      # 9 domain skills + skill-check
│   ├── token-distribution/
│   ├── ask-mcp/
│   ├── data-streaming/
│   ├── light-sdk/
│   ├── light-token-client/
│   ├── solana-compression/
│   ├── payments-and-wallets/
│   ├── testing/
│   ├── zk-nullifier/
│   └── skill-check/
├── eval/                        # Promptfoo eval suite
│   ├── datasets/                # Test cases (routing, quality, security)
│   ├── prompts/                 # Generated routing prompts
│   └── scripts/                 # Python providers and builders
├── scripts/                     # Utility scripts
│   └── sync-to-docs.sh
├── openclaw.plugin.json         # Plugin manifest
└── README.md
```

## Skills

| Name | Description |
|------|-------------|
| token-distribution | Distribute SPL tokens with 5000x cheaper cost. For airdrops, DePIN, or token distribution. Can implement custom claim for advanced usage. |
| ask-mcp | Query Light Protocol and related repositories via DeepWiki MCP. Use when answering questions about compressed accounts, Light SDK, Solana development, Claude Code features, or agent skills. |
| data-streaming | Stream Light Protocol account state via Laserstream gRPC. Covers token accounts, mint accounts, and compressible PDAs with hot/cold lifecycle tracking. |
| light-sdk | Build rent-free Solana programs with Light SDK. For DeFi (AMMs, vaults, lending), infrastructure, or any Solana program. Anchor macros or Pinocchio patterns. Covers state structs, account creation, CPI, client SDK, router integration, and testing. |
| light-token-client | Use Light Token client SDKs (TypeScript and Rust). Cookbook for creating mints, associated token accounts, transfers, and more. |
| solana-compression | Build compressed PDA programs on Solana with Light System Program CPI. Create, update, close, burn, reinitialize compressed accounts. Client integration and testing. |
| payments-and-wallets | Build payment flows and wallet integrations with light-token. Covers receive/send/balance/history, client-side signing patterns for Privy and Solana wallet adapters, nullifier-based double-spend prevention. |
| testing | Test Light Protocol programs and clients for localnet, devnet and mainnet. |
| zk-nullifier | Use for privacy preserving applications and ZK Solana programs. Prevents double spending using rent-free PDAs. |
| skill-check | Run promptfoo eval suites against Light Protocol agent-skills. Tests routing accuracy, output quality, and adversarial security. |

## Running Evals

Set environment variables:
```bash
export PROMPTFOO_DISABLE_TELEMETRY=1
export PROMPTFOO_DISABLE_UPDATE=1
```

Run all suites:
```bash
npx promptfoo@latest eval
```

Run specific suite:
```bash
npx promptfoo@latest eval -c routing.yaml    # Routing tests
npx promptfoo@latest eval -c quality.yaml    # Quality tests
npx promptfoo@latest eval -c security.yaml   # Security tests
```

Requires `claude` CLI on PATH with active session (provider calls `claude -p`).

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

## Adding Test Cases

Append to eval datasets:
- `eval/datasets/routing-tests.yaml` — Skill routing accuracy
- `eval/datasets/quality-tests.yaml` — Output quality checks
- `eval/datasets/security-tests.yaml` — Adversarial prompt resistance

Rebuild routing prompt after adding skills:
```bash
python3 eval/scripts/build-routing-prompt.py
```

## Conventions

- SKILL.md frontmatter requires `name` and `description` fields
- Use sentence case for headings
- MIT license for all contributions
- Skills follow Agent Skills Specification (https://agentskills.io)
