# CONFIGURAZIONE — da incollare in pi

> Copia e incolla tutto il testo qui sotto nella chat di pi.
> pi eseguirà la configurazione passo-passo spiegandoti ogni passaggio.

---

Installa e configura WrenAI **solo il motore NL-query** (non installare la console grafica, l'interfaccia web né il resto della suite WrenAI, non servono).
Chiedimi dove si trova il database.

Riferimento: https://github.com/Canner/WrenAI

Fai così:

1. Leggi il database nella cartella indicata e analizza la sua struttura (tabelle, campi, relazioni).
2. Configura il motore NL-query di WrenAI collegato a quel database.
3. Se il database è Winfarm (Firebird), usa anche la cartella del profilo Firebird se presente accanto al database; altrimenti chiedimi le informazioni mancanti.
4. Verifica che siano installate e attive le estensioni (elenco reale dei pacchetti attivi su questa macchina, da `~/.pi/agent/settings.json`):
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
5. Crea per me le regole di comportamento dell'agente (stile delle risposte, sicurezza, limiti, formato).
6. Crea per questo progetto un file PROJECT.md con le regole del progetto (struttura cartelle, convenzioni, cose da non toccare).
7. Crea un alias con il nome `axios` (conformità AI Act: io resto deployer, il ruolo di provider resta allo sviluppatore).
8. Fammi una domanda di prova sul database per verificare che il motore NL-query funziona.

Quando hai finito, riepilogami in elenco cosa hai installato e configurato.
