# Azlan Percussion Hub Development Memory

## Project Overview
- **App**: Single-file PWA for Azlan (7th grade percussion student, Scoggins Band, Frisco ISD)
- **Features**: 14 tabs (Home, Upload, Marimba, Snare, Metronome, Timer, Scales, Rudiments, Sight-Read, Notes, Concert, Glossary, Lessons, Progress, Reference)
- **Tech**: HTML/CSS/JS, Web Audio API, JSONbin.io PIN sync, Service Worker offline
- **Repo**: https://github.com/sharjeelalikhan/azlan-percussion (GitHub Pages deployment)

## Key Architecture Notes
- Audio engine: `unlockAudio()` synchronous, no async/await for timing
- PIN sync: Registry bin 'azlan-registry' maps PIN to binId for cross-device consistency
- Data persistence: `getPayload()` includes all state, saved to localStorage + JSONbin
- Fixed bugs: [[o1,g1]...].forEach outer brackets, loadLocal exists, metro uses setInterval

## Recent Changes (as of April 23, 2026)
- Added favicon (icons/icon-192.png)
- Implemented registry-based PIN sync for consistent cross-device bin mapping
- Secured renderNotes() against HTML injection by using DOM creation
- Added keyboard input for PIN entry (digits 0-9, Backspace, Enter)
- Fixed showPINScreen() button text consistency based on pinMode
- AI analysis has try-catch fallback for offline/network errors

## Current State
- Repo initialized with git, remote set, main branch pushed
- All fixes committed and deployed to GitHub Pages
- App ready for testing with JSONbin key replacement

## Next Steps
- Replace 'REPLACE_WITH_YOUR_JSONBIN_MASTER_KEY' in index.html with actual key
- Test PIN sync across devices
- Deploy to GitHub Pages if not already
- Monitor for any new bugs or feature requests

## Conversation History Summary
- Initial review of index.html, identified PIN sync issue and other minor bugs
- Set up git repo and pushed to GitHub
- Implemented all requested fixes
- Committed changes and pushed to main branch