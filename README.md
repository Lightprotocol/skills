# Solana Development Skills using Light Protocol

AI agent skills for rent-free Solana development: light PDA, token and mint accounts, and compressed PDA.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-Compatible-green.svg)](https://agentskills.io)

## Installation

These skills work with any AI agent. We recommend [Claude Code](https://claude.ai/code) with Opus models for best results.

### Claude Code

Add the marketplace:

```
/plugin marketplace add lightprotocol/ai-tools
```

Install skills:

```
/plugin install defi-program
/plugin install airdrop
/plugin install testing
```

### Cursor

1. Open Settings (**Cmd+Shift+J** / **Ctrl+Shift+J**)
2. Navigate to **Rules & Commands** → **Project Rules** → **Add Rule** → **Remote Rule (GitHub)**
3. Enter: `https://github.com/lightprotocol/ai-tools.git`

Skills are auto-discovered based on context. Ask about light-token, defi, payments, or program migration and the agent uses the relevant skill automatically.

### Any Agent

```
npx skills add lightprotocol/ai-tools
```

## Available skills

### DeFi

| Skill | Description |
| ----- | ----------- |
| [defi-program](skills/defi-program/) | Build rent-free DeFi programs (AMMs, vaults, lending) with Anchor or Pinocchio |
| [defi-router](skills/defi-router/) | Integrate rent-free markets into routers and aggregators |

### Tokens

| Skill | Description |
| ----- | ----------- |
| [airdrop](skills/airdrop/) | Distribute SPL tokens at 5000x lower cost for airdrops, DePINs, and token distribution |

### Payments

| Skill | Description |
| ----- | ----------- |
| [payments-and-wallets](skills/payments-and-wallets/) | Payment flows and wallet integrations with light-token |

### Data

| Skill | Description |
| ----- | ----------- |
| [data-streaming](skills/data-streaming/) | Stream account state via Laserstream gRPC with hot/cold lifecycle tracking |

### ZK Applications

| Skill | Description |
| ----- | ----------- |
| [zk-nullifier](skills/zk-nullifier/) | Privacy-preserving applications with ZK nullifiers to prevent double spending |

### Testing

| Skill | Description |
| ----- | ----------- |
| [testing](skills/testing/) | Test Light Protocol programs and clients on localnet, devnet, and mainnet |

### Research

| Skill | Description |
| ----- | ----------- |
| [ask-mcp](skills/ask-mcp/) | Query Light Protocol repository via DeepWiki MCP for errors and implementation questions |

## Resources

- [Light Protocol documentation](https://www.zkcompression.com/)
- [Light Protocol GitHub](https://github.com/lightprotocol/light-protocol)
- [Examples](https://github.com/Lightprotocol/examples-light-token)

## Contributing

1. Fork the repository
2. Copy an existing skill directory as a starting point: `cp -r skills/airdrop/ skills/your-skill-name/`
3. Write a `SKILL.md` with frontmatter (`name`, `description`) and instructions
4. Add your skill to `.claude-plugin/marketplace.json`
5. Submit a pull request

## License

[MIT](LICENSE)

## Acknowledgments

Built on [Anthropic's Skills](https://github.com/anthropics/skills) and the [Agent Skills Specification](https://agentskills.io).

---

<p align="center">
  Built by <a href="https://github.com/Lightprotocol">Light Protocol</a> for the Solana ecosystem
</p>
