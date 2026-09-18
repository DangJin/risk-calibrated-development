<div align="center">
  <h1>Risk-Calibrated Development</h1>
  <p><strong>根据变更的实际风险，匹配恰当的软件开发流程与验证强度。</strong></p>
  <p><a href="README.md">English</a> | <a href="README.zh-CN.md">简体中文</a></p>
  <p>
    <img alt="Agent Skill" src="https://img.shields.io/badge/Agent-Skill-0969DA">
    <img alt="Risk-Calibrated Workflow" src="https://img.shields.io/badge/Workflow-Risk--Calibrated-1F883D">
    <img alt="Codex Compatible" src="https://img.shields.io/badge/Codex-Compatible-6F42C1">
    <img alt="Fast、Standard 和 Rigorous 等级" src="https://img.shields.io/badge/Levels-Fast%20%7C%20Standard%20%7C%20Rigorous-D97706">
  </p>
</div>

这个 Agent Skill 从成本最低的流程开始，仅在证据表明影响范围、恢复难度或不确定性更高时升级流程。它让日常改动保持高效，同时为高风险工作保留必要的安全保障。

## 背景

不同的软件变更不应该采用完全相同的流程。调整一处文案与迁移认证系统具有不同的失败模式、影响范围和回滚成本，但 Coding Agent 往往会对两者套用同一套固定工作流。

这会导致两类常见问题：小改动承担了不必要的规划与验证成本，而重要变更又缺少足够的设计确认、回滚准备和验证证据。Risk-Calibrated Development 是一个流程路由器，它根据变更本身调整工作流，而不是把所有任务视为相同风险。

## 解决的问题

- **一刀切的工作流：** 避免每项任务都承担相同的流程仪式和测试负担。
- **流程膨胀：** 当头脑风暴、规划、Worktree、完整测试或评审不能降低具体风险时，不盲目叠加这些流程。
- **保障不足：** 识别数据迁移、认证、隐私、计费、公共契约和破坏性操作等硬性风险信号。
- **验证失焦：** 要求每项检查都对应一个明确的失败风险，避免重复收集无关证据。
- **范围与授权漂移：** 将代码变更、本地服务、Git 交付和部署保持为独立的授权边界。

## 工作原理

这个 Skill 通过四个因素进行定性风险路由：

```text
所需保障强度 = 失败概率 × 影响程度 × 恢复难度 × 不确定性
```

| 因素 | 需要回答的问题 |
| --- | --- |
| 失败概率 | 变更出现错误行为的可能性有多大？ |
| 影响程度 | 哪些用户、系统、契约或数据可能受到影响？ |
| 恢复难度 | 变更能否轻松回滚或修复？ |
| 不确定性 | 对问题原因、预期行为和受影响边界的理解是否充分？ |

面对每项任务时，这个 Skill 会：

1. 从 **Fast** 开始。
2. 检查是否存在需要升级到 **Standard** 或 **Rigorous** 的可观察信号。
3. 选择能够将残余风险控制在可接受范围内的最小工作流。
4. 创建新实现前，优先复用平台和项目已有能力。
5. 只执行覆盖已识别风险所需的验证。

## 风险等级

| 等级 | 适用场景 | 执行方式 |
| --- | --- | --- |
| **Fast** | 变更明确、局部、可回滚且影响较低 | 直接实现，并执行范围最小且相关的检查 |
| **Standard** | 涉及业务行为、共享代码、依赖、配置，或问题原因尚不确定 | 确认受影响的契约，并执行针对性测试和静态检查 |
| **Rigorous** | 涉及数据、安全、隐私、计费、公共契约、基础设施、破坏性操作或广泛影响 | 变更前确认设计与风险控制措施，随后执行全面且相关的验证 |

完整决策规则请查看 [SKILL.md](skills/risk-calibrated-development/SKILL.md)。

## 使用案例

### 1. 局部 UI 修正 — Fast

```text
使用 $risk-calibrated-development，按照现有按钮模式对齐这个图标。
```

预期行为：检查现有组件，完成最小范围的局部修改，审阅差异，并确认受影响的 UI 或执行窄范围检查；不额外引入完整测试套件或设计阶段。

### 2. 共享表单或 API 行为 — Standard

```text
使用 $risk-calibrated-development，为共享注册表单和 API 增加这条验证规则。
```

预期行为：明确受影响的验证契约，检查所有相关调用方，保持客户端与服务端行为一致，并执行针对性测试和受影响的静态检查。

### 3. 原因不明确的缺陷 — Standard

```text
使用 $risk-calibrated-development，诊断并修复这个间歇性的状态同步问题。
```

预期行为：修改行为前先确定根因，识别受影响的状态契约，补充针对性的回归证据，并验证受影响路径。

### 4. 数据迁移、认证或计费变更 — Rigorous

```text
使用 $risk-calibrated-development，迁移这张用户表，同时保护认证与计费数据。
```

预期行为：执行变更前确认设计，定义回滚和迁移控制措施，保护敏感数据与外部契约，并执行全面且相关的验证；部署仍然作为独立授权步骤处理。

## 安装

克隆仓库，并将 Skill 复制到 Agent 环境中。以 Codex 为例：

```bash
git clone https://github.com/DangJin/risk-calibrated-development.git
mkdir -p ~/.codex/skills
cp -R risk-calibrated-development/skills/risk-calibrated-development ~/.codex/skills/
```

如果 Agent 环境不能自动发现新安装的 Skill，请重新启动该环境。

## 使用

在提示词中显式调用：

```text
使用 $risk-calibrated-development，以与风险相匹配的流程和验证方式实现这项变更。
```

兼容的 Agent 环境也可以自动调用该 Skill。仓库包含的 OpenAI Agent 配置已允许隐式调用。

## 设计原则

- 从 Fast 开始，仅在证据充分时升级流程。
- 创建新实现前，优先复用平台和项目已有能力。
- 根据失败概率、影响程度、恢复难度和不确定性匹配验证成本。
- 将代码变更、本地服务、Git 交付和部署视为独立的授权边界。
- 当更小范围的保障措施已经足够时，避免叠加重量级流程。

## 仓库结构

```text
skills/
└── risk-calibrated-development/
    ├── SKILL.md
    └── agents/
        └── openai.yaml
```

## 支持与贡献

请通过 [GitHub Issues](https://github.com/DangJin/risk-calibrated-development/issues) 报告问题或提出改进建议。Pull Request 应保持流程适度、结果可复现，并与现有 Skill 契约兼容。

维护者：[@DangJin](https://github.com/DangJin)。

## 许可证

本项目目前未授予任何许可证。在添加许可证文件前，保留所有权利。
