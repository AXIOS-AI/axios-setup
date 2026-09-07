# CONFIGURAZIONE — da incollare in pi

> Copia e incolla tutto il testo qui sotto nella chat di pi.
> pi eseguirà la configurazione passo-passo spiegandoti ogni passaggio.

---

Configura il motore NL-query per interrogare il database in linguaggio naturale, scegliendo tu la soluzione più adatta tra:
- **WrenAI** (progetto completo, non solo il motore NL-query — include anche una piattaforma per generare grafici e dashboard moderni a partire dai dati) — https://github.com/Canner/WrenAI. Collega la parte LLM di WrenAI all'agent stesso, in modo che sia l'agent a gestire il ragionamento invece di usare un provider LLM separato dentro WrenAI.
- **Vanna** (motore text-to-SQL con supporto a più database già preconfigurati) — https://github.com/vanna-ai/vanna
- oppure crea un connettore personalizzato, se nessuna delle due soluzioni si adatta bene al database.

Chiedimi dove si trova il database.

Fai così:

1. **Prima di tutto, verifica che siano installate e attive le estensioni** (elenco reale dei pacchetti attivi su questa macchina, da `~/.pi/agent/settings.json`):
   - @narumitw/pi-goal (goal tracking)
   - @narumitw/pi-plan-mode (plan mode)
   - @pi-stef/catalog (catalogo pacchetti)
   - @pi-stef/web (estensione web @pi-stef)
   - @rohaquinlop/pi-subagents (orchestrazione subagent)
   - pi-codex-goal (gestione obiettivi/stato Codex)
   - pi-mcp-adapter (integrazione server MCP esterni)
   - @tmustier/pi-clean-slides (generazione e modifica PowerPoint)
   - pi-ocr (riconoscimento testo da immagini e PDF)
   - pi-docparser (parse di documenti: PDF, DOCX, XLSX, CSV...)
   - @joemccann/pi-pdf (operazioni PDF: merge, split, moduli, watermark)
   - @firstpick/pi-package-webui (Web UI dei pacchetti)
   - @narumitw/pi-chrome-devtools (integrazione Chrome DevTools)
   - @llblab/pi-telegram (integrazione Telegram)
   - @zosmaai/pi-llm-wiki (wiki persistente, stile Karpathy)
   - @juicesharp/rpiv-web-tools (web tools: ricerca e navigazione web)
   - pi-hermes-memory (memoria a lungo termine tra le sessioni)
   - pi-agent-pi-markitdown (conversione documento→Markdown (PDF, DOCX, XLSX, immagini, audio...))
   Se qualcuna di queste non serve per questo progetto, non installarla.
2. Poi leggi il database nella cartella indicata e analizza la sua struttura (tabelle, campi, relazioni). Se non riconosci il tipo di database, cerca online le informazioni necessarie per capirlo e procedi solo se hai conferma di averlo identificato.
3. Configura il motore NL-query scelto, collegato a quel database.
4. Crea per me le regole di comportamento dell'agente (stile delle risposte, sicurezza, limiti, formato). Applica queste regole operative:
   - Rispondi sempre in italiano.
   - Prima di ogni azione con impatto reale (installazioni, modifiche a file di configurazione, cancellazioni, operazioni sul database, file importanti) spiega cosa stai per fare e aspetta conferma esplicita.
   - Se non sai qualcosa, dillo e chiedi: non inventare.
   - Prima di indicazioni tecniche importanti, verifica se ci sono novità aggiornate sull'argomento.
   - Usa solo i token necessari: risposte brevi, senza commenti superflui.
5. Crea per questo progetto un file PROJECT.md con le regole del progetto (struttura cartelle, convenzioni, cose da non toccare).
6. Crea un alias con il nome `axios` (conformità AI Act: io resto deployer, il ruolo di provider resta allo sviluppatore).
7. Fammi una domanda di prova sul database per verificare che il motore NL-query funziona.

Quando hai finito, riepilogami in elenco cosa hai installato e configurato.
