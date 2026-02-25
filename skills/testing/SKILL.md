---
name: testing
description: "For testing with Light Protocol programs and clients on localnet, devnet, and mainnet validation."
metadata:
  openclaw:
    requires:
      env: []
      bins: ["node", "solana", "anchor", "cargo", "light"]
license: MIT
author: Light Protocol
version: 1.0.0
---

# Light Protocol testing

## Workflow

1. **Clarify intent**
   - Recommend plan mode, if it's not activated
   - Use `AskUserQuestion` to resolve blind spots
   - All questions must be resolved before execution
2. **Identify references and skills**
   - Match task to [test references](#routing) below
   - Locate relevant documentation and examples
3. **Write plan file** (YAML task format)
   - Use `AskUserQuestion` for anything unclear — never guess or assume
   - Identify blockers: permissions, dependencies, unknowns
   - Plan must be complete before execution begins
4. **Execute**
   - Use `Task` tool with subagents for parallel research
   - Subagents load skills via `Skill` tool
   - Track progress with `TodoWrite`
5. **When stuck**: spawn subagent with `Read`, `Glob`, `Grep`, DeepWiki MCP access and load `skills/ask-mcp`

## Routing

| Task | Reference |
|------|-----------|
| Start local validator | [references/local.md](references/local.md) |
| Test on devnet | [references/devnet.md](references/devnet.md) |
| Test Pinocchio programs | `cargo test-sbf -p <program-name>` (no Anchor required) |

## Program addresses

These addresses are identical on devnet and mainnet.

| Program | Address |
|---------|---------|
| Light System | `SySTEM1eSU2p4BGQfQpimFEWWSC1XDFeun3Nqzz3rT7` |
| Compressed Token | `cTokenmWW8bLPjZEBAUgYy3zKxQZW6VKi7bqNFEVv3m` |
| Account Compression | `compr6CUsB5m2jS4Y3831ztGSTnDpnKJTKS95d64XVq` |
| Light Registry | `Lighton6oQpVkeewmo2mcPTQQp7kYHr4fWpAgJyEmDX` |

## Pre-initialized accounts

See [references/accounts.md](references/accounts.md) for state trees, address trees, and protocol PDAs.

See [references/addresses.md](references/addresses.md) for devnet-specific addresses and lookup tables.

## SDK references

| Package | Link |
|---------|------|
| `light-program-test` | [docs.rs](https://docs.rs/crate/light-program-test/latest) |
| `@lightprotocol/stateless.js` | [API docs](https://lightprotocol.github.io/light-protocol/stateless.js/index.html) |
| `light-client` | [docs.rs](https://docs.rs/light-client/latest/light_client/) |
