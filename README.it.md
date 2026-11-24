# ai-app-audit

[🇬🇧 English](README.md) · 🇮🇹 Italiano

Una skill per [Claude](https://claude.com/claude-code) che esegue l'audit di **app basate su AI** su due assi:

- **Cybersecurity** dell'implementazione (accessi, prompt injection, confini dei dati e del retrieval, abusi, logging e controlli specifici per gli agenti).
- **Conformità all'AI Act** (Regolamento (UE) 2024/1689): classificazione di ruolo e rischio, poi gli obblighi che ne derivano.

Combina una breve **intervista allo sviluppatore** (l'intento conta per l'AI Act) con una **revisione del codice**, e segnala ogni punto in cui quanto dichiarato differisce da quanto fa il codice.

> Strumento di pre-audit. Non è consulenza legale né una certificazione.

## Stato del progetto: v0.0.1 (fase 0)

Questo è lo scheletro. Cosa esiste e cosa no:

| Area | Stato |
|------|-------|
| Flusso della skill (`SKILL.md`) | Scritto, non ancora provato su app reali |
| Checklist di sicurezza (5 fasi + agenti) | Derivate dal progetto originale e riscritte per app AI; prima versione |
| Classificazione e obblighi AI Act | Prima versione; **richiede revisione legale** |
| Test avversariali | Non inclusi; da ricostruire |
| Template del report | Scritto |
| Packaging come plugin | Non fatto |

### Roadmap
1. Validare la skill su app reali e correggere il flusso.
2. Ricostruire i casi di test avversariali.
3. Revisione legale delle checklist AI Act.
4. Pacchettizzare come plugin di Claude Code.

## Come funziona
1. Intervista (circa 6 domande): scopo, utenti e settore, ruolo, dati, autonomia, modello.
2. Classificazione AI Act (ruolo, livello di rischio, flag modello per uso generale).
3. Scansione del codice con le checklist marcate.
4. Domande mirate per le voci a cui può rispondere solo lo sviluppatore.
5. Segnalazione delle divergenze tra intento e codice.
6. Produzione del report.

Ogni voce delle checklist è marcata `[code]`, `[intent]` o `[both]` e ha una severità (`critical | high | medium | low`).

## Struttura del repository
```
SKILL.md                 flusso e regole dell'audit
security/                5 fasi di sicurezza + agents.md
ai-act/                  classification.md, obligations.md
references/              framework e testi ufficiali
report-template.md       formato del report
CLAUDE.md                istruzioni per lavorare su questo repo
```

## Installazione
Copia questa cartella in `~/.claude/skills/ai-app-audit`, poi chiedi a Claude di fare l'audit di un'app AI.

## Crediti
Derivato da `ai-agent-security-audit` di Don De Jesus (MIT). Le fasi di sicurezza partono da quel progetto; materiale promozionale, esempi, elenchi di strumenti e test avversariali sono stati rimossi, e la parte AI Act è nuova.

## Licenza
MIT. Vedi [LICENSE](LICENSE).
