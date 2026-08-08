# AXIOS-AI — Setup

Repository di setup e riproduzione per **AXIOS-AI**, l'assistente intelligente per la gestione quotidiana della farmacia.

## Contenuto del repository

| Cartella / File | Contenuto |
|---|---|
| `CONFIGURAZIONE.md` | Testo da incollare nella chat di pi: installa il motore NL-query di WrenAI sul database del progetto e verifica le estensioni attive |
| `COME-USARE-AXIOS.md` | Consigli d'uso facoltativi e personalizzabili, adatti anche a chi ha poca dimestichezza con l'AI |
| `GUIDA_INSTALLAZIONE-AGENT_LLM.md` | Installazione dell'agent, configurazione del provider LLM e importazione del database |
| `winfarm/` | Profilo Winfarm (Firebird) per WrenAI: istruzioni, query e guida di riferimento. **Senza database** — i file database (*.phs, *.fdb, ecc.) sono esclusi dal `.gitignore`. Credenziali reali in `winfarm/.env` (modello: `winfarm/.env.example`) |

## ⚠️ Avvertenze

- **Mai** committare il database (file `arc2000.phs`, ~11 GB) né le credenziali reali (`.env`).
- Il ruolo di provider resta allo sviluppatore; il deployer dell'agente è l'utente finale (conformità AI Act).
- Il sito web vive nel repo `axios-ai` (https://github.com/AXIOS-AI/axios-ai), non qui.

## 📌 Indice

* [CONFIGURAZIONE.md](CONFIGURAZIONE.md) — testo da incollare nella chat di pi
* [COME-USARE-AXIOS.md](COME-USARE-AXIOS.md) — modalità d'uso consigliata
* [GUIDA_INSTALLAZIONE-AGENT_LLM.md](GUIDA_INSTALLAZIONE-AGENT_LLM.md) — installazione completa
* [winfarm/WINFARM_GUIDA_RIFERIMENTO.md](winfarm/WINFARM_GUIDA_RIFERIMENTO.md) — riferimento database Winfarm
