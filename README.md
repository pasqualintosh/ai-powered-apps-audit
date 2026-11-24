# ai-app-audit

🇬🇧 English · [🇮🇹 Italiano](README.it.md)

A [Claude](https://claude.com/claude-code) skill that audits **AI-powered apps** on two axes:

- **Cybersecurity** of the implementation (access, prompt injection, data and retrieval boundaries, abuse, logging, and agent-specific controls).
- **EU AI Act** compliance (Regulation (EU) 2024/1689): role and risk classification, then the obligations that follow.

It combines a short **interview with the developer** (intent matters for the AI Act) with a **code review**, and flags every place where what was said differs from what the code does.

> Pre-audit tool. It is not legal advice and not a certification.

## Project status: v0.0.1 (phase 0)

This is the skeleton. What exists and what does not:

| Area | State |
|------|-------|
| Skill flow (`SKILL.md`) | Written, not yet tested on real apps |
| Security checklists (5 phases + agents) | Derived from the original project and rewritten for AI apps; first pass |
| AI Act classification and obligations | First pass; **needs legal review** |
| Adversarial tests | Not included; to be rebuilt |
| Report template | Written |
| Plugin packaging | Not done |

### Roadmap
1. Validate the skill on real apps and fix the flow.
2. Rebuild adversarial test cases.
3. Legal review of the AI Act checklists.
4. Package as a Claude Code plugin.

## How it works
1. Interview (about 6 questions): purpose, users and sector, role, data, autonomy, model.
2. Classify under the AI Act (role, risk level, general-purpose model flag).
3. Scan the code against the tagged checklists.
4. Ask targeted questions for items only the developer can answer.
5. Report divergences between intent and code.
6. Produce the report.

Each checklist item is tagged `[code]`, `[intent]` or `[both]` and has a severity (`critical | high | medium | low`).

## Repository layout
```
SKILL.md                 audit flow and rules
security/                5 security phases + agents.md
ai-act/                  classification.md, obligations.md
references/              frameworks and official texts
report-template.md       report format
CLAUDE.md                instructions for working on this repo
```

## Install
Copy this folder to `~/.claude/skills/ai-app-audit`, then ask Claude to audit an AI app.

## Credits
Derived from `ai-agent-security-audit` by Don De Jesus (MIT). The security phases started from that project; the marketing material, examples, tool lists and adversarial tests were removed, and the AI Act part is new.

## License
MIT. See [LICENSE](LICENSE).
