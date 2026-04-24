# Azlan's Percussion Hub

A Progressive Web App for Azlan, a 7th grade percussion student at Scoggins Middle School in Frisco ISD.

## About

- Single-file PWA in `index.html` with UI, styling, and app logic.
- PIN-based cloud sync via JSONbin.io.
- Offline installable experience with `manifest.json` and `sw.js`.
- Includes practice tools for marimba, snare, metronome, timer, scales, rudiments, sight-reading, notes, concert checklist, glossary, lessons, progress, and reference recordings.

## Files

- `index.html` — main app shell, UI, audio engine, storage, sync, and app logic.
- `manifest.json` — PWA metadata.
- `sw.js` — service worker for offline caching.
- `CONTEXT.md` — development notes and app context.
- `SETUP_GUIDE.md` — setup instructions.
- `generate-icons.html` — helper page for icon generation.
- `icons/` — app icons.

## Setup

1. Replace `REPLACE_WITH_YOUR_JSONBIN_MASTER_KEY` in `index.html` with a JSONbin.io master API key.
2. Serve the folder over HTTPS or from GitHub Pages.
3. Open the app in a browser and enter a 6-digit PIN to sync data across devices.

## Deployment

This repo is configured for GitHub Pages at:

`https://sharjeelalikhan.github.io/azlan-percussion`
