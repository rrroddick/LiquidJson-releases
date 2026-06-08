<div align="center">

<img src="128x128@2x.png" width="120" alt="LiquidJson icon" />

# LiquidJson

**A blazing-fast desktop app for exploring large JSON files.**

[![Version](https://img.shields.io/github/v/release/rrroddick/LiquidJson-releases?style=flat-square&color=violet&label=version)](https://github.com/rrroddick/LiquidJson-releases/releases/latest)
[![Tauri](https://img.shields.io/badge/Tauri-2-blue?style=flat-square&logo=tauri)](https://tauri.app)
[![Rust](https://img.shields.io/badge/Rust-1.77+-orange?style=flat-square&logo=rust)](https://www.rust-lang.org)
[![React](https://img.shields.io/badge/React-18-61DAFB?style=flat-square&logo=react)](https://react.dev)
[![Platform](https://img.shields.io/badge/platform-macOS%20%7C%20Windows-lightgrey?style=flat-square)](https://github.com/rrroddick/LiquidJson-releases/releases)
[![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)](LICENSE)

---

[Features](#-features) · [Installation](#-installation) · [Usage](#-usage) · [Tech Stack](#-tech-stack) · [Build from source](#️-build-from-source) · [Italiano](#-italiano)

</div>

---

## ✨ Features

| | |
|---|---|
| 🚀 **Lightning fast** | Opens a 55 MB file in ~0.5 s. Built with SIMD-accelerated JSON parsing (sonic-rs) and mimalloc |
| 📦 **Huge file support** | Handles big files without breaking a sweat |
| 🧾 **JSON & NDJSON** | Opens standard JSON plus NDJSON / JSON Lines (`.ndjson`, `.jsonl`) — auto-detected, with each record shown as an item of the root array |
| 🖥️ **60 fps scrolling** | Virtual DOM — only ~40 rows rendered at any time, no matter how large the file |
| 🔍 **Instant search** | Search keys and values in real time, navigate results with ←/→ arrows |
| 🎯 **Scoped search** | Restrict matching to keys only, values only, or both (`k:v` chip) |
| 🌳 **Filter view** | Switch results to a tree pruned to matches, their ancestors, and the containing object's other fields — see hits in context |
| 🧬 **Regex search** | Toggle `.*` to match keys and values with case-insensitive regular expressions |
| 📋 **Smart clipboard** | Copy key, value, path — with or without surrounding quotes |
| ✅ **Multi-select** | Cmd/Ctrl+click to select multiple nodes, then copy all their keys or values (⌘/Ctrl+C or the context menu) — or delete them all at once |
| ✏️ **Edit & save** | Edit any leaf value or object key in place, then **Save** / **Save As** to disk |
| ➕ **Add & edit nodes** | Right-click a container → **Add field… / Add item…** to insert a scalar, an empty `{}` / `[]`, or a whole nested object/array; the same goes for editing a value |
| 🗑️ **Delete nodes** | Right-click → **Delete** to remove a node and its whole subtree (with a confirm) |
| 📤 **Export as JSON** | Right-click any node to save that subtree to a `.json` file (streamed straight to disk) |
| 📂 **Recent files** | Quick access to the last 8 opened files |
| ⌨️ **Full keyboard navigation** | Arrow keys, Enter, Space, Home/End — no mouse needed |
| 🖱️ **Context menu** | Right-click for edit value, delete, expand/collapse subtree, copy options, export, show details |
| 📐 **Detail panel** | Resizable side panel showing type, path, depth, children and full value; follows the node you click while open |
| 📎 **Paste to open** | Paste any JSON directly from the clipboard — no file needed |
| 🗂️ **Drag & drop** | Drop a `.json`, `.ndjson` or `.jsonl` file anywhere on the window to open it |
| 🎨 **Liquid Glass UI** | Apple-inspired frosted glass interface with smooth animations |
| 🌗 **Light / dark / system** | Switch theme manually or follow the OS — your choice is remembered |
| 💧 **Toggle liquid glow** | Turn the pointer-reactive glass glow on/off from the toolbar — your choice is remembered |
| 🔄 **Auto-update** | Checks GitHub Releases on launch and installs new signed versions in the background, then relaunches |

---

## 📥 Installation

Download the [**latest release**](https://github.com/rrroddick/LiquidJson-releases/releases/latest) and grab the file for your platform:

| Platform | File |
|---|---|
| macOS (Apple Silicon) | the `…_aarch64.dmg` |
| Windows | the `…_x64-setup.exe` |

After the first install, the app **updates itself**: on launch it checks for a newer release and, if found, downloads + verifies + installs it, then relaunches.

---

## 🧭 Usage

### Opening a file

- Click **Open JSON** in the toolbar and select a `.json`, `.ndjson` or `.jsonl` file
- Or **drag & drop** a `.json`, `.ndjson` or `.jsonl` file anywhere on the window
- NDJSON / JSON Lines is **auto-detected** (from any source, paste included) — each line becomes an item of the root array
- Or **paste JSON** directly from the clipboard (`Cmd+V` / `Ctrl+V`)
- Or pick from **Recent files** (clock icon)

### Navigating the tree

| Action | Shortcut |
|---|---|
| Focus tree | Click on tree area |
| Move up / down | `↑` / `↓` |
| Expand node | `→` or `Enter` |
| Collapse node | `←` or `Enter` |
| Show detail panel | `Space` |
| Add / remove from multi-selection | `Cmd`/`Ctrl` + click |
| First / last row | `Home` / `End` |

### Searching

| Action | Shortcut |
|---|---|
| Focus search bar | `Cmd+F` / `Ctrl+F` |
| Next result | `Enter` |
| Previous result | `Shift+Enter` (or ← button) |
| Toggle regex | `.*` button in the search bar |
| Clear search | `Escape` |

Regex is case-insensitive; an invalid pattern shows a red border while you type.

- **Scope** — the chip next to `.*` cycles where the query is tested: `k:v` (keys & values, default) → `key` → `val`.
- **List vs filter view** — the segmented toggle switches between a flat ranked **list** of matches and a **filter** view: the document tree pruned to the matches, their ancestors, and each match's siblings (the other fields of the object that contains it), so you see hits in their structural context. Sibling objects/arrays are shown collapsed — click one to expand it within the filter and reveal its contents. Clearing the search restores the previous tree exactly.

### Editing & saving

- Open the **detail panel** for a node (`Space`, "Show details", or "Edit value…" from the context menu).
- Click the **pencil** next to the value to edit any node — a leaf *or* a whole object/array (its JSON is prefilled); type any JSON value and press `⌘/Ctrl+Enter` to save, `Esc` to cancel. The pencil next to the key renames an object member.
- **Delete** a node and its whole subtree from the context menu (with a confirm). It can't be undone except by reloading the file — your changes only hit disk when you **Save**.
- A **dot** on the **Save** button marks unsaved edits. Use **Save** to write back to the open file, or **Save As…** to choose a new path (also used for pasted JSON). Saving streams straight to disk.
- ⚠️ Saving reformats the file (pretty-printed, 2-space indent).

### Appearance

- **Theme** — cycle **light → dark → system** with the sun/moon/monitor button in the toolbar. "System" follows the OS live; your choice is remembered.
- **Liquid glow** — toggle the pointer-reactive glass highlight with the **💧 droplet** button. On by default and remembered between sessions.

### Context menu (right-click)

- **Show details** — opens the detail side panel
- **Edit value… / Edit JSON…** — edit a leaf's value, or a whole object/array, in the detail panel
- **Copy N keys / Copy N values / Copy N plain values** — when several nodes are multi-selected (Cmd/Ctrl+click), copy all their keys, raw values, or unquoted values at once (newline-separated, document order)
- **Copy key** — the object-member key
- **Copy value / Copy plain value** — with or without surrounding quotes
- **Copy path** — dot-notation path to the node
- **Add field… / Add item…** — on a container, insert a new child: a JSON scalar, an empty `{}` / `[]`, or a full nested object/array (paste it in); objects ask for a key
- **Expand / Collapse subtree** — recursively expand or collapse
- **Export as JSON…** — save this node's subtree to a `.json` file
- **Delete** — remove this node and its whole subtree (with a confirm)
- **Delete N nodes** — with a multi-selection (Cmd/Ctrl+click), remove all the selected nodes at once (with a confirm)

---

## 🛠 Tech Stack

<div align="center">

| Layer | Technology |
|---|---|
| Desktop shell | [Tauri 2](https://tauri.app) |
| Backend language | Rust 1.77+ |
| JSON parser | [sonic-rs](https://github.com/cloudwego/sonic-rs) (SIMD) |
| Memory allocator | [mimalloc](https://github.com/microsoft/mimalloc) |
| Frontend framework | React 18 + TypeScript |
| Virtualisation | [@tanstack/react-virtual](https://tanstack.com/virtual) |
| Styling | Tailwind CSS v3 |
| Build tool | Vite 6 |

</div>

### How it works

```
┌──────────────────────────────────────────────────────┐
│                    Tauri Window                      │
│  ┌──────────────┐        ┌──────────────────────┐   │
│  │  React / TS  │  IPC   │   Rust backend       │   │
│  │  (Vite)      │◄──────►│                      │   │
│  │              │        │  • sonic-rs parser    │   │
│  │  Virtual     │        │  • Flat Vec<JsonNode> │   │
│  │  scroll      │        │  • Range-based IPC    │   │
│  │  ~40 DOM     │        │  • Recent files store │   │
│  │  nodes       │        │  • Native clipboard   │   │
│  └──────────────┘        └──────────────────────┘   │
└──────────────────────────────────────────────────────┘
```

The entire JSON is parsed into a **flat `Vec<JsonNode>`** in a single streaming pass — no intermediate `serde_json::Value` is ever created. The frontend requests only the visible slice via range-based IPC, so memory stays low even for gigabyte files.

---

## ⚙️ Build from source

### Prerequisites

- [Rust](https://rustup.rs) 1.77+
- [Node.js](https://nodejs.org) 18+
- [Tauri prerequisites](https://tauri.app/start/prerequisites/) for your OS

### Steps

```bash
# Clone
git clone https://github.com/rrroddick/LiquidJson.git
cd LiquidJson

# Install JS dependencies
npm install

# Dev mode (hot reload)
npm run tauri dev

# Production build
npm run tauri build
```

The production `.app` / `.exe` will be in `src-tauri/target/release/bundle/`.

---

## 🤝 Contributing

Issues and pull requests are welcome. Please open an issue first to discuss major changes.

---

<br />
<br />

---

<div align="center">

# 🇮🇹 Italiano

<img src="128x128@2x.png" width="80" alt="LiquidJson icon" />

**Un'app desktop velocissima per esplorare file JSON di grandi dimensioni.**

</div>

---

## ✨ Funzionalità

| | |
|---|---|
| 🚀 **Velocità estrema** | Apre un file da 55 MB in ~0,5 s grazie al parser JSON SIMD (sonic-rs) e mimalloc |
| 📦 **Supporto per file grandi** | Nessun limite pratico alle dimensioni del file |
| 🧾 **JSON e NDJSON** | Apre JSON standard più NDJSON / JSON Lines (`.ndjson`, `.jsonl`) — rilevati automaticamente, con ogni record mostrato come elemento dell'array radice |
| 🖥️ **Scroll a 60 fps** | DOM virtuale — solo ~40 righe renderizzate contemporaneamente |
| 🔍 **Ricerca istantanea** | Cerca chiavi e valori in tempo reale, naviga i risultati con le frecce |
| 🎯 **Ricerca per ambito** | Limita il match alle sole chiavi, ai soli valori, o a entrambi (chip `k:v`) |
| 🌳 **Vista filtrata** | Mostra i risultati come albero ridotto ai match, ai loro antenati e agli altri campi dell'oggetto che li contiene — risultati nel contesto |
| 🧬 **Ricerca regex** | Attiva `.*` per cercare chiavi e valori con espressioni regolari (case-insensitive) |
| 📋 **Clipboard intelligente** | Copia chiave, valore, percorso — con o senza virgolette |
| ✅ **Selezione multipla** | Cmd/Ctrl+click per selezionare più nodi, poi copia tutte le loro chiavi o valori (⌘/Ctrl+C o dal menu contestuale) — oppure eliminali tutti in un colpo |
| ✏️ **Modifica e salva** | Modifica il valore di una foglia o la chiave di un oggetto, poi **Salva** / **Salva con nome** su disco |
| ➕ **Aggiungi e modifica nodi** | Tasto destro su un container → **Add field… / Add item…** per inserire uno scalare, un `{}` / `[]` vuoto o un intero oggetto/array annidato; lo stesso vale modificando un valore |
| 🗑️ **Elimina nodi** | Tasto destro → **Delete** per rimuovere un nodo e tutto il suo sottoalbero (con conferma) |
| 📤 **Esporta in JSON** | Tasto destro su un nodo per salvarne il sottoalbero in un file `.json` (scritto in streaming su disco) |
| 📂 **File recenti** | Accesso rapido agli ultimi 8 file aperti |
| ⌨️ **Navigazione da tastiera** | Frecce, Invio, Spazio, Home/End |
| 🖱️ **Menu contestuale** | Tasto destro per modificare il valore, eliminare, espandere/comprimere sottoalberi, copiare, esportare, mostrare dettagli |
| 📐 **Pannello dettagli** | Pannello laterale ridimensionabile con tipo, percorso, profondità, figli e valore completo; mentre è aperto segue il nodo che clicchi |
| 📎 **Incolla per aprire** | Incolla qualsiasi JSON dagli appunti — senza bisogno di un file |
| 🗂️ **Drag & drop** | Trascina un file `.json`, `.ndjson` o `.jsonl` in qualsiasi punto della finestra per aprirlo |
| 🎨 **UI Liquid Glass** | Interfaccia in stile frosted glass ispirata ad Apple |
| 🌗 **Chiaro / scuro / sistema** | Cambia tema manualmente o segui l'OS — la scelta viene ricordata |
| 💧 **Interruttore liquid glow** | Attiva/disattiva il bagliore del vetro reattivo al cursore dalla toolbar — la scelta viene ricordata |
| 🔄 **Aggiornamento automatico** | All'avvio controlla le Release su GitHub e installa in background le nuove versioni firmate, poi riavvia |

---

## 📥 Installazione

Scarica l'[**ultima release**](https://github.com/rrroddick/LiquidJson-releases/releases/latest) e prendi il file per la tua piattaforma:

| Piattaforma | File |
|---|---|
| macOS (Apple Silicon) | il `…_aarch64.dmg` |
| Windows | il `…_x64-setup.exe` |

Dopo la prima installazione l'app **si aggiorna da sola**: all'avvio verifica se c'è una release più recente e, se la trova, la scarica + verifica + installa, poi si riavvia.

---

## 🧭 Utilizzo

### Aprire un file

- Clicca **Open JSON** nella toolbar e seleziona un file `.json`, `.ndjson` o `.jsonl`
- Oppure **trascina** un file `.json`, `.ndjson` o `.jsonl` in qualsiasi punto della finestra
- NDJSON / JSON Lines viene **rilevato automaticamente** (da qualsiasi origine, incolla compreso) — ogni riga diventa un elemento dell'array radice
- Oppure **incolla il JSON** dagli appunti (`Cmd+V` / `Ctrl+V`)
- Oppure seleziona dalla lista dei **file recenti** (icona orologio)

### Navigare l'albero

| Azione | Scorciatoia |
|---|---|
| Muoversi su / giù | `↑` / `↓` |
| Espandere un nodo | `→` o `Invio` |
| Comprimere un nodo | `←` o `Invio` |
| Mostrare il pannello dettagli | `Spazio` |
| Aggiungere / togliere dalla selezione multipla | `Cmd`/`Ctrl` + click |
| Prima / ultima riga | `Home` / `End` |

### Cercare

| Azione | Scorciatoia |
|---|---|
| Focalizzare la barra di ricerca | `Cmd+F` / `Ctrl+F` |
| Risultato successivo | `Invio` |
| Risultato precedente | pulsante ← |
| Attivare regex | pulsante `.*` nella barra |
| Cancellare la ricerca | `Escape` |

La regex è case-insensitive; un pattern non valido mostra un bordo rosso mentre digiti.

- **Ambito** — il chip accanto a `.*` cicla dove viene testata la query: `k:v` (chiavi e valori, default) → `key` → `val`.
- **Vista lista vs filtro** — il toggle segmentato passa da una **lista** piatta di risultati a una **vista filtrata**: l'albero ridotto ai match, ai loro antenati e ai fratelli del match (gli altri campi dell'oggetto che lo contiene), per vedere i risultati nel loro contesto strutturale. Gli oggetti/array fratelli sono mostrati collassati — cliccane uno per espanderlo dentro il filtro e vederne il contenuto. Cancellando la ricerca l'albero precedente viene ripristinato esattamente.

### Modifica e salvataggio

- Apri il **pannello dettagli** di un nodo (`Spazio`, "Show details", o "Edit value…" dal menu contestuale).
- Clicca la **matita** accanto al valore per modificare qualsiasi nodo — una foglia *o* un intero oggetto/array (il suo JSON viene precompilato); digita un qualsiasi valore JSON e premi `⌘/Ctrl+Invio` per salvare, `Esc` per annullare. La matita accanto alla chiave rinomina un membro di oggetto.
- **Elimina** un nodo e tutto il suo sottoalbero dal menu contestuale (con conferma). Non è annullabile se non ricaricando il file — le modifiche finiscono su disco solo quando fai **Salva**.
- Un **pallino** sul pulsante **Salva** segnala modifiche non salvate. Usa **Salva** per riscrivere il file aperto, o **Salva con nome…** per scegliere un nuovo percorso (usato anche per il JSON incollato). Il salvataggio avviene in streaming su disco.
- ⚠️ Il salvataggio riformatta il file (pretty-print, indentazione di 2 spazi).

### Aspetto

- **Tema** — cicla **chiaro → scuro → sistema** con il pulsante sole/luna/monitor nella toolbar. "Sistema" segue l'OS in tempo reale; la scelta viene ricordata.
- **Liquid glow** — attiva/disattiva il bagliore del vetro reattivo al cursore con il pulsante **💧 goccia**. Attivo di default e ricordato tra le sessioni.

### Menu contestuale (tasto destro)

- **Show details** — apre il pannello laterale con i dettagli del nodo
- **Edit value… / Edit JSON…** — modifica il valore di una foglia, o un intero oggetto/array, nel pannello dettagli
- **Copy N keys / Copy N values / Copy N plain values** — con più nodi selezionati (Cmd/Ctrl+click), copia in un colpo le chiavi, i valori raw o i valori senza virgolette (separati da newline, in ordine di documento)
- **Copy key** — la chiave del membro dell'oggetto
- **Copy value / Copy plain value** — con o senza virgolette
- **Copy path** — percorso dot-notation fino al nodo
- **Add field… / Add item…** — su un container, inserisce un nuovo figlio: uno scalare JSON, un `{}` / `[]` vuoto, o un oggetto/array annidato completo (incollalo); per gli oggetti chiede una chiave
- **Expand / Collapse subtree** — espandi o comprimi ricorsivamente
- **Export as JSON…** — salva il sottoalbero del nodo in un file `.json`
- **Delete** — rimuove questo nodo e tutto il suo sottoalbero (con conferma)
- **Delete N nodes** — con una selezione multipla (Cmd/Ctrl+click), rimuove tutti i nodi selezionati in un colpo (con conferma)

---

## ⚙️ Compilare dal sorgente

### Prerequisiti

- [Rust](https://rustup.rs) 1.77+
- [Node.js](https://nodejs.org) 18+
- [Prerequisiti Tauri](https://tauri.app/start/prerequisites/) per il tuo sistema operativo

### Passaggi

```bash
# Clona il repository
git clone https://github.com/rrroddick/LiquidJson.git
cd LiquidJson

# Installa le dipendenze JS
npm install

# Modalità sviluppo (hot reload)
npm run tauri dev

# Build di produzione
npm run tauri build
```

L'`.app` / `.exe` di produzione si troverà in `src-tauri/target/release/bundle/`.

---

<div align="center">

Made with ❤️ using [Tauri](https://tauri.app), [React](https://react.dev) and [Claude](https://claude.ai)

</div>
