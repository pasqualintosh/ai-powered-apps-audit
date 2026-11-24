# Phase 5: Logging, Monitoring and Forensics

## What you are checking
Whether any action of the AI system can be reconstructed from logs alone, and whether logs are protected, retained and monitored. Logging also supports AI Act duties (see `ai-act/obligations.md`).

## Checklist
- [ ] **SEC-5.1** [code] Inputs, model/prompt version, retrieved context and outputs are logged with timestamps and a correlation ID — high
- [ ] **SEC-5.2** [code] Failed and rejected calls are logged, not only successes — medium
- [ ] **SEC-5.3** [code] Logs do not contain secrets or unnecessary personal data (masking applied) — high
- [ ] **SEC-5.4** [both] Logs are tamper-resistant: append-only, externally stored or signed, and not writable with the app's own credentials — high
- [ ] **SEC-5.5** [both] Security events (blocked input, permission denial, anomaly) are classified and alert on thresholds — medium
- [ ] **SEC-5.6** [intent] A log retention period and access policy are defined and documented — medium
- [ ] **SEC-5.7** [intent] An incident response process exists and has been exercised using logs only — medium

## How to verify
- **Code:** read the logging layer and what each call site records; check storage permissions.
- **Intent:** "Pick one past request: can you reconstruct what happened from logs? How long are logs kept, and who can read them?"
