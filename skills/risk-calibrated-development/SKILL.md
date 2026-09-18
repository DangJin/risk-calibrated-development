---
name: risk-calibrated-development
description: Use when implementing, modifying, or fixing software and the appropriate amount of design, testing, review, or delivery work must be chosen.
---

# Risk Calibrated Development

## Principle

Choose the lowest-cost workflow that leaves residual risk acceptable:

`assurance needed = failure likelihood × impact × recovery difficulty × uncertainty`

User-specified workflows and authorization boundaries take precedence. Domain and tool skills still apply.

## Classify Before Acting

Use the highest matching level. Start Fast; upgrade only on evidence. File count, effort, and extra caution are not upgrade reasons.

| Level | Observable conditions |
| --- | --- |
| Fast | All: local, reversible, clear, established pattern, and no persistent data, public contract, security, privacy, billing, or production risk. Examples: copy, spacing, styling, icons, and small existing-component adjustments. |
| Standard | Any: local business behavior, forms/state, one API, shared code, dependencies/config, uncertain bug cause, or multi-screen impact without a hard gate. |
| Rigorous | Any: schema/data migration, bulk mutation, auth, security, privacy, secrets, billing, public/external contract, production infrastructure, destructive work, broad impact, difficult rollback, or explicit full-process request. |

## Execute Proportionately

- **Fast:** Briefly state scope, inspect the target/pattern, make the smallest change, review the diff, and run the narrowest local check or UI confirmation. Add no design gate, new test, full suite, Docker, Git delivery, or deployment unless required or requested.
- **Standard:** Establish cause and contract, implement narrowly, and run targeted tests plus affected static checks. Ask only about material choices that cannot be inferred.
- **Rigorous:** Confirm design and risks before mutation. Define rollback/migration controls, test behavior when meaningful, run comprehensive relevant checks, and validate production changes.

## Acquire Capabilities in Order

Check platform/framework/library, project implementations, adapting existing capability, creating locally, then external dependencies. Stop at the first sound option; do not force reuse across wrong ownership or contracts.

## Keep Evidence and Delivery Scoped

Every validation must answer a concrete risk. Avoid duplicate evidence and unrelated suites. Code changes, local services/Docker, Git delivery, and deployment are separate boundaries. Execute requested boundaries and batch repeated builds or deployments at the end.

## Process Skills

Do not stack brainstorming, planning, TDD, worktree, review, or full-verification workflows merely because keywords match. Apply their safeguards only when this classification requires them or the user explicitly names them. Tool-mandated and domain-specific skills remain unaffected.

## Completion

Report the result, material verification evidence, remaining risk, and only the next action that actually requires the user.

## Common Rationalizations

| Rationalization | Correction |
| --- | --- |
| "The full suite is safer." | Unrelated checks add delay without evidence for the changed risk. |
| "Every bug needs the same TDD ceremony." | Match regression coverage to behavior and failure impact. |
| "Many files means Rigorous." | Classify by consequence, reversibility, and uncertainty. |
| "While here, refactor it." | Keep unrelated improvements outside the authorized scope. |
