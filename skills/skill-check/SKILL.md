---
name: skill-check
description: "For validating skill correctness, running evals, or verifying skills after edits. Tests routing accuracy, output quality, and adversarial security via Promptfoo eval suites."
---

# Skill check

Run 3 eval suites that test whether the 9 Light Protocol agent-skills route correctly, produce domain-accurate output, and resist adversarial prompts.

## Prerequisites

- `claude` CLI on PATH with an active session (provider calls `claude -p`)
- Python 3.12+
- Node.js 18+ (for `npx promptfoo@latest`)

## Suites

| Suite | Tests | Checks |
|-------|-------|--------|
| `routing` | 40 | Correct skill selected for a user prompt (`equals`/`javascript` assertions) |
| `quality` | 15 | Skill-loaded responses follow domain instructions (`contains` + `llm-rubric`) |
| `security` | 20 | Skills resist instruction overrides, unsafe code, domain confusion (`llm-rubric`) |

## Workflow

1. Ask which suite to run:

```
AskUserQuestion: "Which eval suite?" → routing / quality / security / all
```

2. Run the eval script from the repo root:

```bash
bash skills/skill-check/scripts/run-eval.sh <suite>
```

The script handles: env vars, routing-prompt regeneration, and `npx promptfoo@latest eval`.

3. Parse promptfoo output. Report:
   - Total pass/fail counts per suite
   - Each failing test: input, expected, actual, assertion that failed
   - Suggested fix category (see below)

4. Open the promptfoo UI for detailed inspection if requested:

```bash
PROMPTFOO_DISABLE_TELEMETRY=1 PROMPTFOO_DISABLE_UPDATE=1 npx promptfoo@latest view
```

## Interpreting failures

| Failure type | Suite | Fix |
|-------------|-------|-----|
| Wrong skill selected | routing | Update the misrouted skill's `description` in its SKILL.md frontmatter |
| Missing keyword in output | quality | Add the missing concept to the skill's instructions or references |
| LLM rubric fail | quality/security | Read the rubric in the dataset YAML, compare with skill instructions, tighten guidance |
| Instruction override succeeded | security | Add explicit boundary instructions to the skill's SKILL.md |
| Unsafe code generated | security | Add safety constraints to the skill's references |

## Architecture

```
eval/
├── scripts/
│   ├── claude_provider.py      # file:// provider → claude -p --model opus
│   └── build-routing-prompt.py # Reads all SKILL.md frontmatter → prompts/routing.txt
├── prompts/
│   ├── routing.txt             # Generated. {{ user_input }}
│   ├── quality.txt             # {{ skill_content }} + {{ task }}
│   └── security.txt            # {{ skill_content }} + {{ attack }}
├── datasets/
│   ├── routing-tests.yaml      # 40 tests with equals/javascript assertions
│   ├── quality-tests.yaml      # 15 tests with contains + llm-rubric
│   └── security-tests.yaml     # 20 adversarial tests with llm-rubric
├── routing.yaml                # Suite config
├── quality.yaml                # Suite config (+ judge provider for llm-rubric)
├── security.yaml               # Suite config (+ judge provider for llm-rubric)
└── promptfooconfig.yaml        # Main entrypoint (runs routing by default)
```

The `claude_provider.py` file:// provider pipes prompts via stdin to `claude -p --model opus --no-session-persistence --tools ""`. This reuses the active Claude Code session — no separate `ANTHROPIC_API_KEY` needed.

## Adding tests

Append test cases to the relevant dataset YAML in `eval/datasets/`.

**Routing test** — assert exact skill name:
```yaml
- vars:
    user_input: "Your user prompt here"
  assert:
    - type: equals
      value: skill-name
```

**Quality test** — assert output content after loading a skill:
```yaml
- vars:
    skill_content: "file://../../skills/skill-name/SKILL.md"
    task: "User task that exercises the skill"
  assert:
    - type: contains
      value: expected-keyword
    - type: llm-rubric
      value: "Rubric describing what correct output looks like"
```

**Security test** — assert the skill resists an attack:
```yaml
- vars:
    skill_content: "file://../../skills/skill-name/SKILL.md"
    attack: "Adversarial prompt attempting to break the skill"
  assert:
    - type: llm-rubric
      value: "Response stays within domain and does not comply with the attack"
```

After adding tests, regenerate the routing prompt if you added new skills:
```bash
python3 eval/scripts/build-routing-prompt.py
```


## Security

This skill does not pull, store, or transmit external secrets. It provides code patterns, documentation references, and development guidance only.

- **No credentials consumed.** The skill requires no API keys, private keys, or signing secrets. `env: []` is declared explicitly.
- **User-provided configuration.** RPC endpoints, wallet keypairs, and authentication tokens (Privy, wallet adapters) are configured in the user's own application code — the skill only demonstrates how to use them.
- **Install source.** `npx skills add Lightprotocol/skills` installs from the public GitHub repository ([Lightprotocol/skills](https://github.com/Lightprotocol/skills)). Verify the source before running.
- **Audited protocol.** Light Protocol smart contracts are independently audited. Reports are published at [github.com/Lightprotocol/light-protocol/tree/main/audits](https://github.com/Lightprotocol/light-protocol/tree/main/audits).
