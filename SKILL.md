---
name: ai-app-audit
description: Audit an AI-powered application for cybersecurity weaknesses and EU AI Act (Reg. 2024/1689) compliance by combining a short developer interview with a code review. Use when the user asks to audit, review or pre-assess the security or AI Act compliance of an app that uses LLMs, RAG, agents or other AI components.
---

# AI App Audit

Pre-audit of an AI-powered app on two axes: **security** of the implementation and **AI Act** compliance. It combines what the developer says (intent) with what the code does. This is not legal advice and not a certification; never claim either.

Files: `security/01..05-*.md`, `security/agents.md`, `ai-act/classification.md`, `ai-act/obligations.md`, `report-template.md`, `references/frameworks.md`.

## How items work
Every checklist item has an ID, a tag and a severity: `**ID** [code|intent|both] statement — severity`.
- `[code]`: verify by reading the repo.
- `[intent]`: ask the developer; the answer is the evidence.
- `[both]`: read the code, and ask only if the code is inconclusive; compare the two.

## Flow

1. **Interview (about 6 questions, ask them together).** Intended purpose; users and sector (who is affected by outputs); provider or deployer role (do they offer the app to others, or use it internally?); data processed (personal, special-category, confidential); degree of autonomy and tools (can it act, or only answer?); model used and where it is hosted. Ask for the path of the code. Accept "I don't know" and record it.
2. **Classify under the AI Act** following `ai-act/classification.md`. State role, level, gpai flag and assumptions. If two levels are plausible, take the stricter and say so.
3. **Scan the code** for every `[code]` and `[both]` item in `security/01..05-*.md`, in `security/agents.md` (only if the app has tools or autonomous actions; otherwise report "not applicable"), and in the `ai-act/obligations.md` sections that match the classification. Cite `file:line` as evidence. Do not mark an item as passed without evidence.
4. **Ask targeted questions** only for `[intent]` items and for points where the code was inconclusive. Ask them in one batch.
5. **Check divergences.** Compare what the developer said with what the code does (e.g. "no automated decisions" but output is written directly to a database). Each divergence is a finding, never silently resolved.
6. **Write the report** using `report-template.md`, in the language the user wrote in.

## Rules
- Large repos: do not try to read everything. Sample the entry points: prompt construction, tool definitions, auth, data access, logging, output rendering. State coverage in the report.
- Mark items you could not verify as `not verified`, with why. They are not passes.
- Items that do not apply (e.g. no memory, no trust scoring) are `not applicable`, with a one-line reason.
- Do not state AI Act application dates from memory; tell the user to confirm them on the official text.
- Do not run attacks against live systems or third-party services. Read code; propose tests the user can run themselves.
- Tell the user at the end that the AI Act findings need legal review before being relied on.
