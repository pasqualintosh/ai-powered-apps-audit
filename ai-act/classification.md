# AI Act Classification

Regulation (EU) 2024/1689. This is a pre-audit aid, not legal advice. **Do not state application dates from memory:** verify entry-into-application dates for each obligation on the official text (EUR-Lex) before reporting, and say in the report that you did or did not.

## Rule for uncertainty
If two outcomes are plausible, assign the **stricter** one and record the assumption and the question that would settle it.

## Decision sequence
Work through in order and record the answer to each step in the report.

1. **In scope? (Art. 2)** Is the system placed on the EU market, put into service in the EU, or is its output used in the EU? Is it a purely personal, non-professional use, or purely scientific research, or military? If out of scope, say so and stop the AI Act part.
2. **Role (Art. 3):** `provider` (develops or has developed an AI system and places it on the market or puts it into service under its own name), `deployer` (uses an AI system under its authority, professionally), `both`, or `other` (importer, distributor, authorized representative). An organization that builds an app on a third-party model and offers it to users is normally the provider of that app. Using an AI tool internally only is a deployer. Substantially modifying or rebranding a high-risk system can make a deployer a provider (Art. 25).
3. **Prohibited practices? (Art. 5)** Check the intended purpose against each prohibited practice (e.g. manipulative or exploitative techniques causing harm, social scoring, certain biometric and emotion-inference uses). Any match → level `prohibited`: report as critical and stop recommending compliance steps; recommend legal advice.
4. **High-risk? (Art. 6)** (a) Is the system a safety component of, or itself, a product under the Union harmonisation legislation in Annex I, requiring third-party conformity assessment? (b) Is the intended purpose in an Annex III area (e.g. biometrics, critical infrastructure, education, employment and worker management, access to essential services such as credit or insurance, law enforcement, migration, justice and democratic processes)? If Annex III applies, check the Art. 6(3) exceptions (narrow procedural task, improving a prior human activity, detecting patterns without replacing human assessment, preparatory task) and **record why an exception does or does not hold**; profiling of natural persons is always high-risk. → level `high-risk`.
5. **Transparency (Art. 50)?** Does the system interact directly with people, generate synthetic audio/image/video/text, perform emotion recognition or biometric categorisation, or produce deepfakes? → level `transparency` (also applies on top of `high-risk`).
6. **GPAI (Arts. 51-55)?** Only if the user trains, fine-tunes at scale, or places on the market a general-purpose AI model itself. Using a third-party GPAI model through an API does not make the user a GPAI provider. Set flag `gpai`.
7. Otherwise → level `minimal`. AI literacy (Art. 4) still applies to providers and deployers.

## Output vocabulary (use exactly)
- role: `provider | deployer | both | other`
- level: `prohibited | high-risk | transparency | minimal`
- flag: `gpai` (yes/no)
- assumptions: list, each with the question that would settle it

## Intent questions this step depends on
Intended purpose (the developer's stated purpose is what counts, not only what the code does), who is affected, the sector, whether outputs support or replace human decisions about people, and whether the user places the system on the market or only uses it internally.
