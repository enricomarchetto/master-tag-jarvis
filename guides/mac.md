---
tipo: guida
piattaforma: macOS
master: ITAVPT AI for Advertising — Spring 2026
docente: Enrico Marchetto
tags: [guida, setup, mac, jarvis, master-tag]
---

# Guida setup Jarvis — versione Mac

Questa guida ti porta da zero a un ambiente di lavoro AI completo, identico a quello che useremo in aula durante le mie lezioni del 19 e 21 maggio. Tempo stimato: **circa un'ora**, una volta sola.

Quando finisci avrai:

- un **terminale moderno** (Warp)
- un **AI conversazionale** che lavora dentro il tuo file system (Claude Code = "Jarvis")
- un **archivio personale di note** che cresce nel tempo (Obsidian + un piccolo vault)
- un **IDE** dove tutto questo si parla (Antigravity)

Non serve sapere programmare. Serve solo seguire i passi in ordine.

## Cos'è un vault e a cosa serve

Il "vault" è semplicemente una **cartella del tuo computer** dove tieni tutte le note che scrivi con Obsidian. Sono **file di testo in markdown** (`.md`), niente database o formati proprietari: leggibili e portabili ovunque.

A cosa serve, in pratica:

- **Tenere insieme appunti, ricerche, progetti** in una sola cartella, invece che sparsi tra Note, Drive, Word, ecc.
- **Far lavorare Jarvis dentro la tua conoscenza**: Jarvis legge e scrive nelle tue note, quindi può estrarre, riassumere, produrre brief, presentazioni, post LinkedIn partendo da ciò che hai già scritto invece che da una pagina bianca.
- **Crescere nel tempo**: ogni sessione lascia tracce (daily note, file di tracking, memoria di Jarvis). Col tempo il vault diventa il tuo archivio personale di pensiero e produzione.

**Esempio concreto** (lo vedrete in aula): posso connettere Jarvis a Meta Ads e chiedergli un report per ROAS, per creatività, o i top 3 ad set per ROAS negli ultimi 7 giorni. Jarvis prende i dati, prepara una nota nel vault con il riassunto e i punti su cui agire, e voi la trasformate in un messaggio per il cliente o in slide per la review settimanale.

In aula partirete tutti con uno **starter pack** identico (cartelle base, skill, configurazione di Jarvis). Lo personalizzeremo insieme durante la prima lezione.

## Cosa ti serve prima di iniziare

- un Mac (Apple Silicon o Intel, qualsiasi versione di macOS dal 2020 in poi)
- un **abbonamento Claude Pro** (o crediti API Anthropic). Senza uno dei due Claude Code non parte. Se non ce l'hai, ne parliamo in aula: valutiamo alternative insieme.
- un account Google (serve per Antigravity, e per Google Drive se lo userai come cloud di sincronizzazione del vault — vedi Step 6. Drive non è obbligatorio, vanno bene anche Dropbox, OneDrive, iCloud Drive)
- circa 2 GB di spazio libero su disco
- una connessione decente (alcuni download sono grossi, es. Xcode Command Line Tools ~1 GB)

## Step 1 — Installa Warp (terminale)

Warp è il tuo nuovo terminale. Più moderno e più "umano" del Terminale di sistema.

