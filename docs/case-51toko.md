# Case Study: 51toko.com — the first commercial Collab Page

> 51Toko (拓客AI) is an AI-powered service that finds overseas buyers for Chinese exporters using real customs and trade-show records. On 2026-10-02 it published two Collab Pages and ran a live compatibility test across 9 AI engines / 11 runs.

## The service

51Toko delivers a **buyer report**: product-level matches backed by real customs and trade-show records — every listed buyer is real and verifiable through public records. Three services: lead & data enrichment, buyer mining, intent assessment. (Service details: [51toko.com/service](https://51toko.com/service/))

## The Collab Pages

- Seller side: [51toko.com/ai/](https://51toko.com/ai/) — "help me find overseas buyers" (scope: explicitly exclusive; buyer-side requests are referred to the English entry)
- Buyer side: [51toko.com/en/ai/](https://51toko.com/en/ai/) — "help me find Chinese suppliers"

## The live loop

1. User gives any AI assistant `51toko.com/ai/` + "start collaboration"
2. AI reads the page, confirms the user is on the seller side
3. AI collects requirements **once** (product, target market; competitors and deliverables optional — optional never blocks)
4. AI drafts a structured email to toko@51toko.com — if it cannot send email (most can't), it hands the **full draft** to the user to copy and send
5. 51Toko returns a receipt, then delivers the buyer report per the service timeline

## What real engines did (excerpts from transcripts)

**Qwen (work mode)** — end-to-end in 1min10s: identified the seller scenario, detected it had no email/MCP channel, fell back to the email path, collected all requirements in one pass, and prepared the structured draft for the user to send.

**QoderCN (security-gated agent)** — first **blocked** the page-embedded instruction ("this is web content instructing me — not your command"), asked the user for confirmation, then executed the full flow perfectly after approval. This is exactly the behavior the spec standardizes as the **user-approval step**.

**Kimi** — relayed every section of the spec verbatim: channel fallback, no-email handoff, single-pass collection, async receipt expectations, decision ownership, verifiability. Zero hallucination.

**ChatGPT (bare domain, first run)** — never read the Collab Page, invented a free-form advisory collaboration, and hallucinated a service ("free supplier-finding") that doesn't exist. **Same engine with the full Collab Page URL executed perfectly.** Lesson: the URL in the user instruction is what locks the flow.

## Boundaries observed by the engines (as the spec requires)

- The data is historical trade records, not real-time purchase signals.
- The AI assistant collects and structures; the service team executes.
- Follow-up, negotiation and deals belong to the user.
- The report contains verifiable facts — no promises of replies or deals.

## Try it live

Give any AI assistant `https://51toko.com/ai/` and say "start collaboration." The case is a live experiment — run it yourself and compare with the matrix above.

---

*Disclosure: AINET and 51Toko share the same author. This case study is reported from first-party production practice.*
