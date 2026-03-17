---
title: "AFS — Agent-Friendly Standard"
subtitle: "Whitepaper v0.1"
author:
  - Norrai-lab
date: "March 2026"
abstract: |
  AFS (Agent-Friendly Standard) is an open specification that defines how software
  should be designed from the ground up so that AI agents can discover, understand,
  and interact with it safely, efficiently, and reliably. Rather than forcing AI to
  navigate human interfaces, AFS makes software a first-class tool for AI agents.
keywords: [Agent-Oriented System Design, Software Engineering, AI Agent, MCP]
# Eisvogel PDF template options
titlepage: true
titlepage-color: "1a1a2e"
titlepage-text-color: "FFFFFF"
titlepage-rule-color: "e94560"
toc-own-page: true
number-sections: true
colorlinks: true
linkcolor: "e94560"
---


# AFS Whitepaper v0.1 — Agent-Friendly Standard

*"Don't teach AI to use human software — make software a good tool for AI."*

*Version:* 0.1 (Draft)
*Status:* Work in progress
*Date:* March 2026

---

## 1. Introduction

We are witnessing a paradigm shift in how humans interact with software. The rise of autonomous AI agents — capable of reasoning, planning, and executing multi-step workflows — demands a fundamental rethinking of software design. Today's software was built for humans: graphical interfaces, mouse clicks, and manual copy-paste between applications. AI agents forced to navigate this human-centric landscape waste enormous resources, introduce security vulnerabilities, and deliver unreliable results.

**AFS (Agent-Friendly Standard)** is an open specification that flips the script. Instead of making AI adapt to human software, AFS defines how software should be designed from the ground up to be a good tool for AI agents. AFS provides a common vocabulary, layered architecture, and lightweight conventions that make any service or tool "agent-ready" — enabling safe, efficient, and reliable interactions.

This whitepaper explains the motivation behind AFS, its core design philosophy, technical architecture, and positioning within the broader AI + software ecosystem. For the normative technical specification, see [`spec/overview.md`](../spec/overview.md).

---

## 2. The Problem: AI + Software Interaction Is Broken

### 2.1 Making AI Operate Human Interfaces Is Costly

The dominant approach today is to make AI "learn" human software — through screenshots, simulated clicks, and browser automation. This approach has severe limitations:

- **Massive token consumption**: AI must process large screenshot images and UI element metadata, resulting in extremely high costs.
- **Unreliable**: Page load timeouts, unlocatable buttons, layout changes, and race conditions cause frequent failures. Agents easily fall into infinite retry loops.
- **Actively resisted**: Many websites and applications deploy anti-bot measures, leading to account bans and access restrictions.

### 2.2 Every Application Ships Its Own AI — A Fragmented Experience

The current SaaS trend is for every product to embed its own AI assistant: Zoom has its AI, Miro has its AI, Qlik Sense has its AI. This creates four core problems:

- **Context fragmentation**: Ten applications means ten separate AIs, each unaware of the others. Zoom AI summarizes a meeting — but getting Miro AI to create a board from those notes requires manual copy-paste.
- **Redundant billing**: Users pay for essentially the same LLM capability separately in every application.
- **Inconsistent quality**: Some embedded AIs are excellent, others are barely functional. Users have no choice.
- **Vendor lock-in**: Zoom's AI can only operate Zoom. Cross-application orchestration is impossible.

### 2.3 Lessons from OpenClaw — Right Direction, Wrong Infrastructure

OpenClaw (formerly Clawdbot / Moltbot) is the open-source AI Agent that exploded in popularity in early 2026, surpassing Linux in GitHub stars. It validated the overwhelming user demand for "one AI agent to rule them all." But OpenClaw also exposed the deep infrastructure gaps:

- **Token burn**: OpenClaw interacts with human software through browsers and bash commands. A single instance can consume over 50 million API tokens per day. This not only costs a fortune but floods the context window with irrelevant information, degrading reasoning quality.
- **Security disaster**: OpenClaw requires near-total host permissions — shell execution, file system access, email and messaging access. A single prompt-injection attack via a malicious email can cause the agent to leak secrets, delete data, or execute arbitrary code. Security researchers have identified over 40,000 vulnerabilities; Microsoft, Cisco, and Kaspersky have all issued warnings.
- **Skill ecosystem pollution**: OpenClaw's skill marketplace (ClawHub) has become a breeding ground for malicious code. Audits by Snyk show that over 36% of skills contain security flaws, with 13.4% rated critical — including malware distribution and credential theft. The root cause: skills are just Markdown files with near-zero upload barriers, no code signing, and no security review.

