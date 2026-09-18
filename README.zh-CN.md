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

## 风险等级

| 等级 | 适用场景 | 执行方式 |
| --- | --- | --- |
| **Fast** | 变更明确、局部、可回滚且影响较低 | 直接实现，并执行范围最小且相关的检查 |
| **Standard** | 涉及业务行为、共享代码、依赖、配置，或问题原因尚不确定 | 确认受影响的契约，并执行针对性测试和静态检查 |
| **Rigorous** | 涉及数据、安全、隐私、计费、公共契约、基础设施、破坏性操作或广泛影响 | 变更前确认设计与风险控制措施，随后执行全面且相关的验证 |

完整决策规则请查看 [SKILL.md](skills/risk-calibrated-development/SKILL.md)。

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
