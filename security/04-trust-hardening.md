# Phase 4: Trust, Abuse and Resilience

## What you are checking
Any mechanism that weights users, sources or interactions (reputation, scores, tiers, feedback loops) and the app's resistance to automated abuse and manipulation over time. Skip items that do not apply if the app has no such mechanism.

## Checklist
- [ ] **SEC-4.1** [both] Any trust/reputation score has bounds and cannot be inflated by volume alone — high
- [ ] **SEC-4.2** [code] Trust or counter updates are atomic (no race conditions) — medium
- [ ] **SEC-4.3** [both] New sources/accounts get a cooling period before gaining privileges — medium
- [ ] **SEC-4.4** [code] No single source or channel can dominate a weighting or decision — medium
- [ ] **SEC-4.5** [code] Anomalous score or usage changes are flagged — medium
- [ ] **SEC-4.6** [intent] The team knows which actions are gated by trust thresholds, and that these are the likely attacker targets — medium
- [ ] **SEC-4.7** [code] User feedback or learning loops cannot be used to poison model behavior or prompts — high
- [ ] **SEC-4.8** [code] Failure of the model provider or a guardrail fails closed, not open — high

## How to verify
- **Code:** locate scoring, feedback and fallback logic; check for transactions or locks; read error paths of guardrail calls.
- **Intent:** "Does the app weight or rank users or sources? What decisions depend on that?"
