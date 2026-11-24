# Phase 2: Prompt Injection and Output Handling

## What you are checking
Resistance to direct injection (user input overriding instructions) and indirect injection (instructions hidden in retrieved documents, emails, web pages, tool results), including evasion with Unicode homoglyphs, invisible characters and encodings.

## Checklist
- [ ] **SEC-2.1** [code] User input is Unicode-normalized before any filter or policy check — medium
- [ ] **SEC-2.2** [code] Untrusted content (retrieved docs, tool results, emails) is separated from instructions and treated as data — high
- [ ] **SEC-2.3** [code] The system prompt contains no secrets and its disclosure would not compromise security — high
- [ ] **SEC-2.4** [code] Filters are not bypassable by invisible characters, homoglyphs or encoded payloads (base64, hex) — medium
- [ ] **SEC-2.5** [code] Model output is validated or constrained (schema, allowlist) before it reaches downstream systems or users — high
- [ ] **SEC-2.6** [code] Output cannot exfiltrate data through rendered links, images or markdown to external URLs — high
- [ ] **SEC-2.7** [both] Suspicious inputs are flagged and reviewed, not silently passed — medium
- [ ] **SEC-2.8** [intent] Injection testing is performed before major releases — medium

## How to verify
- **Code:** find where prompts are built and where every external data channel enters; check normalization and filter order; check output parsing and rendering.
- **Intent:** "What untrusted content reaches the model? Is injection tested before release, and how?"
