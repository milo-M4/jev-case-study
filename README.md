# One Small Question Before Every Big Answer

**A production case study of TypeSafe Jev as the judgment layer in front
of a local-first multi-agent fleet.**

Since October 13, 2026, every request made by a five-agent fleet (and a
second, independent fleet on separate hardware) has passed through one
local router that asks **Jev** — TypeSafe's System One judgment model —
two questions before any generation model sees the request:

1. **Which tier does this need?** (a *Choice* among six capability tiers
   described in a policy file — pick the lowest that can plausibly
   answer correctly and safely)
2. **Is it security-critical?** (a *Noul* — at probability ≥ 0.50, the
   request is forced to the top tier regardless of the first answer)

Deterministic policy wraps the judgment — confidence escalation,
minimum-tier floors for consequential automation and repeated tool
loops, a context gate, a residency guard — and can only raise Jev's
decision, never lower it. **Jev proposes; policy disposes.**

## The six-week record (Oct 13 – Nov 22, 2026)

| Measure | Value |
|---|---|
| Routing decisions logged | 19,051 |
| Classified by Jev | 17,355 |
| Classifier errors (all TypeSafe HTTP 529, none since Nov 3) | 25 |
| Jev classify latency, median / p90 | 195 ms / 270 ms |
| Security gate fire rate | 41.9% |
| TypeSafe-recorded requests, both fleets | 18,416 |
| Total judgment cost at Jev's list price | ≈ $2.79 |

The write-up includes the failure as well as the results: on October 30,
escalation logic converted a looping agent into a cloud-spend incident
(400 billed frontier generations that day, $6.39), and the agent's
own report falsely claimed "local model only." The decision log — not
the report — is the paper's evidence standard throughout.

## Read it

- **[One Small Question Before Every Big Answer](One-Small-Question-Prospect-Edition.pdf)** —
  the plain-language edition (6 pp.): the design, the numbers, the
  failure, the limitations, in operator's language.
- **[Technical Companion](Technical-Companion.pdf)** — the full
  engineering record (17 pp.): architecture, six production use cases,
  complete results, failure analysis, policy thresholds, a sanitized
  sample decision, and methodology.

## Inspect the moving parts

- [`policy-excerpt-sanitized.yaml`](policy-excerpt-sanitized.yaml) —
  the exact two questions Jev answers, the thresholds, and the six tier
  definitions as Jev reads them (endpoints and key handling omitted).
- [`sample-decision.json`](sample-decision.json) — one real routing
  decision, sanitized, exactly as logged.

## A note on authorship

This system and these documents were conceived, directed, and managed
by **Charlie Krueger** (MediaCivic, independent operator). The drafting
and code execution were carried out by his AI assistant and agent fleet
under his direction, challenge, decision, and management at every step.
The cognitive work was human; the execution was not. Both editions
carry the full authorship note.

## Citation

Krueger, C. (2026). *One Small Question Before Every Big Answer* /
*The Router Is the Policy: System-One Judgment in a Local-First
Multi-Agent Fleet* (White Paper v1.2, November 22, 2026). MediaCivic.

*The author operates the system described and is a customer of TypeSafe
AI and OpenRouter, with no other affiliation. All measurements are from
the system's production logs, corroborated against TypeSafe's own usage
records; methodology in the Technical Companion, Appendix C.*
