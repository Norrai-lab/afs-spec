[English](./README.md) | [中文](./README.zh.md)

# AFS — Agent-Friendly Standard

> 不是让 AI 学会用人类的软件，而是让软件成为 AI 的好工具。

**AFS（Agent-Friendly Standard）** 是一份开放规范，定义软件应当如何从设计层面对 AI Agent 友好——让 Agent 能够安全、高效、可靠地发现、理解和调用软件能力。

---

## 为什么需要 AFS？

当前的 AI Agent 被迫通过截屏、模拟点击和脆弱的浏览器自动化来与人类软件交互。与此同时，每个 SaaS 产品都内置了自己的 AI 助手，导致上下文割裂、重复付费和厂商锁定。

AFS 颠覆了这一模式：不再是"软件里有个 AI"，而是 **"AI 手里有一堆软件"**。AI 是调度中心，软件回归工具的本质。

### AFS 解决的问题

- **屏幕级自动化既贵又不可靠** — AI 浪费大量 token 处理截屏和模拟点击。
- **内置 AI 助手各自为政** — 十个应用十个 AI，无法共享上下文。
- **Agent 框架缺少专用工具** — OpenClaw 等平台因为只能使用人类界面和系统级权限，导致 token 消耗巨大、安全隐患严重。

### AFS 提供什么

- **skill.md** — 标准化、机器可读的能力说明书，支持渐进式披露（按需加载，用多少读多少）。
- **四层架构** — 接口层、文档层、效率层、安全层，可逐层渐进采用。
- **兼容 MCP** — 每个 AFS 工具同时也是合法的 MCP server，确保生态兼容。
- **Agent 无关** — 适用于 OpenClaw、Claude Code 或任何能读取 skill.md 并调用 API 的 AI Agent。

---

## 仓库结构

```
afs-spec/
├── README.md                          ← 英文 README
├── README.zh.md                       ← 中文 README（你在这里）
├── LICENSE                            ← 双协议说明
├── LICENSE-CC-BY-4.0                  ← CC BY 4.0（文档）
├── LICENSE-MIT                        ← MIT（代码）
├── whitepaper/
│   └── afs-whitepaper-v0.1.md         ← 愿景、动机与竞争分析
├── spec/
│   └── overview.md                    ← 技术规范（四层架构）
└── examples/
    └── afs-email/
        └── skill.md                   ← 示例：AFS Email skill
```

| 目录 | 用途 |
|------|------|
| `whitepaper/` | 阐述 AFS 的动机、核心原则和高层架构的叙述性文档。 |
| `spec/` | 规范性技术文档。定义 AFS 四层架构及其规则。 |
| `examples/` | 具体的、带注释的 AFS skill 定义示例。 |

---

## 快速开始

1. **阅读白皮书** — [`whitepaper/afs-whitepaper-v0.1.md`](whitepaper/afs-whitepaper-v0.1.md) 了解完整愿景和动机。
2. **阅读规范** — [`spec/overview.md`](spec/overview.md) 了解技术规范。
3. **查看示例** — [`examples/afs-email/skill.md`](examples/afs-email/skill.md) 查看一个完整的 skill 定义示例。

---

## 参与贡献

AFS 是一个开放项目，欢迎各种形式的贡献：

- **反馈** — 提交 Issue 来建议修改或指出模糊之处。
- **提案** — 针对 `spec/` 或 `whitepaper/` 提交 Pull Request。
- **示例** — 在 `examples/` 下新建目录，为你的场景编写 `skill.md`。

---

## 路线图

| 里程碑 | 状态 |
|--------|------|
| v0.1 — 白皮书 + 仓库脚手架 | ✅ 完成 |
| v0.2 — 接口层与文档层的规范性定义 | 🟡 进行中 |
| v0.3 — 效率层与安全层 + skill 定义的 JSON Schema | ⬜ 计划中 |
| v1.0 — 稳定规范、参考验证器和官方示例 | ⬜ 计划中 |

---

*本项目以文档为先，当前阶段不包含构建工具或代码。*

*© Norrai-lab 贡献者。文档采用 [CC BY 4.0](LICENSE-CC-BY-4.0) 协议，代码采用 [MIT](LICENSE-MIT) 协议。*
