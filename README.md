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

## Background

Software changes do not all deserve the same process. A copy adjustment and an authentication migration have different failure modes, impact, and rollback costs, yet coding agents often apply one fixed workflow to both.

That creates two common failures: small changes accumulate unnecessary planning and verification, while consequential changes proceed without enough design, rollback preparation, or evidence. Risk-Calibrated Development provides a process router that adjusts the workflow to the change instead of treating every task as equally risky.

## Problems it solves

- **One-size-fits-all workflows:** prevents every task from inheriting the same ceremony and test burden.
- **Process inflation:** avoids adding brainstorming, planning, worktrees, full test suites, or reviews when they do not reduce a concrete risk.
- **Insufficient assurance:** identifies hard gates such as data migration, authentication, privacy, billing, public contracts, and destructive operations.
- **Unfocused verification:** requires each check to answer a specific failure risk instead of collecting redundant evidence.
- **Scope and authorization drift:** keeps code changes, local services, Git delivery, and deployment as separate boundaries.

## How it works

The skill acts as a qualitative risk router. It evaluates four factors:

```text
assurance needed = failure likelihood × impact × recovery difficulty × uncertainty
```

| Factor | Question |
| --- | --- |
| Failure likelihood | How likely is the change to behave incorrectly? |
| Impact | What users, systems, contracts, or data could be affected? |
| Recovery difficulty | How easily can the change be rolled back or repaired? |
| Uncertainty | How well are the cause, behavior, and affected boundaries understood? |

For each task, the skill:

1. Starts at **Fast**.
2. Checks for observable signals that require **Standard** or **Rigorous** handling.
3. Chooses the smallest workflow that leaves acceptable residual risk.
4. Reuses platform and project capabilities before creating a new implementation.
5. Runs only the verification needed to cover the identified risks.

## Risk levels

| Level | Use when | Process |
| --- | --- | --- |
| **Fast** | The change is clear, local, reversible, and low impact | Implement directly and run the narrowest relevant check |
| **Standard** | The change affects business behavior, shared code, dependencies, configuration, or has an uncertain cause | Confirm the affected contract and run targeted tests and static checks |
| **Rigorous** | The change involves data, security, privacy, billing, public contracts, infrastructure, destructive work, or broad impact | Confirm design and risk controls before mutation, then verify comprehensively |

The complete decision rules are defined in [SKILL.md](skills/risk-calibrated-development/SKILL.md).

## Use cases

### 1. Local UI correction — Fast

```text
Use $risk-calibrated-development to align this icon with the existing button pattern.
```

Expected behavior: inspect the existing component, make the smallest local change, review the diff, and confirm the affected UI or narrow check. No broad test suite or design phase is added.

### 2. Shared form or API behavior — Standard

```text
Use $risk-calibrated-development to add this validation rule to the shared signup form and API.
```

Expected behavior: define the affected validation contract, inspect all relevant callers, keep client and server behavior consistent, and run targeted tests plus affected static checks.

### 3. Bug with an uncertain cause — Standard

```text
Use $risk-calibrated-development to diagnose and fix this intermittent state synchronization bug.
```

Expected behavior: establish the cause before changing behavior, identify the affected state contract, add focused regression evidence, and verify the impacted paths.

### 4. Migration, authentication, or billing change — Rigorous

```text
Use $risk-calibrated-development to migrate this user table while preserving authentication and billing data.
```

Expected behavior: confirm the design before mutation, define rollback and migration controls, protect sensitive data and external contracts, and run comprehensive relevant verification. Deployment remains a separate authorization step.

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
