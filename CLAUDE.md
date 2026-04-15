# بنت السبيت Calculator (Sibeet)

Standalone 4-player Hearts (بنت السبيت) score tracker PWA — sibling to baloot and konkan calculators in the الديوانية suite.

## Stack
- Single-file PWA (`index.html` ~750 lines)
- Firebase Realtime Database for shared rooms (host broadcasts state, viewers mirror)
- QRCode.js for room QR codes
- Service Worker (`sw.js`, cache `sibeet-v15`) for offline caching
- Al Dewaniah visual identity (burgundy/gold/navy/cream, Cairo font)

## Commands
```bash
npx http-server . -p 8080    # Local dev server
```

## Live URL
https://ealhamed.github.io/sibeet-calculator/

## Files
| File | What |
|------|------|
| `index.html` | Calculator app (UI + game logic + Firebase rooms) |
| `sw.js` | Service worker (cache-first) |
| `manifest.json` | PWA manifest |
| `firebase.json` / `database.rules.json` / `.firebaserc` | Firebase RTDB config for `sibeet-calculator-al-dew` |
| `logo.png`, `icon-192.png`, `icon-512.png` | Branding |

## How It Works

### Game Rules
- 4 players, each collects penalty points per round
- **بنت السبيت (♠Q)**: 13 points (×2 = 26 if doubled)
- **١٠ ديمن (♦10)**: 10 points (×2 = 20 if doubled)
- **هاص (♥ hearts)**: 1 point each, 13 total per round
- First player to reach target (default 200) loses, lowest wins

### Player Cards
- Player name (tap to rename), running total, progress bar
- **♠Q toggle**: off → ×1 → ×2 → off
- **♦10 toggle**: same three-state pattern
- **♥ Hearts stepper**: SVG heart with count, global 13 limit enforced
- Round total preview (+N)

### Multiplayer (Room System)
- **Firebase-only**: host generates a 4-char code, viewers scan QR or enter the code. No viewer cap beyond Firebase quota.
- State model: `rooms/{code}` holds `state`, `editUnlocked`, `presence/{id}`, and `messages/{id}` (viewer→host round pushes when edit unlocked)
- Host writes full state on every broadcast; viewers mirror via `onValue`. `onDisconnect` removes room on host exit and presence entry on viewer exit.
- **Viewers are read-only** by default — host can toggle edit-unlock to let viewers push rounds
- Legacy `F-XXXX` links are still accepted on join (prefix stripped) for URL compatibility
- Firebase project: `sibeet-calculator-al-dew` (isolated 100-concurrent quota)

### Features
- Editable target (default 200), changeable any time
- Round history with highest scorer highlighted
- Game over ranking with medals
- In-app dialogs (`appConfirm`/`appPrompt`), dark mode, haptic feedback, accessibility (aria-pressed, aria-labels, role=radiogroup)
- Back button integration via `pushOverlay()` + popstate
- iOS Safari bottom-strip fix (html background)

## Menu
Links to all three sibling calculators (حاسبة بلوت / بنت السبيت / كنكان) in shared order.

## Repos
- **sibeet-calculator**: https://github.com/ealhamed/sibeet-calculator
- **Siblings**: [baloot-calculator](https://github.com/ealhamed/baloot-calculator), [konkan-calculator](https://github.com/ealhamed/konkan-calculator)
