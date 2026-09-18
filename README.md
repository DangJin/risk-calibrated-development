# Risk-Calibrated Development

An agent skill that scales software-development process and verification to the risk of a change.

It starts with the least costly workflow and upgrades only when evidence shows greater impact, recovery difficulty, or uncertainty. The skill defines three levels:

- **Fast** for clear, local, reversible changes.
- **Standard** for business behavior, shared code, dependencies, configuration, or uncertain defects.
- **Rigorous** for migrations, security, privacy, billing, public contracts, infrastructure, destructive work, or broad impact.

## Repository structure

```text
skills/
└── risk-calibrated-development/
    ├── SKILL.md
    └── agents/
        └── openai.yaml
```

## Install

Copy `skills/risk-calibrated-development` into the skills directory used by your agent environment. For example, with Codex:

```bash
mkdir -p ~/.codex/skills
cp -R skills/risk-calibrated-development ~/.codex/skills/
```

Restart the agent environment if it does not automatically discover newly installed skills.

## Use

Invoke the skill explicitly when you want the development workflow calibrated to the change risk:

```text
Use $risk-calibrated-development to implement this change with proportionate process and verification.
```

The skill also allows implicit invocation in compatible agent environments.

## License

No license has been granted yet. All rights are reserved unless a license file is added.
