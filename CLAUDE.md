# بنت السبيت Calculator (Sibeet)

Standalone 4-player Hearts (بنت السبيت) score tracker PWA — sibling to baloot and konkan calculators in the الديوانية suite.

## Stack
- Single-file PWA (`index.html` ~750 lines)
- PeerJS v1.5.4 for P2P multiplayer (star topology)
- Firebase Realtime Database as scaling fallback when PeerJS broker is unavailable
- QRCode.js for room QR codes
- Service Worker (`sw.js`, cache `sibeet-v6`) for offline caching
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
| `index.html` | Calculator app (UI + game logic + P2P + Firebase) |
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
- **PeerJS mode** (default): host generates 4-digit code, viewers scan QR or enter code; ~8 viewer soft cap
- **Firebase mode** (auto-fallback): on PeerJS broker error, app silently switches to Firebase RTDB with `F-XXXX` code prefix, removing viewer cap
- **Viewers are read-only** — host's device is the single source of truth. Edit-access toggle was removed; the fallback makes per-session opt-in unnecessary
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
