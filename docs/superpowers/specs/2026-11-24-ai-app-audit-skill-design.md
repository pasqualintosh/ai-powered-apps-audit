# Design: skill `ai-app-audit` (v0.0.1)

## Intento
Una skill per Claude che audita app basate su AI su due piani: **cybersecurity** dell'implementazione e **conformità all'AI Act (Reg. UE 2024/1689)**. Parte dal repo `ai-agent-security-audit` (MIT, Don De Jesus), ripulito del superfluo. L'audit combina lettura del codice e intervista allo sviluppatore, perché parte dei requisiti dipende dalle intenzioni.

## Obiettivi
- Un `SKILL.md` che guida Claude dall'inizio al report.
- Checklist verificabili, ciascuna voce marcata `[codice]`, `[intento]` o `[entrambi]`.
- Classificazione AI Act (ruolo + livello di rischio) prima di scegliere le checklist.
- Report con finding, severità, evidenza e riferimento (fase o articolo).

## Non-obiettivi (v0.0.1)
- Nessun codice di esempio, nessuna libreria o tool consigliato.
- Nessuna suite di test avversariali (da ricostruire in una versione successiva).
- Nessuna consulenza legale: l'output è un pre-audit, non una certificazione.
- Nessun formato plugin (solo cartella skill copiabile).

## Anti-obiettivi
- Classificare AI Act solo dal codice, senza scopo dichiarato.
- Checklist generiche non verificabili.
- Mantenere marketing, statistiche o promozione dell'autore originale.

## Approcci considerati
A) intervista poi codice; B) codice poi domande; **C) ibrido con voci marcate — scelto**. Motivo: lo scopo previsto determina la classificazione AI Act, e il confronto intento/codice è il valore principale.

## Struttura
```
SKILL.md                 flusso e regole
security/01..05-*.md     5 fasi, ridotte a: cosa verificare, come verificarlo, severità
security/agents.md       sezione specifica agenti (approvazioni, tool, memoria)
ai-act/classification.md ruolo (provider/deployer), pratiche vietate, alto rischio, trasparenza, GPAI
ai-act/obligations.md    obbligazioni per livello, con articoli
references/frameworks.md OWASP LLM, MITRE ATLAS, NIST AI RMF, testi AI Act
report-template.md
README.md                inglese (principale): cosa è, stato del progetto, installazione, roadmap
README.it.md             traduzione italiana, stessi contenuti e stesso stato
CLAUDE.md                istruzioni per Claude nel repo: scopo, struttura, convenzioni, stato
LICENSE                  credito all'autore originale
```
Rimossi: `examples/`, `adversarial-tests/`, `CONTRIBUTING.md` (da rifare), sezioni "Tools", statistiche, promo.

## Flusso di SKILL.md
1. **Intervista breve (~6 domande)**: scopo previsto, utenti e settore, ruolo (provider/deployer), dati trattati, grado di autonomia, modello usato.
2. **Classificazione AI Act** con `ai-act/classification.md`; dichiara l'esito e le assunzioni.
3. **Scansione del codice** per le voci `[codice]` e `[entrambi]` delle fasi di sicurezza pertinenti e degli obblighi del livello assegnato.
4. **Domande mirate** solo per le voci `[intento]` e per i dubbi emersi.
5. **Divergenze** intento/codice riportate come finding.
6. **Report** da `report-template.md`.

## Scelte mie (da correggere se non vanno)
- Le fasi di sicurezza sono riscritte per app AI in generale, non solo agenti; l'agente ha un file dedicato.
- Lingue (decise dall'utente): `README.md` in inglese (principale) + `README.it.md` in italiano; `SKILL.md` e tutti i file della skill solo in inglese; `CLAUDE.md` in inglese. Il report è scritto nella lingua dell'utente che lancia la skill.
- Severità: critica / alta / media / bassa, come nel repo originale.
- Date di applicazione dell'AI Act non hardcodate: la skill chiede di verificarle sul testo ufficiale.

## Stato del progetto
Versione **0.0.1 (fase 0)**: scheletro. Contiene struttura, flusso di `SKILL.md`, checklist ridotte derivate dal repo originale e checklist AI Act iniziali. Non ancora validata su app reali, nessun test avversariale, checklist AI Act da revisionare giuridicamente. Entrambi i README (e `CLAUDE.md`) riportano questo stato e una roadmap breve: test avversariali, validazione su app reali, formato plugin, revisione AI Act.

## Lasciato a chi costruisce
Formulazione esatta delle domande, soglie di severità per voce, dettagli delle checklist per articolo.
