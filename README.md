[README-ufop-si-tracker.md](https://github.com/user-attachments/files/26836520/README-ufop-si-tracker.md)
# UFOP SI — Study Progress Tracker

> Interactive checklist to track revision progress across the full Information Systems curriculum at UFOP — no backend, no dependencies, runs entirely in the browser.

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
![No dependencies](https://img.shields.io/badge/dependencies-none-2ea44f?style=flat-square)
![Offline ready](https://img.shields.io/badge/offline-ready-2ea44f?style=flat-square)

## Overview

A single-file web app that maps the complete 8-semester Information Systems curriculum (UFOP) into an interactive progress tracker. Each subject expands into individual topics — check them off as you review, and your progress is automatically saved to `localStorage` and persisted across sessions.

Built to be used personally during exam preparation — zero setup, just open the HTML file in any browser.

## Features

- **38 subjects across 8 semesters**, organized by academic period
- **Topic-level checkboxes** — granular progress per subject
- **Persistent state** via `localStorage` — progress survives page refresh and browser restarts
- **Global progress bar** — real-time percentage of topics reviewed across all subjects
- **Filter by category** — Computação, Matemática, Adm. e SI, Humanas, TCC
- **Search** — instant filter by subject name
- **Expand / Collapse all** — quick navigation
- **Reset** — wipe progress with confirmation dialog
- **Print-friendly** — CSS `@media print` expands all topics for offline study sheets

## Curriculum Coverage

| Category | Subjects | Highlights |
|---|---|---|
| Computação | 24 | Prog I (Python), Prog II (C#), AED I/II/III, SO, Redes, IA, SD |
| Matemática | 5 | Cálculo, GAAL, Discreta, Estatística, Prog. Linear |
| Adm. e SI | 5 | SI, Gestão da Informação, Economia, SAD, Empreendedorismo |
| Humanas | 3 | Informática e Sociedade, TGA, Comportamento Org. |
| TCC | 2 | TCC I (qualificação), TCC II (defesa) |

## Getting Started

No install, no build step.

```bash
# Clone or download the file
git clone https://github.com/vfiedlerc/ufop-si-tracker.git

# Open directly in browser
open roteiro_ufop_si.html
# or just double-click the file
```

> Works in any modern browser: Chrome, Firefox, Safari, Edge.

## How It Works

```
HTML file loaded
      │
      ▼
DATA array (38 subjects × topics) rendered into DOM
      │
      ▼
User checks a topic → toggleTopic()
      │
      ├─ updates progress{} object in memory
      ├─ saves to localStorage ('ufop_si_progress')
      ├─ updates subject progress bar (done/total)
      └─ updates global stats bar (% revisado)
```

State is keyed as `subjectId_topicIndex` and stored as a flat JSON object in `localStorage` — making it trivially portable and inspectable in DevTools.

## Customization

**Adding a new subject:**

```javascript
// In the DATA array, add an entry following this shape:
{
  id: 'p8c7',           // unique — period + sequential
  period: 8,            // semester number (1–8)
  cat: 'computacao',    // computacao | matematica | adm | humanas | tcc
  name: 'Subject Name',
  topics: [
    'Topic one',
    'Topic two',
    // ...
  ]
}
```

**Changing a category color:** edit the `CAT` object at the top of the `<script>` block — each entry has `bg`, `color`, `label`, and `bar` fields using hex values.

## Project Structure

Single-file architecture — everything lives in `roteiro_ufop_si.html`:

```
roteiro_ufop_si.html
├── <style>       CSS variables, layout, cards, progress bars, print styles
├── <body>        Static shell (header, stats bar, toolbar, legend)
└── <script>
    ├── CAT       Category metadata (colors, labels)
    ├── DATA      Full curriculum data (38 subjects)
    ├── render()  Builds the DOM from DATA + current filters
    ├── toggleTopic()   Handles checkbox state + localStorage save
    └── updateStats()   Recalculates global progress bar
```

## Context

Created to assist and help students of the Information Systems course at the Federal University of Ouro Preto, campus of the Institute of Exact and Applied Sciences.

---

*Zero dependencies. Zero build tools. Just open and study.*