**The root cause** is not the "one AI for everything" vision — it's that OpenClaw uses *human tools* to orchestrate everything. It directly operates browsers, executes bash, and accesses arbitrary files because there are no purpose-built AI-friendly tools. The only option is to give the agent system-level permissions, making the blast radius unlimited.

---

## 3. Core Vision: One AI, All Tools

AFS proposes a fundamental inversion:

> **Current model**: "Software with an AI inside" — AI is a feature embedded in each application, trapped in its silo.
>
> **AFS model**: "AI with software at its fingertips" — AI is the orchestration hub. Software returns to its essence as a tool, invoked by AI on behalf of the user.

Users describe their intent in natural language. The AI Agent autonomously decides which tools to invoke, how to compose workflows, and shares context across all interactions seamlessly.

AFS is also CFS — **Claw-Friendly Standard**. OpenClaw proved the demand; AFS provides the supply. AFS-compliant software can be safely and efficiently invoked by OpenClaw, Claude Code, or any other AI Agent — without binding to any single platform.

---

## 4. Design Philosophy: Progressive Disclosure & skill.md

### 4.1 Progressive Disclosure for AI

Progressive Disclosure is a classic interaction design principle: don't dump all information at once; reveal it as needed. AFS applies this to AI-software interaction: an agent doesn't need to "see" every feature of a tool upfront. Instead, it accesses layered documentation on demand.

### 4.2 skill.md — The Software's Self-Introduction

The core innovation of AFS is **skill.md** — a structured capability manifest that accompanies every AFS-compliant tool. It is not an ad-hoc README but a machine-readable document with a standardized format, organized by progressive disclosure layers:

| Layer | Content | Token Cost |
|-------|---------|------------|
| **Layer 0 — Overview** | One-sentence description of what the tool does | Minimal — enables quick relevance filtering |
| **Layer 1 — Capabilities** | Available APIs, parameters, and return formats | Moderate — loaded when the tool is needed |
| **Layer 2 — Examples** | Common usage patterns and workflow templates | Loaded on demand for complex scenarios |
| **Layer 3 — Advanced** | Edge cases, error handling, performance tuning | Rarely loaded — only for deep troubleshooting |

An AI Agent reads Layer 0 to decide if a tool is relevant, Layer 1 to understand how to use it, and Layers 2–3 only when necessary. Each interaction consumes the minimum possible tokens, rather than stuffing the entire manual into context.

### 4.3 user-best-practice.md — User-Defined Workflows

Beyond the developer-provided skill.md, AFS allows users to author **user-best-practice.md** files that define their own recurring workflows. For example: *"Every Monday morning, query last week's sales data, identify the categories with the steepest decline, generate a report, and email it to me."* The AI Agent reads this file and executes tasks like a well-trained assistant, following the user's established habits.

### 4.4 Key Difference from OpenClaw Skills

| Dimension | OpenClaw Skill | AFS skill.md |
|-----------|---------------|--------------|
| **Essence** | Instructions *to* the Agent ("how to use human tools") | The tool's self-introduction ("what I can do") |
| **Security** | Arbitrary Markdown; can contain malicious instructions; 36% have security flaws | Standardized format + security review; describes API interfaces only |
| **Token efficiency** | No standard; Agent must load entire content | Progressive disclosure; load layers on demand |
| **Universality** | OpenClaw ecosystem only | Any AI Agent can use it |

---

## 5. Technical Architecture

### 5.1 System Overview

The system is organized into three tiers:

1. **User Tier**: Users interact with an independent AI Agent using natural language.
2. **Agent Tier**: The AI Agent orchestrates multiple AFS-compliant tools via standardized APIs.
3. **Tool Tier**: Each AFS tool (e.g., AFS-BI, AFS-Docs, AFS-Email) exposes structured interfaces and optionally provides a human UI.

### 5.2 Three Interface Layers per AFS Tool

Every AFS-compliant tool provides three interaction surfaces, all backed by the same core logic:

| Interface | Audience | Purpose |
|-----------|----------|---------|
| **API** | AI Agents (primary) | Structured I/O, token-efficient, reliable |
| **CLI** | Developers / Ops | Thin wrapper over the API for debugging and scripting |
| **Human UI** | End users | Graphical interface for users who prefer direct interaction |

### 5.3 The Four AFS Layers

| Layer | Content | Problem Solved |
|-------|---------|----------------|
| **Layer 1: Interface** | MCP-compatible structured APIs with explicit I/O schemas | Unified communication standard; compatible with existing ecosystems |
| **Layer 2: Documentation** | skill.md + user-best-practice.md with progressive disclosure | AI can fetch information on demand; users can customize workflows |
| **Layer 3: Efficiency** | Compact response formats, verbosity toggles, pagination, streaming | Minimize token consumption; maximize response speed |
| **Layer 4: Security** | Permission declarations, dangerous-operation confirmations, audit logs, rollback interfaces, code signing | Fundamentally address security issues exposed by OpenClaw |

