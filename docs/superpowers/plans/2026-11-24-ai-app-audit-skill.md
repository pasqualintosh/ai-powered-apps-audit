# ai-app-audit Skill v0.0.1 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Turn the forked `ai-agent-security-audit` repo into a Claude skill (`ai-app-audit`) that audits AI apps for cybersecurity and EU AI Act compliance, version 0.0.1.

**Architecture:** Markdown-only skill. `SKILL.md` drives a 6-step flow (interview → AI Act classification → code scan → targeted questions → divergences → report). Checklist items are tagged `[code]`, `[intent]` or `[both]` so Claude knows what to read and what to ask.

**Tech Stack:** Markdown only. Verification via `grep`/`find` shell checks (no code, no tests framework).

**Spec:** `docs/superpowers/specs/2026-11-24-ai-app-audit-skill-design.md`

## Global Constraints

- `SKILL.md`, `security/`, `ai-act/`, `references/`, `report-template.md`, `CLAUDE.md`: English only.
- `README.md` English (primary); `README.it.md` Italian, same content and same status.
- Project status everywhere: **v0.0.1 (phase 0)**.
- No code examples, no recommended libraries/tools, no adversarial tests, no statistics, no author promotion (Substack, newsletter, LinkedIn, quiz).
- Keep MIT `LICENSE` and credit original author Don De Jesus (repo `ai-agent-security-audit`) in both READMEs.
- Severity scale: `critical | high | medium | low`.
- AI Act application dates are NOT hardcoded; the skill tells Claude to verify them on the official text (Reg. EU 2024/1689).
- Not legal advice: output is a pre-audit, not a certification.

## Checklist item format (shared interface for Tasks 2–4)

```
- [ ] **<ID>** [code|intent|both] <verifiable statement> — <severity>
```
IDs: `SEC-<phase>.<n>` (security, phase 1–5), `AGT-<n>` (agents), `AIA-<n>` (AI Act). Each file starts with a short "What you are checking" paragraph, then the items, then "How to verify" (code: what to grep/read; intent: the question to ask).

## Review Focus

- App with no agent/tools: agent-only items must be skipped, not failed (SKILL.md must say so).
- Classification uncertain between two AI Act levels: skill must pick the stricter and state the assumption.
- Developer answers contradict the code: must become a finding, not be silently resolved.
- Repo too large to read fully: skill must say to sample entry points (prompts, tool defs, auth, logging) and declare coverage in the report.
- User not the legal provider/deployer (e.g. internal tool, open-source): classification must still produce an outcome with stated assumption.

---

### Task 1: Clean up and restructure the repo

**Files:**
- Delete: `examples/`, `adversarial-tests/`, `CONTRIBUTING.md`, `.DS_Store`
- Move: `phases/0N-*.md` → `security/0N-*.md` (same filenames)
- Create dirs: `ai-act/`

**Interfaces:**
- Produces: `security/01-stop-the-bleeding.md`, `security/02-prompt-injection.md`, `security/03-defense-in-depth.md`, `security/04-trust-hardening.md`, `security/05-observability.md` (rewritten in Task 2).

- [ ] **Step 1: Delete removed items and move phases**
  Run: `rm -rf examples adversarial-tests CONTRIBUTING.md .DS_Store && mv phases security && mkdir ai-act`
- [ ] **Step 2: Verify**
  Run: `ls` → expect `LICENSE README.md ai-act docs references security`; `ls security` → 5 files.

### Task 2: Rewrite security phases for AI apps

**Files:**
- Modify: `security/01..05-*.md` (rewrite in place)
- Create: `security/agents.md`

**Interfaces:**
- Consumes: item format above.
- Produces: IDs `SEC-1.n`…`SEC-5.n`, `AGT-n` referenced by `report-template.md` and `SKILL.md`.

- [ ] **Step 1:** For each phase file, keep the original checklist content but: reword for AI apps in general (LLM calls, RAG, tools, user input), drop "Why it matters" statistics, "Example vulnerability", and "Tools" sections; convert every item to the shared format with a tag and severity; add "How to verify" with code-reading targets and intent questions.
- [ ] **Step 2:** Move agent-specific items (approval gates on state-changing actions, tool least-privilege, memory poisoning, trust/cooling logic, self-approval) into `security/agents.md` as `AGT-n`; leave in phases 1–5 only items valid for any AI app (e.g. SEC-1 = access control and secrets for model/API keys, SEC-2 = prompt injection and output handling, SEC-3 = data/RAG/SQL boundaries, SEC-4 = trust and rate/abuse controls, SEC-5 = logging and forensics). Start `agents.md` with: "Skip this file entirely if the app has no tool use or autonomous actions."
- [ ] **Step 3: Verify**
  Run: `grep -rLE '\[(code|intent|both)\]' security/` → expect no output (every file has tags).
  Run: `grep -rniE 'substack|garak|pyrit|langfuse|langsmith|helicone|clickhouse|88%|teleport|^## Tools|^## Example' security/` → expect no output.
  Run: `grep -rE '^\- \[ \]' security/ | grep -vE '\*\*(SEC|AGT)-[0-9.]+\*\* \[(code|intent|both)\].* — (critical|high|medium|low)$'` → expect no output.

### Task 3: AI Act files

**Files:**
- Create: `ai-act/classification.md`, `ai-act/obligations.md`

**Interfaces:**
- Produces: classification outcome vocabulary used by `SKILL.md`: role ∈ {`provider`, `deployer`, `both`, `other`}; level ∈ {`prohibited`, `high-risk`, `transparency`, `minimal`}; plus flag `gpai` (general-purpose AI model obligations). Obligation IDs `AIA-<n>` with article references.

