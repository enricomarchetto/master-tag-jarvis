---
tipo: guida
piattaforma: macOS
master: ITAVPT AI for Advertising — Spring 2026
docente: Enrico Marchetto
tags: [guida, setup, mac, jarvis, master-tag]
---

# Guida setup Jarvis — versione Mac

Questa guida ti porta da zero a un ambiente di lavoro AI completo, identico a quello che useremo in aula durante le mie lezioni del Master. Tempo stimato: **circa 40 minuti**, una volta sola.

Quando finisci avrai:

- un **terminale moderno** (Warp)
- un **AI conversazionale** che lavora dentro il tuo file system (Claude Code = "Jarvis")
- un **archivio personale di note** che cresce nel tempo (Obsidian + un piccolo vault)
- un set di **skill** (i comandi di Jarvis, come `/setup-vault` e `/save-session`) già pronte nel vault

Non serve sapere programmare. Serve solo seguire i passi in ordine.

## Cos'è un vault e a cosa serve

Il "vault" è semplicemente una **cartella del tuo computer** dove tieni tutte le note che scrivi con Obsidian. Sono **file di testo in markdown** (`.md`), niente database o formati proprietari: leggibili e portabili ovunque.

A cosa serve, in pratica:

- **Tenere insieme appunti, ricerche, progetti** in una sola cartella, invece che sparsi tra Note, Drive, Word, ecc.
- **Far lavorare Jarvis dentro la tua conoscenza**: Jarvis legge e scrive nelle tue note, quindi può estrarre, riassumere, produrre brief, presentazioni, post LinkedIn partendo da ciò che hai già scritto invece che da una pagina bianca.
- **Crescere nel tempo**: ogni sessione lascia tracce (daily note, file di tracking, memoria di Jarvis). Col tempo il vault diventa il tuo archivio personale di pensiero e produzione.

**Esempio concreto**: scrivi a Jarvis "prepara un brief per il cliente X partendo dai miei appunti dell'ultima call". Jarvis cerca nel vault le note giuste, ti propone una bozza e la salva come nuova nota, pronta da rifinire e inviare. Tu parti da una pagina già piena, non da una bianca.

In aula partirete tutti con uno **starter pack** identico (cartelle base, skill, configurazione di Jarvis). Lo personalizzeremo insieme durante la prima lezione.

## Cosa ti serve prima di iniziare

- un Mac (Apple Silicon o Intel, qualsiasi versione di macOS dal 2020 in poi)
- un **abbonamento Claude Pro** (o crediti API Anthropic). Senza uno dei due Claude Code non parte. Se non ce l'hai, ne parliamo in aula: valutiamo alternative insieme.
- un account Google (serve solo se userai Google Drive come cloud di sincronizzazione del vault, vedi Step 3. Drive non è obbligatorio, vanno bene anche Dropbox, OneDrive, iCloud Drive)
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
   - **"Build an agent" oppure "Terminal"**, scegli **Terminal**
   - **Select directory**, seleziona la tua **home** (`/Users/<tuonome>`) oppure salta se l'opzione c'è

A questo punto vedi un prompt tipo:

```
TuoNome@TuoMac ~ %
```

Sei in Warp. Da qui in poi tutti i comandi li dai qui.

## Step 2 — Installa Claude Code

Claude Code è "Jarvis": l'AI agentica che lavora dentro il tuo file system, legge le tue cartelle, scrive file, ti aiuta a ragionare. È l'unica cosa che installi a mano: **tutto il resto lo installa lui per te**.

In Warp incolla:

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Chiudi e riapri Warp, poi verifica:

```bash
claude --version
```

Se risponde con un numero di versione, è installato. La prima volta che lo lanci (lo faremo allo Step 4) ti chiede di fare **login con il tuo account Claude** (Pro).

> Non serve installare Homebrew, Node.js o npm: l'installer nativo di Claude Code non li richiede. Se in futuro un'attività ne avrà bisogno, te lo dirà Claude stesso e li installerà lui.

## Step 3 — Crea la cartella del vault

Il vault può stare dove vuoi, ma ti consiglio un servizio di sincronizzazione cloud (**Google Drive**, **Dropbox**, **OneDrive**, **iCloud Drive**): se cambi dispositivo ritrovi lo stesso vault aggiornato. Qui usiamo Google Drive; con un altro provider adatta il path. Se lavori sempre da un solo computer puoi saltare il cloud: l'opzione "vault locale" è in fondo a questo step.

**Setup Google Drive** (consigliato):

