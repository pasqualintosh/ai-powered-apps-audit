# Agents: Autonomy, Tools and Memory

**Skip this file entirely if the app has no tool use or autonomous actions.** Report it as "not applicable", not as a pass.

## What you are checking
Controls specific to systems where the model can act: call tools, change external state, keep memory, or chain steps.

## Checklist
- [ ] **AGT-1** [both] Every tool/function is inventoried and classified as read-only or state-changing — high
- [ ] **AGT-2** [code] Every state-changing action requires human approval enforced at the execution layer, not only in the prompt — critical
- [ ] **AGT-3** [code] The agent cannot approve its own actions; approval comes from a human principal — critical
- [ ] **AGT-4** [code] Pending approvals expire and expiry means rejection — high
- [ ] **AGT-5** [code] Approval requests show action, target, parameters and reason; batch actions need explicit batch approval — medium
- [ ] **AGT-6** [code] Every approval decision is logged (who, when, what) — high
- [ ] **AGT-7** [both] Tools run with least privilege; the agent has no more access than its task needs — high
- [ ] **AGT-8** [code] Reversible actions have a rollback path — medium
- [ ] **AGT-9** [code] Memory segments holding core instructions are write-protected; updates require a source-authority check — high
- [ ] **AGT-10** [code] Chained tool calls cannot bypass approval or permission checks — critical
- [ ] **AGT-11** [intent] Limits on autonomy (steps, spend, time) are defined — medium

## How to verify
- **Code:** read tool definitions, the dispatcher, and the approval path; confirm approval is enforced where the tool executes.
- **Intent:** "What can the agent do without a human? What is the worst action it can take?"
