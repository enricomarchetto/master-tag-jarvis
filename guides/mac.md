---
tipo: guida
piattaforma: macOS
master: ITAVPT AI for Advertising — Spring 2026
docente: Enrico Marchetto
tags: [guida, setup, mac, jarvis, master-tag]
---

# Guida setup Jarvis — versione Mac

Questa guida ti porta da zero a un ambiente di lavoro AI completo, identico a quello che useremo in aula durante le mie lezioni del Master. Tempo stimato: **circa 30 minuti**, una volta sola.

L'idea è semplice: **installi solo l'app Claude**, fai il login, e poi è Claude stesso a installare e configurare tutto il resto. Tu confermi i passaggi.

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

- un Mac (Apple Silicon o Intel, qualsiasi versione di macOS dal 2020 in poi)
- un **abbonamento Claude Pro** (o crediti API Anthropic). Senza uno dei due Claude Code non parte. Se non ce l'hai, ne parliamo in aula: valutiamo alternative insieme.
- un account Google (serve solo se userai Google Drive come cloud di sincronizzazione del vault, vedi Step 2. Drive non è obbligatorio, vanno bene anche Dropbox, OneDrive, iCloud Drive)
- circa 2 GB di spazio libero su disco
- una connessione decente

## Step 1 — Installa l'app Claude e fai il login

1. Vai su [claude.ai/download](https://claude.ai/download) e scarica l'app per Mac
2. Apri il `.dmg` e trascina **Claude** in Applicazioni. Al primo avvio, se macOS chiede conferma perché l'app arriva da Internet, autorizza
3. Apri l'app e fai **login con il tuo account Claude** (quello con l'abbonamento Pro)
4. Nell'app trovi la sezione **Code**: è Claude Code, cioè "Jarvis". La useremo allo Step 3

Questa è l'unica installazione "a mano" per Claude. Node.js, npm, git e tutto il resto, se serviranno, li installa Claude per te.

## Step 2 — Crea la cartella del vault

Il vault può stare dove vuoi, ma ti consiglio un servizio di sincronizzazione cloud (**Google Drive**, **Dropbox**, **OneDrive**, **iCloud Drive**): se cambi dispositivo ritrovi lo stesso vault aggiornato. Qui usiamo Google Drive; con un altro provider adatta il percorso. Se lavori sempre da un solo computer puoi saltare il cloud: l'opzione "vault locale" è in fondo a questo step.

**Setup Google Drive** (consigliato):

1. Installa **Google Drive per desktop** da [google.com/drive/download](https://www.google.com/drive/download/), trascina in Applicazioni, avvia
2. Login con il tuo account Google e lascia che Drive si sincronizzi
3. Apri **Finder**: Google Drive compare nella barra laterale. Entra in **Il mio Drive**
4. Crea una nuova cartella e chiamala **MioVault**

**Se preferisci tenere il vault locale** (non su Drive): crea una cartella **MioVault** dentro Documenti.

## Step 3 — Apri la cartella in Claude e installa la skill Jarvis

Questo è il passo "magico": invece di scaricare e scompattare zip a mano, **chiedi a Claude di farlo**.

1. Nell'app Claude vai nella sezione **Code**
2. Quando ti chiede una cartella di lavoro, scegli la cartella **MioVault** appena creata
3. Incolla questo messaggio:

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

## Step 4 — Installa Obsidian + attiva la sua CLI

Obsidian è il database delle tue note. È gratis, locale, basato su file markdown. Chiedi a Claude di installarlo:

```
Installa Obsidian su questo computer, con Homebrew (se non c'è, installa prima Homebrew).
```

(Se preferisci farlo a mano: scarica da [obsidian.md](https://obsidian.md) e trascina in Applicazioni.)

Poi attiva la CLI, che permette a Claude di leggere e scrivere le note tramite Obsidian. Questo passaggio lo fai tu:

1. Apri Obsidian
2. Vai in **Settings** (icona ingranaggio in basso a sinistra) -> **General**
3. Scorri fino a **Command line interface** e attivala
4. Obsidian ti mostra un prompt di registrazione: clicca su "Register" o equivalente
5. **Chiudi e riapri l'app Claude** (importante: deve ricaricare il PATH), rientra in **Code** sulla cartella MioVault e scrivi:

```
Esegui "obsidian help" e dimmi se funziona.
```

Se risponde con la lista comandi, sei a posto (altrimenti vedi Troubleshooting).

## Step 5 — Apri il vault in Obsidian

In Obsidian:

1. **Open folder as vault**
2. Seleziona la cartella MioVault
3. Clicca "Trust author" se chiede
4. **Lascia Obsidian aperto** per tutto il setup e per ogni sessione successiva con Jarvis (la CLI dialoga con Obsidian in esecuzione, se chiudi smette di funzionare)

## Step 6 — Fai il setup di Jarvis

Torna nell'app Claude, sezione **Code**, con la cartella MioVault. Scrivi:

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
2. Apri l'app **Claude**, sezione **Code**, sulla cartella MioVault
3. Lavora con Jarvis
4. A fine sessione: `/save-session`

## Troubleshooting Mac-specifico

**`obsidian` non viene riconosciuto**
Hai attivato la CLI in Obsidian ma non hai chiuso e riaperto l'app Claude. Chiudila, riaprila e riprova.

**Gatekeeper blocca Claude / Obsidian**
Al primo avvio macOS blocca le app scaricate. Soluzione: tasto destro sull'app in Applicazioni -> **Apri**. Solo la prima volta.

**Le slash command non compaiono, o Jarvis non legge il vault**
Tre check:
1. Obsidian è aperto sul vault giusto?
2. Claude risponde a "esegui `obsidian help`"?
3. In Code hai scelto come cartella di lavoro la root del vault (MioVault), non una sottocartella?

Se vuoi una **rete di sicurezza** contro errori, prima di cominciare a lavorare scrivi a Claude:

```
Inizializza git in questa cartella e fai un primo commit "Initial vault starter".
Se git non è installato, installalo tu.
```

Da quel momento, se Jarvis fa danni, chiedi a Claude di riportare il vault all'ultimo commit.

## Domande

Se ti si rompe qualcosa o un passaggio non torna, niente panico: ne parliamo a lezione e lo sistemiamo insieme.
