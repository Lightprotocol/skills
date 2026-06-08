# Solana Agent Skills for rent-free development: compressed tokens and compressed PDAs.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-Compatible-green.svg)](https://agentskills.io)

### Capabilities
ZK Compression lets you build scalable Solana applications with rent-free compressed token accounts and compressed PDAs.

| Creation cost          | Compressed          | Standard Solana |
| ---------------------- | ------------------: | --------------: |
| **Token Account**      | **\~5,000 lamports** | \~2,000,000 lamports |
| **PDA (128-byte)**     | **\~5,000 lamports** | \~1,100,000 lamports |

* Compressed token accounts are always compressed and rent-free. Any SPL or Token-2022 token can be compressed and decompressed at will. The SPL mint and interface PDA still pay rent; each holder's compressed token account does not.
* Compressed PDAs are derived like regular PDAs, but the program invokes the Light System Program (not the System Program) with a validity proof. Use them for per-user state, DePIN registrations, nullifiers, and infrequently accessed accounts.

### Skills by Use Case

```bash
npx skills add Lightprotocol/skills
```

> Find dedicated [prompts for agents here](prompts).

| Use case                                                                                                                                 | Skill                                                                                             |
| ---------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| For compressed token operations on Solana ~400x cheaper than SPL: create mints, mint, transfer, approve, burn, compress/decompress, merge, Token-2022, and token distribution                | [compressed-token](https://github.com/Lightprotocol/skills/tree/main/skills/compressed-token)     |
| For program development on Solana with infrequently accessed state, such as per-user state, DePIN registrations, nullifiers, or custom compressed accounts                                   | [compressed-pda](https://github.com/Lightprotocol/skills/tree/main/skills/compressed-pda)         |
| For custom ZK Solana programs and privacy-preserving applications to prevent double spending                                             | [zk](https://github.com/Lightprotocol/skills/tree/main/skills/zk)                                 |
| For testing with Light Protocol programs and clients on localnet, devnet, and mainnet validation                                         | [testing](https://github.com/Lightprotocol/skills/tree/main/skills/testing)                       |
| For questions about compressed accounts, Light SDK, Solana development, Claude Code features, or agent skills                            | [ask-mcp](https://github.com/Lightprotocol/skills/tree/main/skills/ask-mcp)                       |

> For additional documentation, see: [zkcompression.com](https://www.zkcompression.com)
> For examples, see: [Lightprotocol/examples](https://github.com/Lightprotocol/examples)

### Recommended Workflow

1. **Clarify intent**
   * Recommend plan mode, if it's not activated
   * Use `AskUserQuestion` to resolve blind spots
   * All questions must be resolved before execution
2. **Identify references and skills**
   * Match task to available [skills](#skills-by-use-case) below
   * Locate relevant [documentation and examples](#documentation-and-examples)
3. **Write plan file** (YAML task format)
   * Use `AskUserQuestion` for anything unclear — never guess or assume
   * Identify blockers: permissions, dependencies, unknowns
   * Plan must be complete before execution begins
4. **Execute**
   * Use `Task` tool with subagents for parallel research
   * Subagents load skills via `Skill` tool
   * Track progress with `TodoWrite`
5. **When stuck**: spawn subagent with `Read`, `Glob`, `Grep`, DeepWiki MCP access and load `skills/ask-mcp`

## Installation 

These skills work with any AI agent. Pick your skills to install:

```
npx skills add Lightprotocol/skills
```

### Claude Code

Add the marketplace and install:

```
# install solana-rent-free-dev
/plugin marketplace add Lightprotocol/skills
```

All skills are included. Use them by name (`/compressed-token`, `/compressed-pda`, `/zk`, `/testing`, `/ask-mcp`) or let Claude invoke them based on task context.

### OpenClaw

Install as a plugin (all 5 skills):

```bash
openclaw plugins install ./path/to/skills
```

Or install individual skills from [ClawHub](https://clawhub.ai/tilo-14/solana-rent-free-dev):

```bash
clawhub install solana-rent-free-dev
```

The plugin manifest is defined in [`openclaw.plugin.json`](openclaw.plugin.json).

### Cursor

1. Open Settings (**Cmd+Shift+J** / **Ctrl+Shift+J**)
2. Navigate to **Rules & Commands** → **Project Rules** → **Add Rule** → **Remote Rule (GitHub)**
3. Enter: `https://github.com/Lightprotocol/skills.git`

Skills are auto-discovered based on context. Ask about compressed tokens, compressed PDAs, ZK programs, or testing and the agent uses the relevant skill automatically.

## License

[MIT](LICENSE)

## Acknowledgments

Built on [Anthropic's Skills](https://github.com/anthropics/skills) and the [Agent Skills Specification](https://agentskills.io).

***

> For additional documentation, see: [https://www.zkcompression.com](https://www.zkcompression.com)
> For examples, see: [https://github.com/Lightprotocol/examples](https://github.com/Lightprotocol/examples)
