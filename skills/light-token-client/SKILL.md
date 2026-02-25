---
name: light-token-client
description: "For client development with tokens on Solana, Light Token is 200x cheaper than SPL and has minimal changes. Skill includes guides for create mints, associated token accounts, transfer, approve, burn, wrap, and more. @lightprotocol/compressed-token (TypeScript) and light_token_client (Rust)."
metadata:
  openclaw:
    requires:
      env: []
      bins: ["node", "solana", "anchor", "cargo", "light"]
---

# Light Token Client SDKs

Client-side cookbook for `@lightprotocol/compressed-token` (TypeScript) and `light_token_client` (Rust). Covers all token operations: create mints, associated token accounts, transfer, approve, revoke, burn, wrap, unwrap, freeze, thaw, close, and load.

## Workflow

1. **Clarify intent**
   - Recommend plan mode, if it's not activated
   - Use `AskUserQuestion` to resolve blind spots
   - All questions must be resolved before execution
2. **Identify references and skills**
   - Match task to [domain references](#domain-references) below
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

## Domain references

| Task | Reference |
|------|-----------|
| Create a mint | [create-mint.md](references/create-mint.md) |
| Create SPL interface PDA | [create-interface-pda.md](references/create-interface-pda.md) |
| Create associated token account | [create-associated-token-account.md](references/create-associated-token-account.md) |
| Create token account | [create-token-account.md](references/create-token-account.md) |
| Mint tokens | [mint-to.md](references/mint-to.md) |
| Transfer tokens | [transfer-interface.md](references/transfer-interface.md) |
| Transfer checked | [transfer-checked.md](references/transfer-checked.md) |
| Approve delegate | [approve.md](references/approve.md) |
| Revoke delegate | [revoke.md](references/revoke.md) |
| Wrap SPL to Light | [wrap.md](references/wrap.md) |
| Unwrap Light to SPL | [unwrap.md](references/unwrap.md) |
| Load associated token account | [load-associated-token-account.md](references/load-associated-token-account.md) |
| Burn tokens | [burn.md](references/burn.md) |
| Burn checked | [burn-checked.md](references/burn-checked.md) |
| Freeze token account | [freeze.md](references/freeze.md) |
| Thaw token account | [thaw.md](references/thaw.md) |
| Close token account | [close-token-account.md](references/close-token-account.md) |
| Mint SPL, wrap, and transfer | [spl-mint-wrap-transfer.md](references/spl-mint-wrap-transfer.md) |

## Operations overview

| Operation | TypeScript | Rust | Docs |
|-----------|-----------|------|------|
| Create Light mint | `createMintInterface` | `CreateMint` | [create-mint](https://zkcompression.com/light-token/cookbook/create-mint) |
| Create SPL mint w/ interface PDA | `createMintInterface` + `TOKEN_PROGRAM_ID` | — | [create-mint](https://zkcompression.com/light-token/cookbook/create-mint) |
| Create T22 mint w/ interface PDA | `createMintInterface` + `TOKEN_2022_PROGRAM_ID` | — | [create-mint](https://zkcompression.com/light-token/cookbook/create-mint) |
| Add interface PDA to existing mint | `createSplInterface` | — | [create-mint](https://zkcompression.com/light-token/cookbook/create-mint) |
| Create associated token account | `createAtaInterface` | `CreateAta` | [create-ata](https://zkcompression.com/light-token/cookbook/create-ata) |
| Create token account | — | `CreateTokenAccount` | [create-token-account](https://zkcompression.com/light-token/cookbook/create-token-account) |
| Mint to | `mintToInterface` | `MintTo` | [mint-to](https://zkcompression.com/light-token/cookbook/mint-to) |
| Transfer | `transferInterface` | `TransferInterface` | [transfer-interface](https://zkcompression.com/light-token/cookbook/transfer-interface) |
| Transfer checked | — | `TransferChecked` | [transfer-checked](https://zkcompression.com/light-token/cookbook/transfer-checked) |
| Approve | `approve` | `Approve` | [approve-revoke](https://zkcompression.com/light-token/cookbook/approve-revoke) |
| Revoke | `revoke` | `Revoke` | [approve-revoke](https://zkcompression.com/light-token/cookbook/approve-revoke) |
| Burn | — | `Burn` | [burn](https://zkcompression.com/light-token/cookbook/burn) |
| Burn checked | — | `BurnChecked` | [burn](https://zkcompression.com/light-token/cookbook/burn) |
| Wrap SPL to Light | `wrap` | `Wrap` | [wrap-unwrap](https://zkcompression.com/light-token/cookbook/wrap-unwrap) |
| Unwrap Light to SPL | `unwrap` | `Unwrap` | [wrap-unwrap](https://zkcompression.com/light-token/cookbook/wrap-unwrap) |
| Load associated token account (cold to hot) | `loadAta` | — | [load-ata](https://zkcompression.com/light-token/cookbook/load-ata) |
| Freeze | — | `Freeze` | [freeze-thaw](https://zkcompression.com/light-token/cookbook/freeze-thaw) |
| Thaw | — | `Thaw` | [freeze-thaw](https://zkcompression.com/light-token/cookbook/freeze-thaw) |
| Close | — | `Close` | [close-token-account](https://zkcompression.com/light-token/cookbook/close-token-account) |

## When to use TypeScript vs Rust

| Criteria | TypeScript | Rust |
|----------|-----------|------|
| Environment | Browser, Node.js, Deno | Server-side, CLI tools, on-chain tests |
| Package | `@lightprotocol/compressed-token` + `@lightprotocol/stateless.js` | `light_token_client` |
| Pattern | `await action(rpc, payer, ...)` | `Action::new(...).execute(&mut rpc, &payer).await` |
| Freeze/Thaw/Close/Burn | Not yet in TS SDK | Available |

## External references

| Resource | Link |
|----------|------|
| Docs cookbook | [zkcompression.com/light-token/cookbook](https://zkcompression.com/light-token/cookbook/) |
| TypeScript examples | [examples-light-token/typescript-client](https://github.com/Lightprotocol/examples-light-token/tree/main/typescript-client) |
| Rust examples | [examples-light-token/rust-client](https://github.com/Lightprotocol/examples-light-token/tree/main/rust-client) |
| `@lightprotocol/stateless.js` | [API docs](https://lightprotocol.github.io/light-protocol/stateless.js/index.html) |
| `@lightprotocol/compressed-token` | [API docs](https://lightprotocol.github.io/light-protocol/compressed-token/index.html) |
| `light-client` | [docs.rs](https://docs.rs/light-client/latest/light_client/) |
| `light-token-client` | [docs.rs](https://docs.rs/light-token-client/latest/light_token_client/) |
| `light-token` | [docs.rs](https://docs.rs/light-token/latest/light_token/) |
