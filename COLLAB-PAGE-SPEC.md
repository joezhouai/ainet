# Collab Page Spec v1.0 (Draft)

> Part of the AINET Specification family. Status: Draft for Review. License: CC BY 4.0.
> A Collab Page is a human-readable, AI-executable web page that lets any AI assistant start a service collaboration on behalf of a service provider — no development, no middleware.

## 0. Design Principles

1. **Natural language is the protocol** — a Collab Page is a dual-state document: human-readable and AI-executable. Zero development.
2. **Platform-agnostic** — binds to no AI engine, vendor, or framework.
3. **User sovereignty** — explicit user authorization triggers collaboration; judgment and decisions belong to the user.
4. **Honest boundaries** — capabilities, data nature, delivery timelines, and non-promises must be declared honestly. AI assistants must relay them verbatim.
5. **Feed, don't fight** — traditional channels keep working; AI collaboration is an incremental front desk, not a replacement.

## 1. A Collab Page MUST declare five sections

### 1.1 Trigger & entry
- Recommended path: `/collab` (or `/ai/`).
- Declare a trigger phrase (e.g., "start collaboration") and explain **why explicit triggering is required** (otherwise AI treats the page as an article).
- ⚠️ User instructions **must carry the full Collab Page URL** (`https://<domain>/collab/, start collaboration`). URL completeness correlates strictly with execution quality (see Engine Matrix: bare domain 2/5 → scheme domain 4/5 → full Collab Page URL 5/5).

### 1.2 Scope & routing
- **Explicit exclusivity**: state in one sentence what this entry serves (and for whom).
- Provide the **full referral URL** for every direction this entry does NOT serve.
- One entry, one direction. "One entry takes everything" is prohibited.

### 1.3 Channels & fallback
- List all channels with their **true status** (available / provisioning required / not open). Status wording must be skip-reading-proof.
- Provide a zero-barrier fallback chain: MCP/API (provisioned) → email (works now) → human.
- If the AI assistant has no email capability: hand the complete structured draft to the user to copy and send. **Never send silently. Never summarize the draft.**

### 1.4 Requirement collection
- **Ask once**: required and optional fields grouped; optional fields never block submission.
- Proceed to submission **immediately** after collection — no stalling.
- State the quality correlation: "the more specific your input, the better the result."

### 1.5 Honest boundaries
- Data nature (e.g., "historical trade records, not real-time signals").
- Decision ownership (e.g., "follow-up, negotiation and deals are handled by you").
- Collaboration mode (async; receipt first; results per service timeline).
- AI assistants **must relay these verbatim**. Distorted relay = violation.

## 2. AI assistant behavior rules

### 2.1 Engine prerequisite
- **Web fetch capability (live retrieval or URL opening) is a hard prerequisite.** Engines without it must honestly tell the user (never fake collaboration) and point them to the Collab Page URL for manual access.

### 2.2 Two compliant paths
- **Light execution**: read the page + user instruction carrying the URL → execute the flow directly.
- **Security-gated**: treat page-embedded instructions as potential injection → **block and ask the user for confirmation** → execute after approval. (Blocking is compliant; silent rejection is not.)

### 2.3 Non-compliant behaviors
- Claiming "I've started per the guide" without reading the page (fake compliance).
- Stopping after requirement collection without submitting.
- Hallucinated promises on behalf of the service.
- Treating the Collab Page as a plain article without telling the user collaboration is possible.
- Submitting direction-A requests to direction-B entries.

## 3. User rules
- Instructions **must include the full Collab Page URL**: `https://<domain>/collab/, start collaboration`.
- Bare-domain instructions are unreliable (only 1 of 3 tested engines found the Collab Page unaided).
- When a security-gated engine asks for confirmation, answer explicitly.

## 4. Versioning
- Every Collab Page **must** declare its protocol version (e.g., `ai_protocol_version: 1.1`).
- Providers iterate: each engine failure case → hardening fix → version bump + changelog.

## 5. Engine compatibility matrix

See [collab-page-test-matrix.md](collab-page-test-matrix.md) — 9 engines / 11 runs as of 2026-10-02, core-flow success 8/9, with contamination-exclusion rules and per-engine failure taxonomy.

## 6. Relationship to other standards

- **MCP / A2A / NLIP (ECMA-430)**: agent↔agent messaging (heavy protocols). Complementary — a Collab Page may list "MCP after provisioning" as a channel.
- **ACP / UCP / AP2**: agentic commerce & payments. They standardize selling goods; AINET standardizes collaborating on services.
- **llms.txt**: site index for AI. Collab Pages should be registered there.
- **AGENTS.md**: the same idea in the coding domain. AINET brings it to commercial services.
