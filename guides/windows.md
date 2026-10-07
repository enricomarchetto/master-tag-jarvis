---
tipo: guida
piattaforma: Windows
master: ITAVPT AI for Advertising — Spring 2026
docente: Enrico Marchetto
tags: [guida, setup, windows, pc, jarvis, master-tag]
---

# Guida setup Jarvis — versione Windows

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

- un PC Windows 10 o 11 (64-bit, qualsiasi versione recente)
- un **abbonamento Claude Pro** (o crediti API Anthropic). Senza uno dei due Claude Code non parte. Se non ce l'hai, ne parliamo in aula: valutiamo alternative insieme.
- un account Google (serve solo se userai Google Drive come cloud di sincronizzazione del vault, vedi Step 3. Drive non è obbligatorio, vanno bene anche Dropbox, OneDrive, iCloud Drive)
- circa 2 GB di spazio libero su disco
- una connessione decente
- diritti di amministratore sul tuo PC (per installare software)

## Step 1 — Installa Warp (terminale)

Warp è il tuo nuovo terminale. Più moderno e più "umano" del PowerShell o Prompt dei comandi di sistema.

1. Vai su [warp.dev](https://www.warp.dev) e scarica la versione Windows
2. Apri il file `.exe` scaricato, segui l'installer
3. Se Windows Defender o SmartScreen dice "Windows ha protetto il PC", clicca **Ulteriori informazioni** -> **Esegui comunque**
4. Avvia Warp dal menu Start
5. Al primo avvio Warp chiede:
   - **Login con Google o email** (consigliato, ti dà la sincronizzazione delle preferenze)
   - **"Build an agent" oppure "Terminal"**, scegli **Terminal**
   - **Select directory**, seleziona la tua **home** (`C:\Users\<tuonome>`) oppure salta se l'opzione c'è

A questo punto vedi un prompt tipo:

```
PS C:\Users\TuoNome>
```

Sei in Warp con PowerShell come shell di default. Da qui in poi tutti i comandi li dai qui.

## Step 2 — Installa Claude Code

Claude Code è "Jarvis": l'AI agentica che lavora dentro il tuo file system, legge le tue cartelle, scrive file, ti aiuta a ragionare. È l'unica cosa che installi a mano: **tutto il resto lo installa lui per te**.

In Warp incolla:

```powershell
irm https://claude.ai/install.ps1 | iex
```

Chiudi e riapri Warp, poi verifica:

```powershell
claude --version
```

Se risponde con un numero di versione, è installato. La prima volta che lo lanci (lo faremo allo Step 4) ti chiede di fare **login con il tuo account Claude** (Pro).

> Non serve installare Node.js o npm: l'installer nativo di Claude Code non li richiede. Se in futuro un'attività ne avrà bisogno, te lo dirà Claude stesso e li installerà lui.

## Step 3 — Crea la cartella del vault

Il vault può stare dove vuoi, ma ti consiglio un servizio di sincronizzazione cloud (**Google Drive**, **Dropbox**, **OneDrive**, **iCloud Drive**): se cambi dispositivo ritrovi lo stesso vault aggiornato. Qui usiamo Google Drive; con un altro provider adatta il path. Se lavori sempre da un solo computer puoi saltare il cloud: l'opzione "vault locale" è in fondo a questo step.

**Setup Google Drive** (consigliato):

1. Installa **Google Drive per desktop** da [google.com/drive/download](https://www.google.com/drive/download/), esegui l'installer
2. Login con il tuo account Google
3. Lascia che Drive si sincronizzi. Su Windows il Drive appare come una **lettera**: di solito `G:`, ma può essere `H:`, `D:` o altra a seconda del tuo sistema (dipende dagli altri drive logici che hai sul PC). Per scoprire la tua: aprilo da Esplora File e guarda la barra in alto.
4. Una volta che sai la lettera giusta, crea la cartella del vault in Warp (sostituisci `<X>` con la tua lettera, di solito `G`):

```powershell
mkdir "<X>:\Il mio Drive\MioVault"
```

Le **virgolette sono obbligatorie** perché il path contiene spazi.

**Se preferisci tenere il vault locale** (non su Drive):

```powershell
mkdir "$HOME\MioVault"
```

## Step 4 — Lascia che Claude installi la skill Jarvis

Questo è il passo "magico": invece di scaricare e scompattare zip a mano, **chiedi a Claude di farlo**.

Entra nella cartella del vault e avvia Claude Code:

```powershell
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

1. Vai su [obsidian.md](https://obsidian.md), scarica per Windows (`.exe`)
2. Esegui l'installer
3. Apri Obsidian dal menu Start
4. Vai in **Settings** (icona ingranaggio in basso a sinistra)
5. **General**
6. Scorri fino a **Command line interface** e attivala
7. Obsidian ti mostra un prompt di registrazione: clicca su "Register" o equivalente
8. **Chiudi Warp e riaprilo** (importante: il terminale deve ricaricare il PATH)
9. In Warp, verifica:

```powershell
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

## Troubleshooting Windows-specifico

**`obsidian: non riconosciuto come comando`**
Hai attivato la CLI in Obsidian ma non hai chiuso e riaperto Warp. Chiudi e riapri Warp.

**Path con spazi (es. "Il mio Drive")**
Servono sempre le virgolette nei comandi. Esempio:

```powershell
cd "G:\Il mio Drive\MioVault"
```

Comodo: crea un alias PowerShell in `$PROFILE` per non riscrivere il path lungo ogni volta:

```powershell
notepad $PROFILE
```

Si apre Notepad (anche se il file non esiste, lo crea). Aggiungi questa riga:

```powershell
function vault { Set-Location "G:\Il mio Drive\MioVault" }
```

Salva, chiudi Notepad, riapri Warp. Da quel momento basta scrivere `vault` e ci entri dentro.

**Caratteri speciali nel nome utente (es. accenti)**
Se il tuo nome utente Windows contiene caratteri accentati o speciali, alcuni installer fanno fatica. Se incontri problemi che sembrano legati al path, scrivimi prima della lezione: ci sono workaround ma vanno valutati caso per caso.

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
