<div align="center">
  <h1>Risk-Calibrated Development</h1>
  <p><strong>A development workflow router that matches engineering process and verification effort to the actual risk of a software change.</strong></p>
  <p><a href="README.md">English</a> | <a href="README.zh-CN.md">简体中文</a></p>
  <p>
    <img alt="Agent Skill" src="https://img.shields.io/badge/Agent-Skill-0969DA">
    <img alt="Risk-Calibrated Workflow" src="https://img.shields.io/badge/Workflow-Risk--Calibrated-1F883D">
    <img alt="Codex Compatible" src="https://img.shields.io/badge/Codex-Compatible-6F42C1">
    <img alt="Fast, Standard, and Rigorous levels" src="https://img.shields.io/badge/Levels-Fast%20%7C%20Standard%20%7C%20Rigorous-D97706">
  </p>
</div>

Risk-Calibrated Development helps coding agents use the right amount of engineering process—not the most process and not the least.

## Core proposition

> Use the lowest-cost workflow that leaves the residual risk acceptable.

```text
assurance needed
= failure likelihood
× impact
× recovery difficulty
× uncertainty
```

## Background

Coding agents often apply the same heavyweight workflow to every task.

A small spacing change may trigger brainstorming, design approval, test-driven development, full test suites, Docker rebuilds, code reviews, and deployment preparation. Meanwhile, a one-line permission or production configuration change may look simple but carry significant operational risk.

Risk-Calibrated Development addresses this mismatch. It classifies changes by consequence, reversibility, and uncertainty—not by code size, file count, or estimated effort.

## Problems it solves

- Simple UI changes are overdesigned and oververified.
- Multiple process skills activate together and duplicate work.
- File count or lines changed are mistaken for risk indicators.
- Every small change repeats builds, Docker work, commits, or deployment preparation.
- Existing framework and project capabilities are overlooked before new code is created.
- A genuinely risky one-line configuration change is underestimated.
- Agents run unrelated checks merely because they appear safer.

## Design goals

- Keep process cost proportional to actual risk.
- Start with a lightweight workflow and upgrade only on evidence.
- Give low-risk changes a fast, direct execution path.
- Preserve strong safeguards for data, security, and production changes.
- Make every verification step answer a concrete risk.
- Prefer framework, dependency, and project capabilities before new implementations.
- Avoid unrelated refactors, duplicate verification, and stacked process workflows.
- Preserve authorization boundaries between code changes, Git delivery, and production deployment.

## How it works

The skill acts as a qualitative risk router. It evaluates the four factors in the core proposition:

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

### Fast

Use for clear, local, easily reversible changes, such as:

- Copy, spacing, colors, or icons
- Local layout changes
- Small adjustments to an existing component

Default behavior:

- Implement directly.
- Inspect the target and existing pattern.
- Review the diff.
- Run the narrowest relevant static check or UI confirmation.
- Do not automatically add design approval, TDD, Docker, a full build, Git delivery, or deployment.

### Standard

Use for local business behavior or changes with moderate uncertainty, such as:

- Forms and state management
- A single API
- Shared components
- Dependency or configuration adjustments
- Bugs without a confirmed cause
- Interactions spanning multiple screens

Default behavior:

- Establish the cause and affected contract first.
- Reuse existing implementations where appropriate.
- Run targeted tests.
- Run lint or type checks for the affected scope.
- Ask only when a material product choice cannot be inferred.

### Rigorous

Use when the change has an explicit high-risk signal, such as:

- Schema or data migrations
- Bulk data mutations
- Authentication, permissions, or security
- Privacy, secrets, or billing
- Public APIs or external contracts
- Production infrastructure
- Broad impact or difficult rollback

Default behavior:

- Confirm the design and risks before mutation.
- Define migration, rollback, and stop conditions.
- Add reliable tests for testable behavior.
- Run comprehensive, relevant engineering verification.
- Validate production changes after deployment when deployment is authorized.

The complete decision rules are defined in [SKILL.md](skills/risk-calibrated-development/SKILL.md).

## Typical use cases

| Change | Classification | Key reason |
| --- | --- | --- |
| Change button spacing from `8px` to `12px` | Fast | Local, clear, and reversible |
| Restore pagination state after returning from article editing | Standard | Involves routing and page state |
| Update button copy across a dozen locale files | Fast | File count does not determine risk |
| Change the default role for new users to administrator | Rigorous | Permission and security risk |
| Bulk-publish historical drafts | Rigorous | Bulk mutation of production data |
| Change the default sort order of a public API | Rigorous | External contract and pagination stability |

Example prompts:

```text
Use $risk-calibrated-development to change this button spacing from 8px to 12px.
Use $risk-calibrated-development to preserve pagination after returning from article editing.
Use $risk-calibrated-development to change the default role assigned to new users.
```

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

## Capability reuse order

Before creating a new implementation, inspect capabilities in this order:

```text
Platform / framework / library
→ Existing project implementation
→ Adapt an existing capability
→ Create a local implementation
→ Introduce an external dependency
```

Stop when an option satisfies the requirement and belongs at the correct ownership boundary.

## Relationship to other skills

Risk-Calibrated Development is a process router, not a replacement for domain skills.

Image, document, Figma, browser-control, and framework-specific skills continue to operate normally. Process capabilities such as brainstorming, TDD, implementation planning, worktrees, code review, and full verification are selected according to the risk level. An explicitly requested user workflow always takes precedence.

## Delivery boundaries

The skill treats these operations as separate authorization boundaries:

- Modify code
- Update local services or Docker
- Commit, push, or create a pull request
- Deploy to production

Starting a code change does not automatically authorize a commit, push, or deployment. When the user explicitly requests complete delivery, repeated builds and deployments are batched at the end of the requested scope.

## Non-goals

This skill does not:

- Replace a project's own engineering standards
- Reduce required security or data safeguards
- Force every project to use the same test tools
- Generate a design document for every task
- Grant permission for Git, deployment, or production data operations
- Manage pure research, copywriting, or read-only analysis tasks

## Project positioning

> This is not a “skip the process” skill. It is a “use the right amount of process” skill.

The goal is not to make coding agents always choose the fastest path. It removes ineffective process while preserving engineering safeguards proportional to the actual risk.

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
