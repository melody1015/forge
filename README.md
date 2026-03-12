# Forge 🔨

Automated repair-inspect loop with state persistence, dependency analysis, and safety guardrails.

A [ClawHub](https://clawhub.ai) skill for AI agents. Install with:

```bash
clawhub install forge
```

## What It Does

Forge orchestrates **repair-inspect loops** for code changes:

1. **Add repair tasks** with acceptance criteria and dependencies
2. **Run in parallel waves** based on dependency graph
3. **Independent inspection** after each repair (not just "looks fixed")
4. **Auto-loop on FAIL** (max 5 rounds, then escalate)
5. **Auto-commit on PASS** with protected file guardrails

## Quick Start

```bash
cd /path/to/project

# Initialize
python3 ~/clawd/skills/forge/scripts/forge.py init

# Add tasks
python3 ~/clawd/skills/forge/scripts/forge.py add "Fix null handling" --criteria "No crash on empty input" --priority P0
python3 ~/clawd/skills/forge/scripts/forge.py add "Clean deprecated code" --criteria "No import errors" --depends task-001

# See execution plan
python3 ~/clawd/skills/forge/scripts/forge.py plan

# Run (outputs spawn instructions for AI agents)
python3 ~/clawd/skills/forge/scripts/forge.py run
```

## Safety Features

- **Protected files** — List in `protected-files.txt`, cannot be modified
- **Pre-commit diff check** — Detects file deletions, protected modifications
- **Max rounds limit** — Auto-escalate after 5 failed repair attempts

## Architecture

```
State Machine: pending → repairing → inspecting → done
                                    ↑          │
                                    └── fail ──┘
```

## Full Documentation

See [SKILL.md](./SKILL.md) for complete CLI reference and integration guide.

## License

MIT
