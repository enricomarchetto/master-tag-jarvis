---
tipo: guida
piattaforma: Windows
master: ITAVPT AI for Advertising — Spring 2026
docente: Enrico Marchetto
tags: [guida, setup, windows, pc, jarvis, master-tag]
---

# Guida setup Jarvis — versione Windows

Questa guida ti porta da zero a un ambiente di lavoro AI completo, identico a quello che useremo in aula durante le mie lezioni del Master. Tempo stimato: **circa 30 minuti**, una volta sola.

L'idea è semplice: **installi Google Drive, Obsidian e l'app Claude**, e poi è Claude stesso a installare e configurare il resto (a partire dalla skill Jarvis). Tu confermi i passaggi.

Quando finisci avrai:

- un **AI conversazionale** che lavora dentro le tue cartelle (Claude Code = "Jarvis")
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
- un account Google (serve solo se userai Google Drive come cloud di sincronizzazione del vault, vedi Step 1. Drive non è obbligatorio, vanno bene anche Dropbox, OneDrive, iCloud Drive)
- circa 2 GB di spazio libero su disco
- una connessione decente
- diritti di amministratore sul tuo PC (per installare software)

## Step 1 — Installa Google Drive e crea la cartella del vault

Il vault può stare dove vuoi, ma ti consiglio un servizio di sincronizzazione cloud (**Google Drive**, **Dropbox**, **OneDrive**, **iCloud Drive**): se cambi dispositivo ritrovi lo stesso vault aggiornato. Qui usiamo Google Drive; con un altro provider adatta il percorso. Se lavori sempre da un solo computer puoi saltare il cloud: l'opzione "vault locale" è in fondo a questo step.

**Setup Google Drive** (consigliato):

1. Installa **Google Drive per desktop** da [google.com/drive/download](https://www.google.com/drive/download/), esegui l'installer
2. Login con il tuo account Google e lascia che Drive si sincronizzi
3. Apri **Esplora File**: Drive compare come un'unità (di solito `G:`). Entra in **Il mio Drive**
4. Crea una nuova cartella e chiamala **Il mio vault**

**Se preferisci tenere il vault locale** (non su Drive): crea una cartella **Il mio vault** dentro Documenti.

## Step 2 — Installa Obsidian e collegalo alla cartella

Obsidian è il database delle tue note. È gratis, locale, basato su file markdown.

1. Vai su [obsidian.md](https://obsidian.md), scarica l'app per Windows ed esegui l'installer
2. Apri Obsidian e scegli **Open folder as vault**
3. Seleziona la cartella **Il mio vault** appena creata
4. Clicca "Trust author" se chiede
5. **Lascia Obsidian aperto** per tutto il setup e per ogni sessione successiva con Jarvis (la CLI dialoga con Obsidian in esecuzione, se chiudi smette di funzionare)

Poi attiva la **CLI di Obsidian**, che permette a Claude di leggere e scrivere le note tramite Obsidian:

1. In Obsidian vai in **Settings** (icona ingranaggio in basso a sinistra) -> **General**
2. Scorri fino a **Command line interface** e attivala
3. Obsidian ti mostra un prompt di registrazione: clicca su "Register" o equivalente

## Step 3 — Installa l'app Claude e fai il login

1. Vai su [claude.ai/download](https://claude.ai/download) e scarica l'app per Windows
2. Esegui l'installer. Se Windows Defender o SmartScreen dice "Windows ha protetto il PC", clicca **Ulteriori informazioni** -> **Esegui comunque**
3. Apri l'app e fai **login con il tuo account Claude** (quello con l'abbonamento Pro)
4. Nell'app trovi la sezione **Code**: è Claude Code, cioè "Jarvis"

Questa è l'ultima installazione "a mano". Node.js, npm, git e tutto il resto, se serviranno, li installa Claude per te.

## Step 4 — Apri la cartella in Claude e installa la skill Jarvis

Questo è il passo "magico": invece di scaricare e scompattare zip a mano, **chiedi a Claude di farlo**.

1. Nell'app Claude vai nella sezione **Code**
2. Quando ti chiede una cartella di lavoro, scegli **Il mio vault**, la stessa cartella che hai aperto in Obsidian
3. Incolla questo messaggio:

```
Scarica lo starter pack "vault-starter-master-tag.zip" dall'ultima release di
https://github.com/enricomarchetto/master-tag-jarvis,
estrailo direttamente nella root di questa cartella (non in una sottocartella),
poi verifica che ci siano .claude/, .obsidian/, Templates/ e CLAUDE.md.
Infine esegui "obsidian help" e dimmi se la CLI di Obsidian funziona.
Se per fare qualcosa ti serve un programma che manca (git, Node, ecc.), dimmelo
e installalo tu.
```

Claude ti chiederà il permesso per scaricare e scrivere file: **leggi cosa sta per fare e conferma**. Quando finisce, hai nel vault le skill di Jarvis (`/setup-vault`, `/save-session`, `/handoff`, `/vault-health-check`, ...), i template e la configurazione base. Se `obsidian help` risponde con la lista comandi, sei a posto (altrimenti vedi Troubleshooting).

**Se Claude non riesce a scaricare lo zip**, fallo a mano: scaricalo dalla [pagina Releases](https://github.com/enricomarchetto/master-tag-jarvis/releases/latest) (sezione "Assets"), mettilo nei Download e chiedi a Claude: *"estrai lo zip che trovi in Downloads nella cartella corrente"*.

## Step 5 — Fai il setup di Jarvis

Sempre nell'app Claude, sezione **Code**, sulla cartella **Il mio vault**. Scrivi:

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

Per consolidare lo stato.

## Come lavori ogni giorno

Il tuo setup quotidiano sono due finestre affiancate: **l'app Claude** (dove parli con Jarvis) e **Obsidian** (dove leggi, correggi e colleghi le note che Jarvis crea o modifica).

1. Apri **Obsidian** con il vault (deve restare aperto: la CLI dialoga con lui)
2. Apri l'app **Claude**, sezione **Code**, sulla cartella **Il mio vault**
3. Lavora con Jarvis
4. A fine sessione: `/save-session`

## Troubleshooting Windows-specifico

**`obsidian` non viene riconosciuto**
Controlla che la CLI sia attiva in Obsidian (Settings -> General -> Command line interface) e che Obsidian sia aperto. Poi chiudi e riapri l'app Claude e riprova: deve ricaricare il PATH.

**Caratteri speciali nel nome utente (es. accenti)**
Se il tuo nome utente Windows contiene caratteri accentati o speciali, alcuni installer fanno fatica. Se incontri problemi che sembrano legati al percorso, scrivimi prima della lezione: ci sono workaround ma vanno valutati caso per caso.

**Le slash command non compaiono, o Jarvis non legge il vault**
Tre check:
1. Obsidian è aperto sul vault giusto?
2. Claude risponde a "esegui `obsidian help`"?
3. In Code hai scelto come cartella di lavoro la root del vault (Il mio vault), non una sottocartella?

Se vuoi una **rete di sicurezza** contro errori, prima di cominciare a lavorare scrivi a Claude:

```
Inizializza git in questa cartella e fai un primo commit "Initial vault starter".
Se git non è installato, installalo tu.
```

Da quel momento, se Jarvis fa danni, chiedi a Claude di riportare il vault all'ultimo commit.

## Domande

Se ti si rompe qualcosa o un passaggio non torna, niente panico: ne parliamo a lezione e lo sistemiamo insieme.
