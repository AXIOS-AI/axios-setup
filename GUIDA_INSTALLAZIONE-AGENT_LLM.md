# Guida Installazione pi

> Per chi: utenti non tecnici — passo-passo, un comando alla volta

---

> ⚠️ **AVVISO — PROCEDURA INDIPENDENTE DALLA MACCHINA**
>
> Questa guida descrive una procedura generica per installare e configurare pi e un agente LLM su **Linux**. Le eventuali referenze a percorsi, provider, nomi di pacchetti, porte o comandi sono esempi: adattali al tuo ambiente.
>
> **Non cercare di replicare esattamente un PC specifico.** Se un agente su un'altra macchina legge questa guida, deve trattare ogni percorso, credenziale, provider e comando come un valore da verificare e, se necessario, sostituire con quelli del proprio ambiente.

## 1. Cosa serve

| Cosa | Note |
| ------ | ------ |
| Sistema operativo | Linux, Windows o macOS |
| PC Linux (Ubuntu/Debian) | Qualsiasi, anche vecchio |
| Windows o macOS | Visita il sito ufficiale: <https://pi.dev/> |
| Connessione internet | Per installare e per usare l'AI |
| Chiave API | Scegli un provider nella sezione 3 e registrati |

> Per usare pi su Windows o macOS, segui le istruzioni specifiche disponibili sul sito ufficiale: <https://pi.dev/>. I comandi della sezione 2 sono destinati a Linux.

## 2. Installa Node.js + pi

Apri **Terminale**. Copia un comando alla volta, incollalo e premi **Invio**, aspettando che finisca prima di passare al successivo.

### Passo 1 — Aggiorna il sistema

```bash
sudo apt update && sudo apt upgrade -y
```

```bash
sudo apt install -y curl
```

### Passo 2 — Installa Node.js 22

```bash
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
```

```bash
sudo apt install -y nodejs
```

### Passo 3 — Imposta npm globale SENZA sudo (evita errori di permessi)

```bash
mkdir -p ~/.npm-global
```

```bash
npm config set prefix ~/.npm-global
```

```bash
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
```

**Chiudi il terminale** (la X in alto o il comando `exit`) e **riaprilo**.

> Così la modifica si applica: al prossimo avvio il terminale legge il
> file `~/.bashrc` aggiornato e il comando `pi` viene riconosciuto senza sudo.
> Se non lo chiudi, su alcune macchine il percorso non viene ricaricato e pi
> potrebbe non essere trovato.

### Passo 4 — Installa pi

```bash
npm install -g @earendil-works/pi-coding-agent
```

> **Attenzione a sudo:** se questo comando ti chiede `sudo`, significa che il Passo 3 non è stato applicato. Con `~/.npm-global` i pacchetti si installano nella tua cartella utente e **sudo non serve**.

### Verifica

Chiudi e riapri il terminale, poi esegui un comando alla volta:

```bash
node -v
```

Deve mostrare una versione `v22.x.x`.

```bash
pi --version
```

Deve mostrare un numero di versione.

---

## 3. Scegli un provider e ottieni la chiave API

Prima di scegliere un provider, installa il pacchetto gratuito:

```bash
pi install npm:pi-free
```

Questo pacchetto dà accesso a provider e modelli gratuiti per le prime operazioni. Potrai continuare a usarli oppure passare a provider a pagamento.

Registrati su uno di questi servizi e genera una chiave API gratuita:

| Provider | URL | Modelli gratis | Cosa offre |
| ---------- | ----- | --------------- | ------------ |
| **OpenCode** | <https://opencode.ai> | ✅ sì | Diversi modelli gratuiti (DeepSeek, Llama, Qwen...) |
| **Kilo** | <https://kilocode.ai> | ✅ sì | 300+ modelli, free tier incluso |
| **Cline** | <https://cline.bot> | ✅ sì | Modelli gratuiti senza chiave |

Dopo la registrazione, vai su **API Keys** → **Create API Key** e copia la chiave.

### 3a. Inserisci la chiave in pi

Avvia pi:

```bash
pi
```

Nella chat esegui:

```text
/login
```

Scegli **Sign in with an API key**, seleziona il provider e incolla la chiave API.

Poi esegui:

```text
/model
```

Premi Invio, scrivi `free` per filtrare i modelli gratuiti e provane uno alla volta finché non trovi quello funzionante.

Per testare la risposta, scrivi:

```text
ciao
```

Quando hai finito, esci con:

```text
/quit
```

---

## 4. Crea la cartella per il database

### 4a. Dal file manager (senza terminale)

1. Apri **File** (il gestore file, icona cartella) dalla barra laterale.
2. Vai nella tua cartella **Home**.
3. Clic destro su uno spazio vuoto → **Nuova cartella**.
4. Chiamala `progetti` (minuscolo) e premi Invio.
5. Doppio clic su `progetti` per entrarci.
6. Clic destro → **Nuova cartella** → chiamala `mio-database`.
7. Entra in `mio-database` → crea un'altra cartella `database`.
8. Trova il file del database (per esempio `miodb.sqlite`, `miodb.db` o `arc2000.fdb`) oppure la cartella che lo contiene e copialo dentro `database`.

Il risultato finale deve essere simile a:

```text
~/progetti/mio-database/database/
```

### 4b. Dal terminale (equivalente)

```bash
mkdir -p ~/progetti/mio-database/database
```

Copia poi il file del database dentro:

```text
~/progetti/mio-database/database/
```

Il nome e il tipo del database possono essere diversi: la procedura successiva li identifica prima di configurare il motore NL-query.

---

## 5. Configura pi per il tuo database

Avvia pi:

```bash
pi
```

Poi, in chat, **copia e incolla tutto il contenuto del file**
[CONFIGURAZIONE.md](CONFIGURAZIONE.md), che si trova nella stessa cartella di questa guida.

> Il file contiene la procedura completa: pi chiede dove si trova il database,
> ne identifica il tipo, ne analizza tabelle, campi e relazioni, sceglie il
> motore NL-query più adatto, verifica e spiega le estensioni, crea le regole
> dell'agente e del progetto, crea l'alias `axios` e ti fa una domanda di prova.

---

## Note finali

Questa è la configurazione **minima** per partire.

Pi è un ambiente **fortemente personalizzabile**: ognuno configura il proprio agente in base alle proprie esigenze. Non esiste una configurazione "giusta" universale: quello che va bene per un utente può non andare bene per un altro.

Per personalizzare serve un po' di dimestichezza con:

- ambiente Linux
- mondo AI (modelli, provider, API key)

La scelta della configurazione minima non è pigrizia: è **deliberata**. Ogni persona ha esigenze diverse. Con questa base puoi già usare pi, poi lo adatterai.

### Conformità AI Act

Pi è il **motore agentico** di **axios**. Per evitare conflitti tra i ruoli di provider e deployer previsti dal regolamento AI Act (UE), **chiedi a pi di creare un alias col nome `axios`**. In questo modo rimani **deployer**, lasciando il ruolo di **provider** allo sviluppatore.

A tua discrezione e sotto la tua responsabilità, puoi rinominare `axios` col nome della tua azienda, ma questo comporta adeguamenti legislativi europei.
