# Phase 3: Data, Retrieval and Boundary Validation

## What you are checking
Integrity of stored context (vector stores, history, memory, caches) and validation at every internal trust boundary: structured queries, file access, retrieval pipelines, tool parameters.

## Checklist
- [ ] **SEC-3.1** [code] Every path by which external data enters context or storage is identified and validated — high
- [ ] **SEC-3.2** [code] Model-generated queries are parameterized or constrained; no raw SQL/NoSQL/shell built from model output — critical
- [ ] **SEC-3.3** [code] File paths from the model or user are validated against an allowlist (no traversal) — high
- [ ] **SEC-3.4** [both] Indexed/retrieved documents come from trusted sources; ingestion is access-controlled — high
- [ ] **SEC-3.5** [code] Retrieval enforces the requesting user's permissions on documents — critical
- [ ] **SEC-3.6** [code] Errors do not leak stack traces, paths, prompts or configuration to users — medium
- [ ] **SEC-3.7** [code] Parameters of every function the model can call have explicit types and ranges — high
- [ ] **SEC-3.8** [intent] Who can add or change documents, prompts and stored memory is defined and limited — medium

## How to verify
- **Code:** read the data-access layer, ingestion pipeline, retriever and error handlers.
- **Intent:** "Who can write to the knowledge base? Where does indexed content originate?"
