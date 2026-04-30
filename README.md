<div align="center">

<img src="system/static/horce-logo.png" alt="HORCE Logo" width="180"/>

# HORCE - Compliance Manager

**Gestione intelligente di documenti DUVRI e RAMS per la sicurezza sul lavoro**

[![Python](https://img.shields.io/badge/Python-3.8%2B-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org)
[![Flask](https://img.shields.io/badge/Flask-3.0-000000?style=flat-square&logo=flask&logoColor=white)](https://flask.palletsprojects.com)
[![SQLite](https://img.shields.io/badge/SQLite-3-003B57?style=flat-square&logo=sqlite&logoColor=white)](https://sqlite.org)
[![Version](https://img.shields.io/badge/Versione-2.0-brightgreen?style=flat-square)](.)

*Smetti di cercare file su cartelle di rete. Smetti di perdere tempo con Excel. Inizia ad avere controllo reale.*

</div>

---

## • Il Problema

Gestire la compliance documentale di decine di aziende appaltatrici su cartelle di rete è un incubo.

- 📂 Migliaia di file sparsi in cartelle annidate, senza una vista unificata
- 🕵 Chi ha caricato questo file? Quando? Nessuna traccia
- 📋 RAMS e DUVRI approvati da chi? Con quale workflow? Solo email sparse
- 👷 I lavoratori hanno tutti i documenti in regola? Aprendo ogni cartella manualmente

**HORCE risolve tutto questo** con una web app moderna locale, zero cloud, zero costi.

---

## ✨ Funzionalità

### ▸ Dashboard Aziendale
Panoramica istantanea di tutte le aziende. Status documenti in tempo reale, ricerca rapida, badge per criticità. Aggiornamento automatico ogni 3 minuti.

### ▸ Verifica Compliance Documenti
Per ogni azienda, HORCE sa cosa c’è, cosa manca e cosa è scaduto.

- **Documenti azienda**: Allegati, CCIAA, DURC, DUVRI, RAMS
- **Documenti lavoratori**: Preposti, DPI, Formazione
- Viewer PDF integrato nella pagina

### ▸ Gestione Progetti RAMS/DUVRI
Workflow approvazione a doppio livello:

1. Il contractor carica RAMS + DUVRI
2. **RME** (Regional Manager) approva la parte tecnica  
3. **WHS** (Safety Technician) approva la parte sicurezza
4. Rigetto: motivazione obbligatoria, eliminazione automatica file, log completo

### ▸ Scanner Multi-Thread
Scansione intera struttura cartelle in **2-3 minuti** con 8 thread paralleli.
~7.000 file indicizzati con metadata completo: owner, data, dimensione.

### ▸ Autenticazione & Ruoli

| Ruolo | Accesso |
|-------|---------|
| **Admin** | Tutto: utenti, log, configurazione |
| **User (WHS)** | Dashboard, documenti, approvazioni WHS |
| **RME** | Dashboard, documenti, approvazioni RME |
| **Contractor** | Solo la propria azienda |

### ▸ Analytics & Reporting
- KPI compliance per azienda e tipo documento
- Top aziende per criticità, grafici interattivi
- Export CSV log attività

---

## ▶ Avvio Rapido

**30 secondi per partire:**

Doppio click su Avvia_HORCE.bat — installa dipendenze e apre il browser automaticamente.

Oppure manuale:

```bash
cd system
pip install -r requirements.txt
python app.py
# http://localhost:5000
```

Credenziali default: `admin` / `admin2026`

> ⚠ Cambia la password al primo accesso.

---

## ▣ Architettura

```
HORCE/
+-- Avvia_HORCE.bat           <- One-click launcher
+-- system/
    +-- app.py                <- Flask backend
    +-- database.py           <- SQLite (sync rete/locale)
    +-- scanner.py            <- Scanner multi-thread
    +-- document_checker.py   <- Logica compliance
    +-- auth_helpers.py       <- Autenticazione + ruoli
    +-- duvri.db              <- Database SQLite
    +-- templates/            <- 13 template HTML moderni
    +-- static/               <- CSS + assets
    +-- owner scanner/        <- Tool metadata file owner
```

### ▸ Stack Tecnico

| Layer | Tecnologia |
|-------|-----------|
| Backend | Python 3.8+ · Flask 3.0 |
| Database | SQLite 3 con sync rete/locale automatico |
| Frontend | HTML5 · CSS3 · JavaScript vanilla |
| Scanner | concurrent.futures ThreadPoolExecutor (8 worker) |
| Auth | Werkzeug bcrypt · Flask sessions |
| Scheduler | APScheduler (auto-refresh background) |
| Reporting | openpyxl · pandas |

---

## ⚿ Sicurezza

- Password hashate (Werkzeug bcrypt)
- Nuovi utenti **disattivati per default** — abilitazione manuale da admin
- Controllo permessi role-based su ogni endpoint API
- Audit trail completo: chi, cosa, quando
- Upload solo PDF max 20MB, validazione server-side
- Server locale — non esposto a internet

---

## ⚡ Performance

| Operazione | Tempo | Dettagli |
|-----------|-------|---------|
| Scansione completa | ~2-3 min | 8 thread · ~7.000 file |
| Auto-refresh silenzioso | ~1-2 min | Background ogni 3 minuti |
| Verifica singola azienda | < 1 sec | Cache database locale |
| Upload file | < 2 sec | Validazione + copia su rete |

---

## ⚙ Configurazione

```python
ROOT_PATH = r"\server\rete\percorso"  # Cartella root da scansionare
MAX_WORKERS = 8                          # Thread paralleli scanner
REFRESH_INTERVAL = 180                   # Secondi tra auto-refresh
```

---

## ◆ Requisiti

- Python 3.8+ (consigliato 3.11)
- Accesso lettura/scrittura alla cartella di rete
- Windows (owner detection via win32security)
- Browser moderno (Chrome, Edge, Firefox)

---

## ★ Changelog

### v2.0 — Marzo 2026
- ✅ Autenticazione multi-ruolo (Admin, User, RME, Contractor)
- ✅ Gestione progetti RAMS/DUVRI con workflow approvazioni
- ✅ Doppio livello approvazione RME + WHS
- ✅ Rigetto con motivazione + cleanup automatico
- ✅ Owner detection file
- ✅ Sync DB rete/locale con conflict resolution

### v1.0 — Febbraio 2026
- Scanner multi-thread base
- Dashboard aziende
- Export Excel/JSON

---

## ◉ Autore

**Mirkoglo** — HSE Manager & HORCE Project Author

Costruito per risolvere un problema reale, testato sul campo con 230+ aziende e 1.200+ lavoratori.

---

*Se gestisci compliance documentale su cartelle di rete e hai perso il conto di quante volte hai cercato un file manualmente — questo progetto è per te.*
