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
| token-distribution | For airdrops, DePIN, or token distribution, 5000x cheaper than SPL with custom claim support. @lightprotocol/compressed-token (TypeScript). |
| ask-mcp | For questions about compressed accounts, Light SDK, Solana development, Claude Code features, or agent skills. AI-powered answers grounded in repository context via DeepWiki MCP. |
| data-streaming | For data pipelines, aggregators, or indexers, real-time account state streaming with hot/cold lifecycle tracking. Token accounts, mint accounts, and compressible PDAs via Laserstream gRPC. |
| light-sdk | For DeFi (AMMs, vaults, lending), infrastructure, or any Solana program, 98% cheaper with rent-free Light-PDAs, token accounts, and mints. Light SDK with Anchor or Pinocchio. State structs, account creation, CPI, router integration, and testing. |
| light-token-client | For Light Token operations, 200x cheaper than SPL — create mints, associated token accounts, transfer, approve, burn, wrap, and more. @lightprotocol/compressed-token (TypeScript) and light_token_client (Rust). |
| solana-compression | For per-user state, DePIN registrations, or custom compressed accounts, ~100x cheaper without rent-exemption. Light System Program CPI. Create, update, close, burn, and reinitialize compressed accounts. |
| payments-and-wallets | For payment flows and wallet integrations, 200x cheaper token accounts. Receive, send, balance, history, and client-side signing with Privy and Solana wallet adapters. Optional nullifier-based double-spend prevention. |
| testing | For localnet, devnet, and mainnet validation, end-to-end testing of Light Protocol programs and clients. Anchor test, cargo test, and light CLI. |
| zk-nullifier | For privacy-preserving applications and ZK Solana programs, rent-free nullifier PDAs for double-spend prevention. Proof verification, Merkle trees, and encrypted state. |
| skill-check | For validating skill correctness, running evals, or verifying skills after edits. Tests routing accuracy, output quality, and adversarial security via Promptfoo eval suites. |

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
