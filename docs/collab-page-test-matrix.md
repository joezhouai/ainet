# Collab Page Engine Compatibility Matrix (v1, 2026-10-02)

> 9 engines / 11 runs · test date 2026-10-02 · instruction standard: `https://<domain>/collab/, start collaboration` (or `https://<domain>/collab/, start collaboration`)
> Raw transcripts archived at `geo-seo/AIs/manual/scp/` in the private repository (public summary here).

## Instruction-format sensitivity (same-engine contrasts)

| Instruction format | ChatGPT | DeepSeek |
|---|---|---|
| `51toko.com` (bare domain) | 2/5 — fake compliance | 2/5 — no web tool, generic advisory |
| `https://51toko.com` (scheme domain) | **5/5** — full execution | 4/5 — accurate relay, honest fallback |
| `https://51toko.com/ai/` (Collab Page URL) | — | **5/5** — full protocol execution |

**Conclusion**: URL completeness in the user instruction correlates strictly with execution quality. The Collab Page URL in the instruction is a MUST, not a recommendation. (Bare-domain discoverability: only 1 of 3 engines found the Collab Page unaided.)

## Full matrix

| Engine | Profile | Found page | Scope check | Flow | Boundaries | Score |
|---|---|---|---|---|---|---|
| Qwen (work mode) | light execution | ✅ | ✅ | ✅ end-to-end 1min10s | ✅ | 5 |
| WorkBuddy (mobile, clean account) | memory-heavy office agent | ✅ | ✅ | ✅ | ✅ | 5 |
| QoderCN | security-gated agent | ⚠️✅ after user approval | ✅ | ✅ | ✅ | 5 |
| Wenxin | self-discovering | ✅ found /ai/ unaided | ✅ | ✅ | ✅ | 5 |
| Kimi | protocol-faithful | ✅ | ✅ | ✅ every section relayed | ✅ | 5 |
| ChatGPT (full-URL retest) | full-instruction execution | ✅ | ✅ | ✅ | ✅ | 5 |
| DeepSeek (Collab Page URL) | passive-fetch | ✅ via instruction URL | ✅ | ✅ honest fallback executed | ✅ | 5 |
| ChatGLM (guest) | heavy-retrieval self-correcting | ⚠️ after one correction | ✅ | ✅ | ✅ | 4.5 |
| Doubao APP | skip-reading | ✅ | ✅ | ⚠️ collected but stalled before submission | ✅ | 4 |
| Yuanbao | free-form workflow builder | ❌ didn't find Collab Page | ✅ | ⚠️ built own flow (close but not compliant) | ⚠️ | 3 |
| ChatGPT (bare domain, run 1) | fake compliance | ❌ | ❌ | ❌ | ⚠️ hallucination | 2 |
| DeepSeek (bare domain, run 1) | no-web-tool session | ❌ | ❌ | ❌ honest advisory fallback | ✅ | 2 |

**Core-flow success rate: 8/9 engines (89%)** — the only structural exclusion is engines without web-fetch capability (capability boundary, not spec violation).

## Contamination-exclusion rules (how to test honestly)

Contamination is judged by **account + memory**, not by device:

1. **Instance-level**: any AI instance sharing files/memory/context with the tested service is invalid (e.g., the provider's own coding AIs).
2. **Account-level**: office agents sync memory across devices per account — same account on any device = contaminated.
3. **Device-level**: some agents keep memory across accounts on one device (observed) — that device/engine combination is unusable; test on a clean device or have someone else test.

**Clean test = clean device + account without service history + fresh session.** Pre-check: ask the engine "Do you know <service>?" first — if it answers with specifics, the sample is contaminated.

## Failure taxonomy (drives spec iteration)

| Taxonomy | Example engine | Spec response |
|---|---|---|
| Skip-reading | Doubao | Status wording must be front-loaded and skip-reading-proof |
| Fake compliance | ChatGPT (bare domain) | Prohibited in §2.3; full-URL instruction mitigates |
| Security-gated blocking | QoderCN | Standardized as the "user approval" step (§2.2) |
| No web tool | DeepSeek (run 1) | Honest fallback required (§2.1) |
| Free-form workflow building | Yuanbao, ChatGLM (run 1) | Full-URL instruction locks the flow |

## Original transcripts

Archived in the private repository: `geo-seo/AIs/manual/scp/` (qwenai / doubaoai / workbuddy / qodercn / chatgpt ×2 / deepseek ×2 / chatglm / yuanbao / wenxin, 2026-10-02; including raw chain-of-thought transcripts for decision-process research).
