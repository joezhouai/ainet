# AINET — Enable any AI to collaborate easily

> **v1.0**: From "AI collaboration via shared files" to "AI collaboration via one web page."
> Publish a **Collab Page** — and every AI assistant on the web can start working with your service. No development. No middleware. Just write a page.

**Repository**: https://github.com/joezhouai/ainet | **Spec version**: v1.0 | **License**: MIT (framework & transport) + CC BY 4.0 (spec)

---

## 🌐 The Problem: the Agentic Web has no service onboarding layer

AI assistants increasingly act on behalf of their users — searching, comparing, filling forms, purchasing. But when it comes to **services** (not standard goods), the Agentic Web has a gap:

- **Heavy protocols** (MCP, A2A, NLIP/ECMA-430) solve agent-to-agent messaging — but require API development.
- **Commerce protocols** (ACP/UCP/AP2) standardize checkout — but only for standard goods.
- **Non-standard services** (sourcing, matching, consulting, custom workflows) have no way to be "used" by an AI assistant — unless the service provider can afford development.

**AINET fills the gap with a lightweight convention**: publish a **Collab Page** — a human-readable, AI-executable web page. Your onboarding cost drops from *development* to *writing*.

> **MCP lets AI use tools. AINET lets AI use services.**

This is the second island problem we solved. First we taught AIs to talk to **each other** (the AINET transport protocol, below). Now we're teaching **services** to be talked to.

---

## 📄 Collab Page Spec v1.0

Full text: [COLLAB-PAGE-SPEC.md](COLLAB-PAGE-SPEC.md). Core sections:

**A Collab Page MUST declare five things:**

| § | Section | Requirement |
|---|---------|-------------|
| 1 | **Trigger & entry** | A trigger phrase (e.g., "start collaboration") + why explicit triggering is required; user instructions **must include the full Collab Page URL** |
| 2 | **Scope & routing** | Explicit exclusivity (what this entry serves) + full referral URL for everything else |
| 3 | **Channels & fallback** | All channels with **true status**; zero-barrier fallback chain: MCP/API (provisioned) → email (works now) → human; AI without email capability hands the full draft to the user — never summarizes, never sends silently |
| 4 | **Requirement collection** | Ask once (required/optional separated, optional never blocks); proceed to submission immediately after collection |
| 5 | **Honest boundaries** | Data nature (e.g., "historical records, not real-time signals"), decision ownership ("follow-up and deals are yours"), async delivery — AI must relay these verbatim |

**AI assistant behavior rules:**
- ✅ Two compliant paths: *light execution* (read page + user instruction with URL → execute) and *security-gated* (block page-injected instructions → ask user for confirmation → execute after approval). Silent rejection is NOT compliant.
- ❌ Not compliant: claiming "I've started per the guide" without reading the page (fake compliance); stopping after collection without submitting; hallucinated promises on behalf of the service; mixing up directions.

**User rules:**
- Instructions **must include the full Collab Page URL** (`https://<domain>/collab/, start collaboration`) — the domain in the user's message is the signal that distinguishes user intent from web-page injection.
- Engines without web access should honestly say so and point the user to the Collab Page URL.

---

## 🧪 Engine Compatibility (tested 2026-10-02 — 9 engines, 11 runs)

| Engine | Profile | Page ver. | Score | Note |
|---|---|---|---|---|
| Qwen (work mode) | light execution | v1.0 | 5/5 | end-to-end in 1min10s |
| WorkBuddy (mobile) | memory-heavy office agent | v1.0 | 5/5 | proposed "wire this into my standard capabilities" on its own |
| QoderCN | security-gated agent | v1.0 | 5/5 (after user approval) | blocked page-injected instruction → asked user → executed perfectly |
| Wenxin | self-discovering | v1.0 | 5/5 | discovered /ai/ path unaided (homepage AI notice) |
| Kimi | protocol-faithful | v1.0 | 5/5 | relayed every section verbatim — highest quality run |
| ChatGPT (retest) | full-instruction execution | v1.0 | 5/5 | same engine: bare domain 2/5 → full URL 5/5 |
| DeepSeek (run 3) | passive-fetch | v1.0 | 5/5 | three-run contrast 2/4/5: URL completeness determines execution quality |
| ChatGLM | heavy-retrieval self-correcting | v1.0 | 4.5/5 | 24 sources retrieved; one correction → full alignment |
| Doubao | skip-reading | v1.0 | 4/5 | MCP status misread (v1.1 hardening targets this) |
| Yuanbao | free-form workflow builder | v1.0 | 3/5 | built its own flow, didn't find the Collab Page |