1. Installa **Google Drive per desktop** da [google.com/drive/download](https://www.google.com/drive/download/), trascina in Applicazioni, avvia, login con il tuo account Google
2. Lascia che Drive si sincronizzi. Il path sul Mac sarà tipo:
   `~/Library/CloudStorage/GoogleDrive-<tuamail>/Il mio Drive/`
3. Crea la cartella del vault in Warp:

```bash
mkdir "$HOME/Library/CloudStorage/GoogleDrive-tuamail@gmail.com/Il mio Drive/MioVault"
```

(Sostituisci `tuamail@gmail.com` col tuo indirizzo Google. Il path ha gli spazi, quindi vanno le **virgolette**.)

Per scoprire il path esatto del tuo Drive: in Finder vai su Google Drive, tasto destro -> **Get Info** (oppure ⌘I), sotto "Where" trovi il path completo. Puoi anche **trascinare la cartella da Finder dentro Warp** dopo aver scritto `cd `: Warp incolla il path automaticamente.

**Se preferisci tenere il vault locale** (non su Drive):

```bash
mkdir ~/MioVault
```

## Step 4 — Lascia che Claude installi la skill Jarvis

Questo è il passo "magico": invece di scaricare e scompattare zip a mano, **chiedi a Claude di farlo**.

Entra nella cartella del vault e avvia Claude Code:

```bash
cd "<path-completo-del-vault>"
claude
```

Al primo avvio fai login con il tuo account Claude. Poi incolla questo messaggio:

```
Scarica lo starter pack "vault-starter-master-tag.zip" dall'ultima release di
https://github.com/enricomarchetto/master-tag-jarvis,
estrailo direttamente nella root di questa cartella (non in una sottocartella),
poi verifica che ci siano .claude/, .obsidian/, Templates/ e CLAUDE.md.
Se per fare qualcosa ti serve un programma che manca (git, Node, ecc.), dimmelo
e installalo tu.
```

Claude ti chiederà il permesso per scaricare e scrivere file: **leggi cosa sta per fare e conferma**. Quando finisce, hai nel vault le skill di Jarvis (`/setup-vault`, `/save-session`, `/handoff`, `/vault-health-check`, ...), i template e la configurazione base.

**Se Claude non riesce a scaricare lo zip**, fallo a mano: scaricalo dalla [pagina Releases](https://github.com/enricomarchetto/master-tag-jarvis/releases/latest) (sezione "Assets"), mettilo nei Download e chiedi a Claude: *"estrai lo zip che trovi in Downloads nella cartella corrente"*.

Quando ha finito, scrivi `/exit`: nei prossimi step lavori su Obsidian, e a Claude torniamo allo Step 7.

## Step 5 — Installa Obsidian + attiva la sua CLI

Obsidian è il database delle tue note. È gratis, locale, basato su file markdown.

1. Vai su [obsidian.md](https://obsidian.md), scarica per Mac, apri il `.dmg`, trascina in Applicazioni
2. Apri Obsidian
3. Vai in **Settings** (icona ingranaggio in basso a sinistra)
4. **General**
5. Scorri fino a **Command line interface** e attivala
6. Obsidian ti mostra un prompt di registrazione: clicca su "Register" o equivalente
7. **Chiudi Warp e riaprilo** (importante: il terminale deve ricaricare il PATH)
8. In Warp, verifica:

```bash
obsidian help
```

Se risponde con la lista comandi, sei a posto (altrimenti vedi Troubleshooting).

## Step 6 — Apri il vault in Obsidian

In Obsidian:

1. **Open folder as vault**
2. Seleziona la cartella del vault appena creata
3. Clicca "Trust author" se chiede
4. **Lascia Obsidian aperto** per tutto il setup e per ogni sessione successiva con Jarvis (la CLI dialoga con Obsidian in esecuzione, se chiudi smette di funzionare)

## Step 7 — Avvia Jarvis e fai il setup

Da Warp, nella cartella del vault, lancia `claude`. Poi scrivi:

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

## Come lavori ogni giorno

Il tuo setup quotidiano sono due finestre affiancate: **Warp** (dove parli con Jarvis) e **Obsidian** (dove leggi, correggi e colleghi le note che Jarvis crea o modifica).

1. Apri **Obsidian** con il vault (deve restare aperto: la CLI dialoga con lui)
2. Apri **Warp** e vai nella cartella del vault (`vault`, se hai creato l'alias, oppure `cd` col path completo)
3. Lancia `claude` e lavora con Jarvis
4. A fine sessione: `/save-session` poi `/exit`

## Troubleshooting Mac-specifico

**`obsidian: command not found`**
Hai attivato la CLI in Obsidian ma non hai chiuso e riaperto Warp. Chiudi e riapri Warp.

**Gatekeeper blocca Warp / Obsidian**
Al primo avvio macOS blocca le app scaricate. Soluzione: tasto destro sull'app in Applicazioni -> **Apri**. Solo la prima volta.

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

**Le slash command non compaiono, o Jarvis non legge il vault**
Tre check:
1. Obsidian è aperto sul vault giusto?
2. `obsidian help` risponde dal terminale?
3. Claude Code è lanciato dalla root del vault?

Se vuoi una **rete di sicurezza** contro errori, prima di cominciare a lavorare scrivi a Claude:

```
Inizializza git in questa cartella e fai un primo commit "Initial vault starter".
Se git non è installato, installalo tu.
```

Da quel momento, se Jarvis fa danni, chiedi a Claude di riportare il vault all'ultimo commit.

## Domande

Se ti si rompe qualcosa o un passaggio non torna, niente panico: ne parliamo a lezione e lo sistemiamo insieme.