---

## 6. Competitive Analysis

### 6.1 Four Approaches to AI + Software

| Approach | Representatives | Characteristics |
|----------|----------------|-----------------|
| **Screen-level adaptation** | Computer Use, Operator | Zero modification cost, but slow, expensive, and unreliable |
| **Agent frameworks** | OpenClaw | Visionary, but burns tokens via human tools, severe security holes, polluted skill ecosystem |
| **Protocol-level adaptation** | MCP / Function Calling | Adds interfaces to existing software, but doesn't address software design issues; inconsistent response quality |
| **Software-level redesign** ★ | **AFS** | Optimized for AI from the design level; maximum efficiency and reliability; compatible with all Agent platforms |

### 6.2 AFS and MCP: Complementary, Not Competing

AFS does not replace MCP — it raises the bar above MCP. An analogy: **MCP is like HTTP; AFS is like the RESTful API design convention.** Every AFS tool is simultaneously an MCP server, but additionally satisfies AFS quality requirements for documentation, efficiency, and security.

### 6.3 AFS and OpenClaw: Solving the "Chef Without Ingredients" Problem

OpenClaw is an excellent AI Agent framework, but it faces a "chef without ingredients" dilemma: it can only use bash, browsers, and raw APIs to accomplish tasks because the market lacks purpose-built AI Agent tools. AFS tools are those "ingredients" — they enable OpenClaw (and any other Agent) to complete tasks safely, efficiently, and reliably, without requiring system-level permissions.

---

## 7. Core Advantages

### ① Token Savings — Less Cost, Less Energy

Through structured APIs, compact response formats, and skill.md's progressive disclosure design, AFS dramatically reduces token consumption. Shorter context windows mean lower cost, faster responses, and higher AI reasoning quality. Compared to OpenClaw's 50M+ tokens per instance per day, AFS can reduce token usage for equivalent tasks by an order of magnitude.

### ② Security by Design

OpenClaw's security problems are not bugs — they are architectural flaws: it *must* grant system-level permissions to function. AFS solves this fundamentally: tools expose only limited operation interfaces, and actual operations are executed by the tool itself. Even under prompt injection attacks, the agent cannot breach interface boundaries. Agents no longer need bash or file system access; the blast radius shrinks from "the entire system" to "a single tool's API surface."

### ③ Reliability

Structured interfaces are far more reliable than screen-level operations or bash command parsing. No more "button not found," "page timed out," or "output format changed" failures. In enterprise contexts, this may be even more compelling than token savings.

### ④ Shared Context, Cross-Tool Collaboration

A single AI Agent orchestrates all tools with naturally shared context. Users no longer need to manually copy-paste between different applications' AI assistants or pay separately for each one.

### ⑤ Agent-Agnostic, Maximum Portability

AFS tools are not bound to any specific Agent. Whether OpenClaw, Claude Code, a future GPT Agent, or any new framework — as long as it can read skill.md and call APIs, it can use AFS tools. This contrasts sharply with OpenClaw's closed skill ecosystem.

---

## 8. Market Strategy

### Dual Track for Existing Software Giants

- **Track A — Adaptation Layer**: Wrap existing software's public APIs (Zoom, Miro, etc.) into AFS-compatible interfaces using MCP adapters. Solves the "can we use it?" problem.
- **Track B — Replacement Layer**: Build AFS-native software in specific verticals to deliver a 10× experience advantage over legacy approaches. Solves the "is it any good?" problem.

The realistic path: **A first, B gradually replaces.** The adaptation layer addresses availability; native software addresses quality.

---

## 9. Vision: The First Step Toward Agent OS

We are witnessing an irreversible industry shift: from the "software + embedded AI" bundling model to a new paradigm where **AI is the entry point and hub, and software becomes AI's plugins**.

AFS's ultimate vision is to become the foundation layer of an **Agent OS**. Just as an operating system defines the rules for how applications interact with hardware, AFS defines the rules for how AI Agents interact with software tools. As more software adopts AFS, a software ecosystem centered on AI will naturally emerge — this is the Agent OS.

In this future, users describe their needs in a single sentence, and AI automatically orchestrates multiple tools to complete complex workflows. No context fragmentation, no redundant billing, no manual copy-paste, no security nightmares.

**AFS is the standard that writes the rules for this future.**

---

*© Norrai-lab contributors. Licensed under [CC BY 4.0](../LICENSE-CC-BY-4.0).*
