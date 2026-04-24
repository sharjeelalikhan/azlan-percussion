# Azlan's Percussion Hub — Dev Context
## For continuing development in VS Code / Claude Code / new sessions

---

## What This App Is
A Progressive Web App (PWA) for Azlan — 7th grade percussionist at
Scoggins Middle School, Frisco ISD (Seahawks). Built as a single
`index.html` file (~1700 lines). Deployed to GitHub Pages.

**Live URL:** https://YOUR-USERNAME.github.io/azlan-percussion/
**Sync:** PIN-based via JSONbin.io free tier (no Google login — child account workaround)
**Offline:** Service worker (`sw.js`) caches the app shell

---

## File Structure
```
azlan-pwa/
├── index.html          ← entire app (HTML + CSS + JS, ~1700 lines)
├── manifest.json       ← PWA manifest (theme: #f5a623 orange)
├── sw.js               ← service worker (cache-first for app, network for JSONbin)
├── generate-icons.html ← open in Chrome to generate app icons
├── icons/
│   ├── icon-192.png
│   └── icon-512.png
└── SETUP_GUIDE.md
```

---

## 14 App Tabs
| Tab | ID | Key Feature |
|-----|-----|-------------|
| Home | home | Daily routine, goals, calendar |
| Upload | upload | Camera/file upload → AI analysis via Anthropic API |
| Marimba | marimba | Interactive marimba bars + etude playback |
| Snare | snare | Virtual snare pad + sticking patterns |
| Metronome | metro | Tap tempo, time sig, BPM presets |
| Timer | timer | Phase-based practice timer (3 routines) |
| Scales | scales | 7 flat scales, Circle of Fourths, mastery tracker |
| Rudiments | rudiments | 12 rudiments, tap to mark mastered |
| Sight-Read | sightread | Random rhythm pattern generator, 3 difficulty levels |
| Teacher Notes | notes | Persistent notepad, syncs via PIN |
| Concert | concert | UIL/concert checklist |
| Glossary | glossary | 40+ searchable music terms |
| Lessons | lessons | 8 expandable lesson cards |
| Progress | progress | Streak tracker, stats, practice log, milestones |
| Reference | reference | In-app etude player + YouTube links + listen log |

---

## Critical Architecture Notes

### Audio Engine (MUST READ before touching audio)
```javascript
// Audio context — lazy creation, synchronous resume
const AC = window.AudioContext || window.webkitAudioContext;
let ctx = null;

function gc() {
  if (!ctx) { try { ctx = new AC(); } catch(e) { return null; } }
  if (ctx.state === 'suspended') ctx.resume();
  return ctx;
}

function unlockAudio() {
  if (!ctx) { try { ctx = new AC(); } catch(e) {} }
  if (ctx && ctx.state === 'suspended') { ctx.resume(); }
}
```
**RULE:** Every button onclick that plays sound MUST call `unlockAudio()` first, synchronously, in the same click event. NO `.then()` on unlockAudio — it is synchronous.

**playNote lookahead:** `const t = when || (c.currentTime + 0.05)` — the 50ms offset ensures sound plays after any pending context resume.

### Known Fixed Bugs — DO NOT REINTRODUCE
1. `[[o1,g1],[o2,g2],[o3,g3]].forEach(...)` ← outer brackets REQUIRED (missing them = "not iterable" crash)
2. `function loadLocal()` must exist — was accidentally deleted in a refactor
3. `startMetro()` uses `setInterval(_metroBeat, ms)` — NO `.then()` chains
4. `unlockAudio()` is synchronous — never use `unlockAudio().then()`

### PIN Sync System
```javascript
// JSONbin.io free tier
// Each PIN gets its own private bin
// Key in index.html: const JSONBIN_KEY = '$2a$10$...'
// Auto-connects on load from localStorage.getItem('azlan_saved_pin')
```
Replace `REPLACE_WITH_YOUR_JSONBIN_MASTER_KEY` with actual key before deploying.

### Data Persistence
All state saved via `saveAll()` → localStorage (backup) + JSONbin (cloud sync).
Loaded via `applyPayload(data)` → calls `refreshAll()` to re-render all components.

```javascript
function getPayload() {
  return { sessionCount, sheetCount, scalePlays, practicedDays,
           practiceLog, teacherNotes, checkStates,
           scaleMastered: [...scaleMastered],
           masteredRuds: [...masteredRuds],
           milestones: MILESTONES.map(m=>m.done),
           listenLog };
}
```

---

## Design System (CSS Variables)
```css
--bg: #0a0f1e        /* dark navy background */
--surface: #111827   /* slightly lighter surface */
--card: #1a2235      /* card background */
--card2: #1e2a40     /* secondary card */
--border: #2a3a55    /* borders */
--accent: #f5a623    /* orange — primary accent */
--accent2: #4fc3f7   /* light blue — secondary accent */
--green: #4ade80     /* success / scales */
--red: #f87171       /* error / forte dynamics */
--purple: #c084fc    /* rudiment levels */
--text: #e2eaf8      /* primary text */
--text2: #8fa3c0     /* secondary text */
--text3: #4a6080     /* tertiary / muted */
```

---

## Curriculum Context (Scoggins Band, Frisco ISD)
- **Mallet Etude:** Quarter Note = 80, Presto, 8th notes throughout
- **Three audition levels:** Concert Band → Symphonic Band → Wind Ensemble
- **Scales required:** C, F, Bb, Eb, Ab, Db, Gb (Circle of Fourths, from memory)
- **Teacher goals:** Note Accuracy, Rebound Strokes, No Stopping
- **Daily routine:** 5-10min scales → 10-20min etude → 5min run-through
- **Key events:** UIL Concert & Sight-Reading (Spring), Region Auditions (Fall), Summer Band Camp June 1-4 2026
- **TMEA books:** Masterworks for Mallets (Gottlieb), Intermediate Snare Drum Studies (Peters)
- **Percussion director:** Ms. Pedersen (Assistant), Mr. Davis (Director)

---

## Responsive Breakpoints
```css
@media(min-width:901px)  /* desktop — more padding */
@media(max-width:768px)  /* tablet */
@media(max-width:480px)  /* mobile */
@media(max-width:360px)  /* small phones */
```

---

## How to Update on GitHub
1. Edit index.html in VS Code
2. Go to github.com → your repo → click index.html → pencil icon ✏️
3. Select all → paste new content → Commit changes
4. Wait 2 min → hard refresh on all devices (Ctrl+Shift+R)

---

## Parent/Student Info
- Student: Azlan, 7th grade, Scoggins Middle School, McKinney TX 75070
- School: Scoggins Middle School Seahawks, Frisco ISD
- Percussion: Marimba primary, Snare secondary
- Sync PIN: [write Azlan's 6-digit PIN here]
- GitHub URL: https://YOUR-USERNAME.github.io/azlan-percussion/
