---
tipo: guida
piattaforma: Windows
master: ITAVPT AI for Advertising — Spring 2026
docente: Enrico Marchetto
tags: [guida, setup, windows, pc, jarvis, master-tag]
---

# Guida setup Jarvis — versione Windows

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

- un PC Windows 10 o 11 (64-bit, qualsiasi versione recente)
- un **abbonamento Claude Pro** (o crediti API Anthropic). Senza uno dei due Claude Code non parte. Se non ce l'hai, ne parliamo in aula: valutiamo alternative insieme.
- un account Google (serve per Antigravity, e per Google Drive se lo userai come cloud di sincronizzazione del vault — vedi Step 5. Drive non è obbligatorio, vanno bene anche Dropbox, OneDrive, iCloud Drive)
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

## Step 2 — Installa Node.js + npm

Node serve a far girare Claude Code.

**Opzione consigliata (più semplice): installer ufficiale**

1. Vai su [nodejs.org](https://nodejs.org) e scarica la versione **LTS** (Long Term Support) per Windows
2. Apri il `.msi` scaricato
3. Segui l'installer accettando le opzioni di default
4. Quando ti chiede *"Automatically install the necessary tools"*, **togli la spunta** (non ti serve, è per chi compila codice da zero)
5. Riavvia Warp dopo l'installazione (chiudi e riapri)

Verifica:

```powershell
node -v
npm -v
```

Dovresti vedere due numeri di versione (es. `v22.x.x` e `10.x.x`).

**Se preferisci usare winget** (più moderno, salta l'installer):

```powershell
winget install OpenJS.NodeJS.LTS
```

Poi chiudi e riapri Warp, e verifica con `node -v` e `npm -v`.

## Step 3 — Installa Claude Code

Claude Code è "Jarvis": l'AI agentica che lavora dentro il tuo file system, legge le tue cartelle, scrive file, ti aiuta a ragionare. In Warp:

```powershell
npm install -g @anthropic-ai/claude-code
```

Su Windows non serve "sudo" (esiste l'equivalente "Run as administrator", ma `npm install -g` non lo richiede di default).

Verifica:

```powershell
claude --help
```

Se risponde con la lista comandi, Claude Code è installato.

## Step 4 — Installa Obsidian + attiva la sua CLI

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

Se risponde con la lista comandi, sei a posto. Se dice "non riconosciuto come comando", non hai ancora riaperto Warp dopo aver attivato la CLI.

## Step 5 — Crea la cartella del vault

Il "vault" è la cartella dove vivono le tue note Obsidian + Jarvis. Puoi metterla dove vuoi.

**Consiglio**: mettila dentro un servizio di sincronizzazione cloud, così se cambi dispositivo (casa, ufficio, laptop) trovi sempre lo stesso vault aggiornato. Va bene **Google Drive**, ma anche alternative come **Dropbox**, **OneDrive** o **iCloud Drive**: il principio è lo stesso. Nelle guide useremo Google Drive perché è il più diffuso; se preferisci un'altra cloud va bene, basta adattare il path al tuo provider.

Se userai sempre lo stesso PC e non hai bisogno di sincronizzare, puoi anche saltare la parte cloud: trovi l'opzione "vault locale" in fondo a questo Step.

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

## Step 6 — Estrai lo starter pack

Scarica `vault-starter-master-tag.zip` dalla [pagina Releases](https://github.com/enricomarchetto/master-tag-jarvis/releases/latest) di questo repo (sotto la sezione "Assets" della release più recente). Mettilo nei Download. Poi in Warp:

```powershell
cd "<path-completo-del-vault>"
Expand-Archive -Path "$HOME\Downloads\vault-starter-master-tag.zip" -DestinationPath . -Force
```

`Expand-Archive` è il comando PowerShell nativo per estrarre zip.

Verifica che siano comparsi:

```powershell
Get-ChildItem -Force
```

(L'opzione `-Force` serve a vedere anche file/cartelle nascosti che iniziano con `.`)

Devi vedere (a livello root, **non** in una sottocartella):

- `.claude\`
- `.agents\`
- `.obsidian\`
- `Templates\`
- `CLAUDE.md`
- `AGENTS.md`
- `Guida vault-starter-generic.md`

**Se vedi una sottocartella `vault-starter-master-tag\` dentro al vault** (errore comune):

```powershell
Remove-Item -Recurse -Force vault-starter-master-tag
Expand-Archive -Path "$HOME\Downloads\vault-starter-master-tag.zip" -DestinationPath . -Force
```

Lo zip va estratto direttamente nella root del vault, non dentro una sottocartella.

## Step 7 — Apri il vault in Obsidian

In Obsidian:

1. **Open folder as vault**
2. Seleziona la cartella del vault appena creata
3. Clicca "Trust author" se chiede
4. **Lascia Obsidian aperto** per tutto il setup e per ogni sessione successiva con Jarvis (la CLI dialoga con Obsidian in esecuzione, se chiudi smette di funzionare)

## Step 8 — Avvia Jarvis e fai il setup

Nella cartella del vault (in Warp):

```powershell
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

## Step 9 — Installa Antigravity (uso quotidiano)

Antigravity è un IDE Google basato su VSCode con AI integrata. Lo useremo come **finestra principale dove tutto si parla**: editor + AI + terminale, tutto in uno.

1. Scarica da [labs.google.com/antigravity](https://labs.google.com/antigravity) la versione Windows
2. Esegui l'installer
3. Se Windows Defender / SmartScreen blocca: **Ulteriori informazioni** -> **Esegui comunque**
4. Avvia Antigravity dal menu Start
5. Login con account Google
6. Welcome screen: salta i tutorial Gemini, non ci servono adesso

### Apri il vault come progetto in Antigravity

1. **File -> Open Folder** (o `Ctrl+K Ctrl+O`)
2. Seleziona la cartella del vault
3. Conferma "Trust the authors"

### Apri il terminale embedded e lancia Claude Code

1. `View -> Terminal` oppure scorciatoia `` Ctrl+` `` (apice grave, in alto a sinistra sotto Esc)
2. Si apre un pannello terminale in basso
3. Verifica di essere nella cartella del vault con `pwd` (o `Get-Location`)
4. Lancia:

```powershell
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

## Troubleshooting Windows-specifico

**`obsidian: non riconosciuto come comando`**
Hai attivato la CLI in Obsidian ma non hai chiuso e riaperto Warp. Chiudi e riapri Warp.

**`Windows Defender / SmartScreen blocca un'installazione`**
È prudenza eccessiva di Windows con software scaricato da Internet. Clicca **Ulteriori informazioni** -> **Esegui comunque**. Tutti i software citati nella guida sono ufficiali e legittimi.

**`npm install -g` dà errore di permessi (EACCES o EPERM)**
Esegui Warp come amministratore: tasto destro sull'icona Warp dal menu Start -> **Esegui come amministratore**. Poi riprova `npm install -g @anthropic-ai/claude-code`.

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

**Le slash command non compaiono in Claude Code**
Hai lanciato `claude` fuori dalla root del vault. `cd` nella cartella del vault, poi rilancia `claude`.

**Jarvis non legge bene il vault**
Tre check:
1. Obsidian è aperto sul vault giusto?
2. `obsidian help` risponde dal terminale?
3. Claude Code è lanciato dalla root del vault?

Se vuoi una **rete di sicurezza** contro errori, prima di cominciare a lavorare:

```powershell
cd "<path-vault>"
git init
git add -A
git commit -m "Initial vault starter"
```

(Su Windows ti serve **Git for Windows** se non l'hai già: scarica da [git-scm.com](https://git-scm.com).) Da quel momento se Jarvis fa danni puoi tornare indietro con `git reset --hard HEAD`.

**PowerShell esegui-script bloccati (`execution policy`)**
Alcune installazioni o script PowerShell vengono bloccati per policy di default. Soluzione: apri PowerShell come amministratore una volta e dai:

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

Da quel momento sei a posto.

## Domande

Se ti si rompe qualcosa o un passaggio non torna, niente panico: ne parliamo a lezione e lo sistemiamo insieme.
