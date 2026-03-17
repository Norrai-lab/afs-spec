[English](./README.md) | [中文](./README.zh.md)

# AFS — Agent-Friendly Standard

> Don't teach AI to use human software — make software a good tool for AI.

**AFS (Agent-Friendly Standard)** is an open specification that defines how software should be designed from the ground up so that AI agents can discover, understand, and interact with it safely, efficiently, and reliably.

---

## Why AFS?

Modern AI agents are forced to interact with software built for humans — through screenshots, simulated clicks, and brittle browser automation. Meanwhile, every SaaS product ships its own siloed AI assistant, creating fragmented context, redundant billing, and vendor lock-in.

AFS flips the model: instead of "software with an AI inside," AFS enables **"AI with software at its fingertips."** AI is the orchestration hub; software returns to its essence as a tool.

### The problem AFS solves

- **Screen-level automation is expensive and unreliable** — AI wastes millions of tokens processing screenshots and simulating clicks.
- **Embedded AI assistants are siloed** — ten apps means ten separate AIs that can't share context.
- **Agent frameworks lack purpose-built tools** — platforms like OpenClaw burn tokens and introduce security disasters because they must use human interfaces and system-level permissions.

### What AFS provides

- **skill.md** — A standardized, machine-readable capability manifest with progressive disclosure (load only what you need, when you need it).
- **Four-layer architecture** — Interface, Documentation, Efficiency, and Security layers that can be adopted incrementally.
- **MCP-compatible** — Every AFS tool is also a valid MCP server, ensuring ecosystem compatibility.
- **Agent-agnostic** — Works with OpenClaw, Claude Code, or any AI Agent that can read skill.md and call APIs.

---

## Repository Structure

```
afs-spec/
├── README.md                          ← You are here
├── LICENSE                            ← Dual license overview
├── LICENSE-CC-BY-4.0                  ← CC BY 4.0 (documentation)
├── LICENSE-MIT                        ← MIT (code)
├── whitepaper/
│   └── afs-whitepaper-v0.1.md         ← Vision, rationale, and competitive analysis
├── spec/
│   └── overview.md                    ← Technical specification (four layers)
└── examples/
    └── afs-email/
        └── skill.md                   ← Worked example: AFS Email skill
```

| Directory | Purpose |
|-----------|---------|
| `whitepaper/` | Narrative documents explaining the motivation, core principles, and high-level architecture of AFS. |
| `spec/` | Normative technical specification. Defines the four AFS layers and their rules. |
| `examples/` | Concrete, annotated examples of AFS-compliant skill definitions. |

---

## Quick Start

1. **Read the whitepaper** — [`whitepaper/afs-whitepaper-v0.1.md`](whitepaper/afs-whitepaper-v0.1.md) for the full vision and motivation.
2. **Read the spec** — [`spec/overview.md`](spec/overview.md) for the technical specification.
3. **See an example** — [`examples/afs-email/skill.md`](examples/afs-email/skill.md) for a worked skill definition.

---

## Getting Involved

AFS is an open project and welcomes contributions of all kinds:

- **Feedback** — Open an issue to suggest changes or flag ambiguities.
- **Proposals** — Submit a pull request against `spec/` or `whitepaper/`.
- **Examples** — Add a new directory under `examples/` with a `skill.md` for your use case.

---

## Roadmap

| Milestone | Status |
|-----------|--------|
| v0.1 — Whitepaper + repository scaffold | ✅ Complete |
| v0.2 — Normative spec for Interface & Documentation layers | 🟡 In progress |
| v0.3 — Efficiency & Security layers + JSON Schema for skill definitions | ⬜ Planned |
| v1.0 — Stable specification, reference validator, and official examples | ⬜ Planned |

---

*This project is documentation-first. No build tooling or code is included at this stage.*

*© Norrai-lab contributors. Documentation licensed under [CC BY 4.0](LICENSE-CC-BY-4.0). Code licensed under [MIT](LICENSE-MIT).*
