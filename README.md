<div align="center">
  <h1>Risk-Calibrated Development</h1>
  <p><strong>Scale software-development process and verification to the actual risk of a change.</strong></p>
  <p><a href="README.md">English</a> | <a href="README.zh-CN.md">简体中文</a></p>
  <p>
    <img alt="Agent Skill" src="https://img.shields.io/badge/Agent-Skill-0969DA">
    <img alt="Risk-Calibrated Workflow" src="https://img.shields.io/badge/Workflow-Risk--Calibrated-1F883D">
    <img alt="Codex Compatible" src="https://img.shields.io/badge/Codex-Compatible-6F42C1">
    <img alt="Fast, Standard, and Rigorous levels" src="https://img.shields.io/badge/Levels-Fast%20%7C%20Standard%20%7C%20Rigorous-D97706">
  </p>
</div>

This agent skill starts with the least costly workflow and upgrades only when evidence shows greater impact, recovery difficulty, or uncertainty. It keeps routine changes fast without relaxing the safeguards needed for high-risk work.

## Risk levels

| Level | Use when | Process |
| --- | --- | --- |
| **Fast** | The change is clear, local, reversible, and low impact | Implement directly and run the narrowest relevant check |
| **Standard** | The change affects business behavior, shared code, dependencies, configuration, or has an uncertain cause | Confirm the affected contract and run targeted tests and static checks |
| **Rigorous** | The change involves data, security, privacy, billing, public contracts, infrastructure, destructive work, or broad impact | Confirm design and risk controls before mutation, then verify comprehensively |

The complete decision rules are defined in [SKILL.md](skills/risk-calibrated-development/SKILL.md).

## Installation

Clone the repository and copy the skill into your agent environment. For Codex:

```bash
git clone https://github.com/DangJin/risk-calibrated-development.git
mkdir -p ~/.codex/skills
cp -R risk-calibrated-development/skills/risk-calibrated-development ~/.codex/skills/
```

Restart the agent environment if it does not automatically discover newly installed skills.

## Usage

Invoke the skill explicitly in your prompt:

```text
Use $risk-calibrated-development to implement this change with proportionate process and verification.
```

Compatible agent environments may also invoke it automatically. The bundled OpenAI agent configuration enables implicit invocation.

## Design principles

- Start with Fast and upgrade only when evidence justifies it.
- Reuse platform and project capabilities before creating new implementations.
- Match verification cost to failure likelihood, impact, recovery difficulty, and uncertainty.
- Treat code changes, local services, Git delivery, and deployment as separate authorization boundaries.
- Avoid stacking heavyweight process workflows when a narrower safeguard is sufficient.

## Repository structure

```text
skills/
└── risk-calibrated-development/
    ├── SKILL.md
    └── agents/
        └── openai.yaml
```

## Support and contributions

Use [GitHub Issues](https://github.com/DangJin/risk-calibrated-development/issues) to report problems or propose improvements. Pull requests should keep the workflow proportionate, deterministic, and compatible with the existing skill contract.

Maintained by [@DangJin](https://github.com/DangJin).

## License

No license has been granted. All rights are reserved unless a license file is added.