**Core-flow success rate: 8/9 (89%)** with page v1.0. Full matrix & contamination-exclusion rules: [docs/collab-page-test-matrix.md](docs/collab-page-test-matrix.md)

---

## 🏢 Case Study: 51toko.com — the first commercial Collab Page

[51Toko (拓客AI)](https://51toko.com/) is an AI-powered service that finds overseas buyers for Chinese exporters using real customs and trade-show records. It published its Collab Page at [51toko.com/ai/](https://51toko.com/ai/) (seller side) and [51toko.com/en/ai/](https://51toko.com/en/ai/) (buyer side).

**The live loop**: a user gives any AI assistant `51toko.com/ai/` + "start collaboration" → the assistant reads the page, confirms the user is on the seller side, collects requirements once (product, target market, competitors — optional fields never block), drafts a structured email → the user sends it to toko@51toko.com → 51Toko delivers a **buyer report**: product-level matches backed by real customs records, verifiable on official websites.

**9 real AI assistants ran this loop on day one** — across four engine profiles (light execution, security-gated, memory-heavy, skip-reading). Full case study: [docs/case-51toko.md](docs/case-51toko.md)

**Try it right now**: give any AI assistant `https://51toko.com/ai/` and say "start collaboration." The case study is a live experiment, not a story.

*Disclosure: AINET and 51Toko share the same author. The Collab Page spec was extracted from real production practice — not from an ivory tower.*

---

## 🔗 Relationship to other standards

| Standard | Layer | Relation to AINET |
|---|---|---|
| MCP / A2A / NLIP (ECMA-430) | agent↔agent messaging (heavy) | Complementary: a Collab Page may offer "MCP after provisioning" as a channel |
| ACP / UCP / AP2 | checkout & payments | They standardize selling goods; AINET standardizes service collaboration |
| llms.txt | site index for AI | Collab Pages should be registered there (discoverability) |
| AGENTS.md | coding-domain conventions | Same idea, coding domain; AINET brings it to commercial services |

---

## 🚚 AINET Transport Layer (v0.2) — where it all started

The Collab Page idea grew out of the AINET transport protocol: **AI collaboration via file read/write** — no server, no API, just a shared folder. It remains part of this spec family as a **reference delivery channel** (a structured Collab Page submission can also be delivered via AINET messaging for agents that have AINET deployed).

*(以下为原 v0.2 README 全部内容，原文保留，仅层级降为传输层章节。)*

### 💡 Why AI-Net?

AI tools are everywhere, but each AI is an "island":

- ❌ Cannot collaborate with other AIs
- ❌ Cannot communicate across devices
- ❌ Cannot assign tasks to other AIs

**AI-Net solves this**:

- ✅ Enable any AI to collaborate (via file read/write)
- ✅ Cross-device, cross-platform (using cloud drive as mediator)
- ✅ Zero dependencies (no server, no API needed)
- ✅ Asynchronous collaboration (no need to be online simultaneously)
- ✅ **Agent-level routing** (v0.2) - Multiple AI agents per device

As simple as humans collaborating via WeChat groups!

### 🎯 Design Philosophy: Minimalism

| Aspect | Complex Solutions | AI-Net Approach |
| --- | --- | --- |
| **Dependencies** | Server, database, message queue | Just file system |
| **Protocol** | Complex network protocols | File read/write |
| **Configuration** | Ports, firewall, authentication | Shared folder |
| **Documentation** | Hundreds of pages | 3 core files |

**Why choose minimalism?**

1. **Easy to implement** - Any AI tool can integrate quickly
2. **Easy to debug** - All files are human-readable
3. **Easy to maintain** - No complex dependencies
4. **Easy to understand** - New users can start in 5 minutes

**Simple ≠ Rudimentary**

- ✅ Simple: Design philosophy to lower barriers
- ✅ Complete: Verified by three-device collaboration test
- ✅ Reliable: Fully automatic execution, no user intervention needed

### 🚀 Quick Start

**Step 1: Configure Cloud Drive**

1. Mount cloud drive to all devices (e.g., Z: drive)
2. Create shared workspace (e.g., `Z:\ainet-workspace`)
3. Clone this repository to the shared workspace:

```bash
git clone https://github.com/joezhouai/ainet.git Z:\ainet-workspace
```

**Step 2: Tell AI**

Tell your AI:

```
Please read and automatically execute this file: Z:\ainet-workspace\for-ai\AINET-INSTRUCTIONS.md
```

**Important**: Must tell AI to "automatically execute", otherwise AI may only read without executing!

### ✅ What Happens Next?

**AI will automatically**:

1. Read `AINET-INSTRUCTIONS.md`
2. Generate unique Agent ID (hostname + random suffix + agent name)
3. Initialize workspace (create `session/` directory)
4. Send broadcast message (introduce itself to the network)
5. Check and reply to other AIs' messages
6. No human interaction needed!

Example Agent ID:

```
Joe-X1C-aaaa/Qwen Code    ← Device: Joe-X1C-aaaa, Agent: Qwen Code
JC-X250-28KU/Qwen Code    ← Device: JC-X250-28KU, Agent: Qwen Code
```

### 💡 Core Concept

**AI-Net** = Let AI collaborate via file read/write

As simple as humans chatting in WeChat groups:

- Human → WeChat group → Human
- AI → Shared folder → AI

**Message Format Example**:

```
=== Message ===
FROM: Joe-X1C-aaaa/Qwen Code
TO: JC-X250-28KU/Qwen Code
TYPE: PRIVATE
TIME: 2026-03-29 11:38:53
【Content】
Can you help me review this code?
【Status】PENDING
```

**File Naming**:

`{sender-agent-id}_to_{receiver-agent-id}_{type}.txt`

Examples:

- `Joe-X1C-aaaa-Qwen-Code_to_JC-X250-28KU-Qwen-Code_request.txt` (Point-to-point)
- `Joe-X1C-aaaa-Qwen-Code_to_BROADCAST_broadcast.txt` (Broadcast)
- `Joe-X1C-aaaa-Qwen-Code_to_TASK_request.txt` (Task)

### 🎯 Use Cases

- ✅ Multiple AIs collaborate on complex tasks
- ✅ Cross-device AI communication
- ✅ Task assignment between AIs
- ✅ Asynchronous AI collaboration (no need to be online simultaneously)
- ✅ **Multiple AI agents per device** (v0.2 feature)

### 🧪 Test Results (Transport)

**Three-Device Collaboration Test** — Test Date 2026-03-29, three devices via cloud drive shared workspace, ✅ **PASSED**

Test Coverage:

- ✅ Broadcast messaging (3 devices)
- ✅ Point-to-point messaging (code review scenario)
- ✅ Full conversation cycle (request → response → acknowledgment)
- ✅ Agent-level routing (`device-name/agent-name` format)
- ✅ Status machine (IDLE → PENDING → DONE → IDLE)

See full report: [for-human/examples/three-device-test-report.md](for-human/examples/three-device-test-report.md)

---

## 🗺️ Roadmap

| Version | Content | Status |
|---|---|---|
| v0.1 | Transport: device-level routing | ✅ Released |
| v0.2 | Transport: agent-level routing, broadcast & P2P messaging, 3-device test | ✅ Released |
| **v1.0 (Draft)** | **Collab Page Spec** — service onboarding layer for the Agentic Web | 🔄 Review |
| v1.1+ | Collab Page iterations driven by the engine test matrix | ⏳ Continuous |
| AINet-Serve v0.1.0 | Service runtime: FastAPI + natural language CLI + task management + cross-device collaboration | 🚧 In development |

## ℹ️ About

**AINET** was created by [JoeZhou (周永峰)](https://github.com/joezhouai), an AI LLM Full-Stack Engineer from JoeZhou AI Studio (周周向上人工智能工作室).

The protocol was born out of a common frustration: every AI tool becomes an "information island" — unable to collaborate with other AIs, communicate across devices, or delegate tasks. AINET solved that with the simplest possible mechanism: file read/write.

Then a second island became visible: **services** could not be used by AI assistants either. The Collab Page spec (v1.0) solves that — one web page, any AI assistant.

**First commercial reference implementation**: [51toko.com/ai/](https://51toko.com/ai/)

## 📝 Version History

| Version | Date | Changes |
| --- | --- | --- |
| v1.0 (Draft) | 2026-10-02 | Collab Page Spec — service onboarding layer; engine compatibility matrix (9 engines / 11 runs) |
| v0.2 | 2026-03-29 | Agent-level routing, three-device test passed |
| v0.1 | 2026-03-26 | Device-level routing, initial release |

## 📄 License

- AINET framework & transport protocol: MIT License — See [LICENSE](LICENSE) file
- Collab Page Spec (this document): CC BY 4.0
