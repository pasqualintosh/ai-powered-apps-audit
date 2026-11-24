# AI Act Obligations Checklist

Regulation (EU) 2024/1689. Use the items for the level and role assigned in `classification.md`. Items marked *needs legal review* are a reading of the text that a lawyer should confirm. Verify application dates on the official text; do not rely on memory.

## All systems (provider and deployer)
- [ ] **AIA-1** [intent] Measures ensure a sufficient level of AI literacy of staff operating or using the system (Art. 4) — medium
- [ ] **AIA-2** [intent] The intended purpose is documented and checked against the prohibited practices (Art. 5) — critical

## Transparency level (Art. 50)
- [ ] **AIA-3** [both] Users are told they are interacting with an AI system, unless obvious from context (Art. 50(1), provider) — high
- [ ] **AIA-4** [code] Synthetic audio, image, video or text outputs are marked in a machine-readable format and detectable as artificially generated, where technically feasible (Art. 50(2), provider) — high
- [ ] **AIA-5** [both] People exposed to emotion recognition or biometric categorisation are informed (Art. 50(3), deployer) — high
- [ ] **AIA-6** [both] Deepfakes, and AI-generated text published to inform the public on matters of public interest, are disclosed as artificially generated or manipulated (Art. 50(4), deployer); exceptions for human-reviewed editorial text — *needs legal review* — medium

## High-risk: provider (Chapter III, Section 2 and Art. 16)
- [ ] **AIA-7** [both] A risk management system runs through the lifecycle: risks identified, evaluated, mitigated, residual risk documented (Art. 9) — critical
- [ ] **AIA-8** [both] Training, validation and testing data meet quality and governance criteria: provenance, relevance, representativeness, bias examination (Art. 10) — high
- [ ] **AIA-9** [intent] Technical documentation is prepared before market placement and kept up to date (Art. 11, Annex IV) — high
- [ ] **AIA-10** [code] The system automatically records events (logs) over its lifetime sufficient for traceability (Art. 12) — high
- [ ] **AIA-11** [intent] Instructions for use give deployers the information to interpret and use outputs correctly: purpose, accuracy, limits, oversight measures (Art. 13) — high
- [ ] **AIA-12** [both] The system is designed so natural persons can effectively oversee it: understand outputs, override or stop it, and avoid automation bias (Art. 14) — critical
- [ ] **AIA-13** [both] Accuracy, robustness and cybersecurity are appropriate and declared, including resilience against attacks such as data poisoning, adversarial inputs and model manipulation (Art. 15) — critical
- [ ] **AIA-14** [intent] A quality management system is in place (Art. 17) — high
- [ ] **AIA-15** [intent] Conformity assessment, EU declaration of conformity, CE marking and registration in the EU database are planned or done (Arts. 16, 43, 47, 48, 49) — high
- [ ] **AIA-16** [intent] Post-market monitoring and serious-incident reporting processes exist (Arts. 72, 73) — high

## High-risk: deployer (Art. 26 and related)
- [ ] **AIA-17** [intent] The system is used according to the provider's instructions and input data under the deployer's control is relevant and representative (Art. 26) — high
- [ ] **AIA-18** [both] Human oversight is assigned to people with the necessary competence, training and authority (Art. 26) — high
- [ ] **AIA-19** [both] Logs under the deployer's control are kept for an appropriate period, at least six months unless other law requires otherwise (Art. 26) — medium
- [ ] **AIA-20** [intent] Workers' representatives and affected workers are informed before a high-risk system is used in the workplace (Art. 26) — medium
- [ ] **AIA-21** [intent] Affected persons are informed when a high-risk system makes or assists decisions about them (Art. 26) and can obtain an explanation of decisions with legal or similarly significant effects (Art. 86) — *needs legal review* — high
- [ ] **AIA-22** [intent] Where required (e.g. public bodies, credit and insurance uses), a fundamental rights impact assessment was performed (Art. 27) — *needs legal review* — high

## GPAI flag (Arts. 51-55; only if the user provides a general-purpose model)
- [ ] **AIA-23** [intent] Technical documentation and information for downstream providers are prepared (Art. 53) — high
- [ ] **AIA-24** [intent] A copyright compliance policy and a public summary of training content exist (Art. 53) — high
- [ ] **AIA-25** [intent] For models with systemic risk: evaluation, adversarial testing, incident reporting and cybersecurity protections (Art. 55) — *needs legal review* — high

## How to verify
- **Code:** logging layer (Art. 12), output labelling and disclosure UI (Art. 50), override/stop controls (Art. 14), validation, security controls from `security/` that evidence Art. 15.
- **Intent:** ask for the documents named in each item; absence of a document is a finding. Where the code contradicts a declared answer (e.g. "a human always decides" but the code applies the model's output automatically), report a divergence.
- A `security/` finding that undermines Art. 15 (e.g. unmitigated prompt injection in a high-risk system) should be cross-referenced to AIA-13.
