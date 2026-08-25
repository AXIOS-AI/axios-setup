# Guida Installazione pi

> Versione: 3.0 — 08/08/2026
> Per chi: utenti non tecnici — passo-passo, un comando alla volta

---

## 1. Cosa serve

| Cosa | Note |
| ------ | ------ |
| PC Linux (Ubuntu/Debian) | Qualsiasi, anche vecchio |
| Connessione internet | Per installare e per usare l'AI |
| Chiave API | Scegli un provider nella sezione 3 e registrati |

---

## 2. Installa Node.js + pi

Apri **Terminale**. Copia un comando alla volta, incollalo e premi **Invio**, aspettando che finisca prima di passare al successivo.

### Passo 1 — Aggiorna il sistema

```bash
sudo apt update
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

> Così la cosa fatta si applica: al prossimo avvio il terminale legge il
> file `~/.bashrc` che abbiamo appena aggiornato, e il comando `pi` sarà
> riconosciuto senza sudo. Se non lo chiudi, in alcune macchine il percorso
> non viene aggiornato e pi potrebbe non essere trovato.

Poi continua col Passo 4.

### Passo 4 — Installa pi

```bash
npm install -g @earendil-works/pi-coding-agent
```

> **Attenzione a sudo:** se questo comando ti chiede `sudo`, significa che il Passo 3 non è stato applicato. Con `~/.npm-global` i pacchetti si installano nella tua cartella utente e **sudo non serve più**.

### Verifica

Chiudi e riapri terminale, poi un comando alla volta:

```bash
node -v   # deve mostrare v22.x.x
```

```bash
pi --version   # deve mostrare un numero
```

---

## 3. Scegli un provider e ottieni la chiave API

Registrati su uno di questi servizi e genera una chiave API gratuita:

| Provider | URL | Modelli gratis | Cosa offre |
| ---------- | ----- | --------------- | ------------ |
| **OpenCode** | <https://opencode.ai> | ✅ sì | Tanti modelli free (DeepSeek, Llama, Qwen...) |
| **Kilo** | <https://kilocode.ai> | ✅ sì | 300+ modelli, free tier incluso |
| **Cline** | <https://cline.bot> | ✅ sì | Modelli gratuiti senza chiave |

**Consigliato:** OpenCode (opencode.ai) — registrazione veloce, tanti modelli gratis.

Dopo la registrazione, vai su **API Keys** → **Create API Key** e copia la chiave.

### 3a. Inserisci la chiave in pi

```bash
pi
```

Al primo avvio, pi ti chiederà automaticamente la chiave.
Incollala e scegli il nome del provider (es. `opencode`).

Se non chiede, scrivi nella chat:

```
/login
```

Poi esci con:

```
/exit
```

---

## 4. Crea la cartella per il database

### 4a. Dal file manager (senza terminale)

1. Apri **File** (il gestore file, icona cartella) dalla barra laterale
2. Vai nella tua cartella **Home** (in alto a sinistra, "Home")
3. Clic destro su uno spazio vuoto → **Nuova cartella**
4. Chiamala `progetti` (miniscolo) e premi Invio
5. Doppio clic su `progetti` per entrarci
6. Clic destro → **Nuova cartella** → chiamala `mio-database`
7. Entra in `mio-database` → crea un'altra cartella `database`
8. Trova il tuo file del database (es. `miodb.sqlite` o `.db`) e **trascinalo** dentro `database`

Il risultato finale deve essere:

```
~/progetti/mio-database/database/miodb.sqlite
```

### 4b. Dal terminale (equivalente)

```bash
mkdir -p ~/progetti/mio-database/database
```

Poi copia il file del database (es. `miodb.sqlite` o `.db`) dentro `~/progetti/mio-database/database/`.

> **Hai un database Winfarm (Firebird)?** Metti anche la cartella del profilo Firebird accanto al database, così pi potrà leggere i dati Winfarm. Se non sai cos'è, salta pure: pi configura tutto da solo chiedendoti le informazioni mancanti.

---

## 5. Configura pi per il tuo database

```bash
pi
```

Poi, in chat, **copia e incolla tutto il contenuto del file**
[CONFIGURAZIONE.md](CONFIGURAZIONE.md) (lo trovi accanto a questa guida,
nella stessa cartella).

> In quel file c'è tutto: pi installa **solo il motore NL-query di WrenAI**,
> configura il database, installa le estensioni (memoria e wiki), crea le
> regole dell'agente e le regole per il progetto, e ti fa una domanda di prova.
>
> Per aggiornare in futuro la configurazione, basta modificare il file
> `CONFIGURAZIONE.md` e incollarlo di nuovo in chat: **non dovrai toccare
> questa guida di installazione**.

---

## Note finali

Questa è la configurazione **minima** per partire.

Pi è un ambiente **fortemente personalizzabile**: ognuno configura il proprio agente in base alle proprie esigenze. Non esiste una configurazione "giusta" universale — quello che va bene per uno può non andare bene per un altro.

Per personalizzare serve un po' di dimestichezza con:

- ambiente Linux
- mondo AI (modelli, provider, API key)

La scelta della configurazione minima non è pigrizia, è **deliberata**: ogni persona ha esigenze diverse. Con questa base puoi già usare pi, poi lo adatterai.

### Conformità AI Act

Pi è il **motore agentico** di **axios**. Per evitare conflitti tra i ruoli di provider e deployer previsti dal regolamento AI Act (UE) già in vigore, **chiedi a pi di creare un alias col nome `axios`**. In questo modo rimani **deployer**, lasciando il ruolo di **provider** allo sviluppatore.

A tua discrezione e sotto la tua responsabilità, puoi rinominare `axios` col nome della tua azienda, ma questo comporta adeguamenti legislativi europei.