1. Vai su [warp.dev](https://www.warp.dev) e scarica la versione Mac
2. Apri il `.dmg`, trascina **Warp** in Applicazioni
3. Avvia Warp dalle Applicazioni
4. Se Mac dice "app scaricata da Internet, sei sicuro?", autorizza (è normale, succede solo al primo avvio)
5. Al primo avvio Warp chiede:
   - **Login con Google o email** (consigliato, ti dà la sincronizzazione delle preferenze)
   - **"Build an agent" oppure "Terminal"** → scegli **Terminal**
   - **Select directory** → seleziona la tua **home** (`/Users/<tuonome>`) oppure salta se l'opzione c'è

A questo punto vedi un prompt tipo:

```
TuoNome@TuoMac ~ %
```

Sei in Warp. Da qui in poi tutti i comandi li dai qui.

## Step 2 — Installa Homebrew

Homebrew è un "gestore di pacchetti" per Mac. Ti permette di installare software (Node, git, ecc.) senza dover scaricare installer uno per uno e senza problemi di permessi.

Copia e incolla questo comando in Warp, poi premi Invio:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Durante l'installazione:

- ti chiederà la **password del tuo Mac** (quella che usi per il login). **Mentre la digiti non vedi niente sullo schermo**: né asterischi, né pallini, né movimento. È normale, è una scelta di sicurezza di Unix. Scrivi la password "al buio" e premi Invio.
- scaricherà i **Command Line Tools per Xcode** (~1 GB, può richiedere 5-20 minuti a seconda della connessione). Lascia girare, non fare altro nel terminale.

Quando finisce, vedrai un messaggio tipo "Installation successful". Aggiungi Homebrew al PATH copiando questo comando, di cui ti darà il testo esatto sullo schermo (di solito è uno dei due qui sotto, dipende dal Mac):

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

Verifica:

```bash
brew --version
```

Se risponde con un numero di versione, sei a posto.

## Step 3 — Installa Node.js + npm

Node serve a far girare Claude Code. Con Homebrew è banale:

```bash
brew install node
```

Aspetta che finisca (30 secondi - 2 minuti). Poi verifica:

```bash
node -v
npm -v
```

Dovresti vedere due numeri di versione (es. `v22.x.x` e `10.x.x`).

## Step 4 — Installa Claude Code

Claude Code è "Jarvis": l'AI agentica che lavora dentro il tuo file system, legge le tue cartelle, scrive file, ti aiuta a ragionare. Installa con:

```bash
npm install -g @anthropic-ai/claude-code
```

(Grazie ad Homebrew, npm non ti chiederà sudo. Se ti chiede sudo, vuol dire che hai installato Node in un altro modo: dimmelo e ti aiuto a sistemare.)

Verifica:

```bash
claude --help
```

Se risponde con la lista comandi, Claude Code è installato.

## Step 5 — Installa Obsidian + attiva la sua CLI

Obsidian è il database delle tue note. È gratis, locale, basato su file markdown.

1. Vai su [obsidian.md](https://obsidian.md), scarica per Mac, apri il `.dmg`, trascina in Applicazioni
2. Apri Obsidian
3. Vai in **Settings** (icona ingranaggio in basso a sinistra)
4. → **General**
5. Scorri fino a **Command line interface** e attivala
6. Obsidian ti mostra un prompt di registrazione: clicca su "Register" o equivalente
7. **Chiudi Warp e riaprilo** (importante: il terminale deve ricaricare il PATH)
8. In Warp, verifica:

```bash
obsidian help
```

Se risponde con la lista comandi, sei a posto. Se dice "command not found", non hai ancora riaperto Warp dopo aver attivato la CLI.

## Step 6 — Crea la cartella del vault

Il "vault" è la cartella dove vivono le tue note Obsidian + Jarvis. Puoi metterla dove vuoi.

**Consiglio**: mettila dentro un servizio di sincronizzazione cloud, così se cambi dispositivo (casa, ufficio, laptop) trovi sempre lo stesso vault aggiornato. Va bene **Google Drive**, ma anche alternative come **Dropbox**, **OneDrive** o **iCloud Drive**: il principio è lo stesso. Nelle guide useremo Google Drive perché è il più diffuso; se preferisci un'altra cloud va bene, basta adattare il path al tuo provider.

Se userai sempre lo stesso Mac e non hai bisogno di sincronizzare, puoi anche saltare la parte cloud: trovi l'opzione "vault locale" in fondo a questo Step.

**Setup Google Drive** (consigliato):

1. Installa **Google Drive per desktop** da [google.com/drive/download](https://www.google.com/drive/download/), trascina in Applicazioni, avvia, login con il tuo account Google
2. Lascia che Drive si sincronizzi. Il path sul Mac sarà tipo:
   `~/Library/CloudStorage/GoogleDrive-<tuamail>/Il mio Drive/`
3. Crea la cartella del vault in Warp:

```bash
mkdir "$HOME/Library/CloudStorage/GoogleDrive-tuamail@gmail.com/Il mio Drive/MioVault"
```

(Sostituisci `tuamail@gmail.com` col tuo indirizzo Google. Il path ha gli spazi, quindi vanno le **virgolette**.)

Per scoprire il path esatto del tuo Drive: in Finder vai su Google Drive, tasto destro → **Get Info** (oppure ⌘I), sotto "Where" trovi il path completo. Puoi anche **trascinare la cartella da Finder dentro Warp** dopo aver scritto `cd `: Warp incolla il path automaticamente.

**Se preferisci tenere il vault locale** (non su Drive):

```bash
mkdir ~/MioVault
```

## Step 7 — Estrai lo starter pack

Scarica `vault-starter-master-tag.zip` dalla [pagina Releases](https://github.com/enricomarchetto/master-tag-jarvis/releases/latest) di questo repo (sotto la sezione "Assets" della release più recente). Mettilo nei Downloads. Poi in Warp:

```bash
cd "<path-completo-del-vault>"
unzip ~/Downloads/vault-starter-master-tag.zip
```

(Anche qui le virgolette se il path ha spazi.)

Verifica che siano comparsi:

```bash
ls -la
```

Devi vedere (a livello root, **non** in una sottocartella):

- `.claude/`
- `.agents/`
- `.obsidian/`
- `Templates/`
- `CLAUDE.md`
- `AGENTS.md`
- `Guida vault-starter-generic.md`

**Se vedi una sottocartella `vault-starter-master-tag/` dentro al vault** (errore comune):

```bash
rm -rf vault-starter-master-tag
unzip ~/Downloads/vault-starter-master-tag.zip
```

Lo zip va estratto direttamente nella root del vault, non dentro una sottocartella.

## Step 8 — Apri il vault in Obsidian

In Obsidian:

1. **Open folder as vault**
2. Seleziona la cartella del vault appena creata
3. Clicca "Trust author" se chiede
4. **Lascia Obsidian aperto** per tutto il setup e per ogni sessione successiva con Jarvis (la CLI dialoga con Obsidian in esecuzione, se chiudi smette di funzionare)

## Step 9 — Avvia Jarvis e fai il setup

Nella cartella del vault (in Warp):

```bash
claude
```

Si apre l'interfaccia di Claude Code. Scrivi:

```
/setup-vault
```

E premi Invio.

Da qui Jarvis ti intervista (chi sei, cosa fai, su cosa lavori, strumenti, frustrazioni). **Rispondi con calma, lungo, non in monosillabi**: più contesto dai adesso, più il vault ti verrà cucito addosso bene.

Alla fine Jarvis crea:

- la struttura di cartelle (`00 - Inbox`, `01 - Daily`, `04 - Areas`, ecc.)
- la memoria di Jarvis in `99 - Jarvis/memory/`
- file di tracking come `Open Loops.md` e `Session Log.md`
- un `CLAUDE.md` personalizzato sul tuo contesto

Quando finisce, scrivi:

```
/save-session
```

Per consolidare lo stato. Poi:

```
/exit
```

Esci da Claude Code.

## Step 10 — Installa Antigravity (uso quotidiano)

Antigravity è un IDE Google basato su VSCode con AI integrata. Lo useremo come **finestra principale dove tutto si parla**: editor + AI + terminale, tutto in uno.

1. Scarica da [labs.google.com/antigravity](https://labs.google.com/antigravity)
2. Apri il `.dmg`, trascina **Antigravity** in Applicazioni
3. Avvia, autorizza Gatekeeper se chiede (Preferenze di Sistema → Privacy e Sicurezza)
4. Login con account Google
5. Welcome screen: salta i tutorial Gemini, non ci servono adesso

### Apri il vault come progetto in Antigravity

1. **File → Open Folder** (o `⌘O`)
2. Seleziona la cartella del vault
3. Conferma "Trust the authors"

### Apri il terminale embedded e lancia Claude Code

1. `View → Terminal` oppure scorciatoia `` Ctrl+` `` (apice grave, in alto a sinistra sotto Esc)
2. Si apre un pannello terminale in basso
3. Verifica di essere nella cartella del vault con `pwd`
4. Lancia:

```bash
claude
```

Da questo momento, **parli con Jarvis dal terminale di Antigravity**. È esattamente lo stesso Jarvis di prima (le slash command `/save-session`, `/handoff`, `/vault-health-check` funzionano identiche), solo che adesso vedi anche i file del vault nell'explorer di sinistra.

## Cosa fare ogni volta che inizi a lavorare

1. Apri **Obsidian** (vault aperto)
2. Apri **Antigravity** (vault aperto come progetto)
3. Nel terminale embedded di Antigravity: `claude`
4. Lavora con Jarvis
5. A fine sessione: `/save-session` poi `/exit`

## Cosa porterai in aula il 19 e 21 maggio

Per le mie lezioni del Master:

- Setup completato fin qui
- Vault Jarvis funzionante
- Il tuo LLM Pro privato (Claude / ChatGPT / Gemini) attivo durante la lezione
- Carta e penna per appunti grezzi

Durante la lezione costruiremo insieme contenuti pratici dentro il tuo vault. Vedrai Jarvis lavorare in diretta sul mio schermo, replicherai sul tuo.

## Troubleshooting Mac-specifico

**`obsidian: command not found`**
Hai attivato la CLI in Obsidian ma non hai chiuso e riaperto Warp. Chiudi e riapri Warp.

**`npm install -g` chiede sudo**
Hai installato Node senza Homebrew. Soluzione pulita: disinstalla Node (`brew uninstall node` se ce l'hai, oppure usa l'uninstaller del `.pkg` di nodejs.org), poi installa via Homebrew (`brew install node`). Da quel momento `npm install -g` non chiederà più sudo.

**Gatekeeper blocca Warp / Obsidian / Antigravity**
Al primo avvio macOS blocca le app scaricate. Soluzione: tasto destro sull'app in Applicazioni → **Apri**. Solo la prima volta.

**Le slash command non compaiono in Claude Code**
Hai lanciato `claude` fuori dalla root del vault. `cd` nella cartella del vault, poi rilancia `claude`.

**Apple Silicon vs Intel**
Tutti i software citati hanno build native per entrambe le architetture. Il sito di solito rileva automaticamente.

**Path con spazi (es. "Il mio Drive")**
Servono sempre le virgolette nei comandi. Esempio:

```bash
cd "/Users/tuonome/Library/CloudStorage/GoogleDrive-tuamail/Il mio Drive/MioVault"
```

Comodo: crea un alias in `~/.zshrc` per non riscrivere il path lungo ogni volta:

```bash
echo 'alias vault="cd \"/Users/tuonome/Library/CloudStorage/GoogleDrive-tuamail/Il mio Drive/MioVault\""' >> ~/.zshrc
source ~/.zshrc
```

Da quel momento basta scrivere `vault` in Warp e ci entri dentro.

**Jarvis non legge bene il vault**
Tre check:
1. Obsidian è aperto sul vault giusto?
2. `obsidian help` risponde dal terminale?
3. Claude Code è lanciato dalla root del vault?

Se vuoi una **rete di sicurezza** contro errori, prima di cominciare a lavorare:

```bash
cd "<path-vault>"
git init && git add -A && git commit -m "Initial vault starter"
```

Da quel momento se Jarvis fa danni puoi tornare indietro con `git reset --hard HEAD`.

## Domande

Se ti si rompe qualcosa o un passaggio non torna, niente panico: ne parliamo a lezione e lo sistemiamo insieme.
