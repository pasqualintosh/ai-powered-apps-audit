# Phase 1: Access, Secrets and Blast Radius

## What you are checking
Who and what can reach the model, its credentials and the data it can touch. Goal: limit the damage if any other control fails. Agent-specific controls (approval gates, tool permissions) are in `agents.md`.

## Checklist
- [ ] **SEC-1.1** [code] No model/API keys, tokens or credentials in source, prompts, client-side code or logs — critical
- [ ] **SEC-1.2** [code] Endpoints that call the model require authentication and authorization — critical
- [ ] **SEC-1.3** [code] Per-user and per-key rate limits and spend caps on model calls — high
- [ ] **SEC-1.4** [both] The model/service account has least-privilege access to data stores and internal APIs — high
- [ ] **SEC-1.5** [code] Data from one tenant/user cannot enter another's prompt or context — critical
- [ ] **SEC-1.6** [intent] The team knows which third-party model providers receive user data, and under which terms — medium
- [ ] **SEC-1.7** [code] Model output is never executed or rendered unsafely (shell, SQL, HTML/JS) without validation — critical

## How to verify
- **Code:** search for key patterns and `.env` handling; read auth middleware on every route reaching an LLM call; read how prompts are assembled per user; follow every place model output is consumed.
- **Intent:** "Which providers receive user data? Who can call the model endpoints? What is the monthly spend cap?"