- [ ] **Step 1: `classification.md`** — decision sequence: (1) in scope of Reg. EU 2024/1689? (Art. 2); (2) role (Art. 3: provider, deployer, importer, distributor); (3) prohibited practices (Art. 5); (4) high-risk (Art. 6 + Annex I and III); (5) transparency obligations (Art. 50); (6) GPAI (Arts. 51–55) if the user builds/fine-tunes a model; else minimal. Rule: if uncertain between two levels, assign the stricter and record the assumption. Include the instruction to verify entry-into-application dates on the official text.
- [ ] **Step 2: `obligations.md`** — per level, items in the shared format with article reference in the statement, tags `[code]/[intent]/[both]`, e.g. high-risk: risk management (Art. 9), data governance (Art. 10), technical documentation (Art. 11), logging (Art. 12), transparency to deployers (Art. 13), human oversight (Art. 14), accuracy/robustness/cybersecurity (Art. 15), plus deployer duties (Art. 26); transparency level: Art. 50 disclosure items; also AI literacy (Art. 4) for all. Only include articles you can state accurately; mark any uncertain item `needs legal review`.
- [ ] **Step 3: Verify**
  Run: `grep -cE '^\- \[ \] \*\*AIA-' ai-act/obligations.md` → expect ≥ 15.
  Run: `grep -E '^\- \[ \]' ai-act/obligations.md | grep -vE 'AIA-[0-9]+\*\* \[(code|intent|both)\].* — (critical|high|medium|low)$'` → no output.
  Run: `grep -nE '20(2[4-9]|3[0-9])' ai-act/*.md` → no hardcoded application dates (output must not contain "applies from"/dates).

### Task 4: SKILL.md, report template, references

**Files:**
- Create: `SKILL.md`, `report-template.md`
- Modify: `references/frameworks.md` (trim)

**Interfaces:**
- Consumes: IDs and vocabularies from Tasks 2–3.

- [ ] **Step 1: `SKILL.md`** — YAML frontmatter `name: ai-app-audit`, `description:` (trigger: user asks to audit/review security or AI Act compliance of an AI-powered app). Body: the 6-step flow from the spec; the ~6 interview questions (intended purpose, users and sector, provider/deployer role, data processed, degree of autonomy/tools, model used and hosting); rules: skip `agents.md` when no tools/autonomy; pick stricter level when uncertain and state assumptions; divergence between intent and code is a finding; for large repos sample entry points (prompts, tool definitions, auth, logging, data stores) and declare coverage; never claim certification; report language = user's language.
- [ ] **Step 2: `report-template.md`** — sections: scope and coverage, AI Act classification (role, level, gpai, assumptions), findings table (ID, severity, tag, evidence file:line or quoted answer, reference, recommendation), divergences, items not verified, summary by severity.
- [ ] **Step 3: `references/frameworks.md`** — keep OWASP LLM Top 10, MITRE ATLAS, NIST AI RMF, SAIF; delete "Testing Tools" and anything tool-related; add AI Act official text (EUR-Lex Reg. 2024/1689) and the AI Office page.
- [ ] **Step 4: Verify**
  Run: `head -5 SKILL.md` → frontmatter with `name: ai-app-audit`.
  Run: `grep -nE 'security/0|security/agents|ai-act/classification|ai-act/obligations|report-template' SKILL.md` → each of the 5 paths + agents.md appears.
  Run: `grep -niE 'garak|pyrit|langfuse' references/ SKILL.md report-template.md -r` → no output.

### Task 5: README (EN + IT), CLAUDE.md, LICENSE credit

**Files:**
- Rewrite: `README.md`
- Create: `README.it.md`, `CLAUDE.md`
- Check: `LICENSE`

- [ ] **Step 1: `README.md` (English)** — title, link to `README.it.md`, what it is, status block ("v0.0.1 — phase 0: skeleton; not validated on real apps; no adversarial tests; AI Act checklists need legal review; not legal advice"), how the audit works (the 6 steps), repo structure, install (copy folder into `~/.claude/skills/ai-app-audit`), roadmap (adversarial tests, validation on real apps, plugin format, legal review of AI Act checklists), credits (derived from `ai-agent-security-audit` by Don De Jesus, MIT), license.
- [ ] **Step 2: `README.it.md`** — same sections and same status block, translated; link back to `README.md`.
- [ ] **Step 3: `CLAUDE.md` (English)** — purpose, repo map, conventions (item format, tags, severity, English-only skill files, no hardcoded AI Act dates, no tool recommendations in v0.0.1), current status v0.0.1 phase 0 and roadmap, and "READMEs must stay in sync".
- [ ] **Step 4: `LICENSE`** — confirm MIT text is kept and original copyright line unchanged.
- [ ] **Step 5: Verify**
  Run: `grep -c '0.0.1' README.md README.it.md CLAUDE.md` → each ≥ 1.
  Run: `grep -liE 'substack|doneyli|linkedin' README*.md CLAUDE.md` → no output.
  Run: `grep -l 'Don De Jesus' README.md README.it.md LICENSE` → all three listed.

### Task 6: Final verification

- [ ] **Step 1:** `find . -type f -not -path './docs/*' | sort` → exactly: `./CLAUDE.md ./LICENSE ./README.it.md ./README.md ./SKILL.md ./ai-act/classification.md ./ai-act/obligations.md ./references/frameworks.md ./report-template.md ./security/01…05 ./security/agents.md`.
- [ ] **Step 2:** `grep -rn 'TODO\|TBD' . --include='*.md' --exclude-dir=docs` → no output.
- [ ] **Step 3:** Walk every Review Focus line against `SKILL.md`; add any missing rule.
- [ ] **Step 4:** Report to the user; offer `git init` + first commit (not done unprompted).
