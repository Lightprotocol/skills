---
name: solana-compression
description: "For program development on Solana for per-user state, DePIN registrations, or custom compressed accounts ~160x cheaper and without rent-exemption. Create, update, close, burn, and reinitialize compressed accounts."
metadata:
  openclaw:
    requires:
      env: []
      bins: ["node", "solana", "anchor", "cargo", "light"]
allowed-tools: Bash(git:*), Bash(cargo:*), Bash(anchor:*), Bash(light:*), Read, Edit, Glob, Grep, Write, Task, WebFetch, WebSearch, mcp__deepwiki__ask_question, mcp__claude-code-docs__SearchClaudeCodeDocs
---

# Compressed PDA Programs

Build Solana programs with compressed accounts via manual CPI to the Light System Program. Compressed accounts cost ~100x less than regular accounts (no rent-exemption required).

## When to use compressed PDAs

- Per-user state (profiles, game state, credentials)
- DePIN device registrations
- Nullifier-based double-spend prevention
- Infrequently accessed accounts

## Choosing approach

| Criteria | Light-PDA (easy) | Compressed PDA (advanced) |
|----------|-----------------|--------------------------|
| When | Rent-free version of existing Anchor accounts | Custom compressed state with ZK proofs |
| Skill | `light-sdk` (Anchor macro pattern) | This skill (`solana-compression`) |
| Macro | `#[light_account(init)]` | `LightAccount::new_init()` manual CPI |
| Dependencies | `light-sdk`, `light-compressible` | `light-sdk`, `light-sdk-types` |

If you just want rent-free Anchor accounts, use the `light-sdk` skill instead. This skill is for programs that require manual CPI to the Light System Program (custom compressed state, ZK proofs, address derivation).

### Client-program interaction flow

```text
 ├─ Client
 │  ├─ Get ValidityProof from RPC.
 │  ├─ pack accounts with PackedAccounts into PackedAddressTreeInfo and PackedStateTreeInfo.
 │  ├─ pack CompressedAccountMeta.
 │  ├─ Build Instruction from PackedAccounts and CompressedAccountMetas.
 │  └─ Send transaction.
 │
 └─ Custom Program
    ├─ CpiAccounts parse accounts consistent with PackedAccounts.
    ├─ LightAccount instantiates from CompressedAccountMeta.
    │
    └─ Light System Program CPI
       ├─ Verify ValidityProof.
       ├─ Update State Merkle tree.
       ├─ Update Address Merkle tree.
       └─ Complete atomic state transition.
```

## Domain references

| Topic | Reference |
|-------|-----------|
| Program operations (create, update, close, burn, reinit) | [references/compressed-pdas.md](references/compressed-pdas.md) |
| Client SDK (TypeScript + Rust) | [references/client.md](references/client.md) |
| Nullifier PDAs (double-spend prevention) | [references/nullifier-pdas.md](references/nullifier-pdas.md) |
| Error codes (6000-16034) | [references/error-codes.md](references/error-codes.md) |

## Reference repos

```
/home/tilo/Workspace/program-examples/
├── create-and-update/     # Basic create + update pattern
├── close-account/         # Close, burn, reinit patterns
├── token-escrow/          # Token + compressed account patterns
├── airdrop-implementations/distributor/  # Merkle + compressed
└── zk/                    # ZK proof patterns

/home/tilo/Workspace/examples-zk-compression/
/home/tilo/Workspace/example-token-distribution/
/home/tilo/Workspace/example-nodejs-client/
```

## Workflow

1. **Clarify intent**
   - Recommend plan mode, if it's not activated
   - Use `AskUserQuestion` to resolve blind spots
   - All questions must be resolved before execution
2. **Identify references**
   - Match task to [domain references](#domain-references) and [reference repos](#reference-repos)
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

## Build and test

### Required commands

**Anchor programs:**
```bash
anchor build
anchor test
```

**Native programs:**
```bash
cargo build-sbf
cargo test-sbf
```

### Forbidden shortcuts

- Do NOT use `cargo build` (must use `cargo build-sbf`)
- Do NOT use `cargo test` (must use `cargo test-sbf`)
- Do NOT skip SBF compilation
- Tests MUST run against real BPF bytecode

### Failure recovery

On failure, spawn debugger agent with error context.

**Loop rules:**
1. Each debugger gets fresh context + previous debug reports
2. Each attempt tries something DIFFERENT
3. **NEVER GIVE UP** - keep spawning until fixed
4. Max 5 attempts per error

Do NOT proceed until all tests pass.

## SDK references

| Package | Link |
|---------|------|
| `light-sdk` | [docs.rs](https://docs.rs/light-sdk/latest/light_sdk/) |
| `light-client` | [docs.rs](https://docs.rs/light-client/latest/light_client/) |
| `@lightprotocol/stateless.js` | [API docs](https://lightprotocol.github.io/light-protocol/stateless.js/index.html) |
| `light-program-test` | [docs.rs](https://docs.rs/crate/light-program-test/latest) |

## DeepWiki fallback

If no matching pattern in reference repos:

```
mcp__deepwiki__ask_question("Lightprotocol/light-protocol", "How to {operation}?")
```
