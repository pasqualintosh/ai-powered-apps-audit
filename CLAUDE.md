# CLAUDE.md

## Purpose
`ai-app-audit` is a Claude skill that audits AI-powered apps for cybersecurity and EU AI Act (Reg. 2024/1689) compliance, combining a developer interview with a code review. Entry point: `SKILL.md`.

## Status
**v0.0.1 (phase 0): skeleton.** Not validated on real apps; no adversarial tests; AI Act checklists need legal review. Keep this status in sync in `README.md`, `README.it.md` and here when it changes.

Roadmap: validate on real apps → rebuild adversarial tests → legal review of AI Act → plugin packaging.

## Layout
- `SKILL.md`: flow and rules (English only)
- `security/01..05-*.md`, `security/agents.md`: security checklists (`SEC-*`, `AGT-*`)
- `ai-act/classification.md`, `ai-act/obligations.md`: classification and obligations (`AIA-*`)
- `references/frameworks.md`, `report-template.md`
- `docs/superpowers/`: design spec (`specs/`) and implementation plan (`plans/`), written in Italian/English during creation

## Conventions
- Checklist item format: `- [ ] **<ID>** [code|intent|both] <statement> — <critical|high|medium|low>`.
- Skill files, `CLAUDE.md`: English only. `README.md` is the primary README; `README.it.md` must mirror it.
- Do not hardcode AI Act application dates; the skill must tell users to verify them on the official text.
- No code examples, no tool/library recommendations, no statistics or promotion in v0.0.1.
- Items needing legal confirmation are marked *needs legal review*.
- Keep `LICENSE` (MIT) and the credit to the original author (Don De Jesus, `ai-agent-security-audit`).

## Checks before finishing a change
- Every checklist line matches the item format (grep in the plan, Task 2–3).
- No tool names or promo text reintroduced.
- READMEs still agree on status and layout.
