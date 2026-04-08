# بنت السبيت Calculator (Sibeet)

Standalone 4-player Hearts (بنت السبيت) score tracker PWA with P2P multiplayer.

## Stack
- Single-file PWA (`index.html` ~750 lines)
- PeerJS v1.5.4 for P2P multiplayer
- QRCode.js for room QR codes
- Service Worker (`sw.js`) for offline caching
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
| `index.html` | بنت السبيت calculator |
| `sw.js` | Service worker (cache-first) |
| `manifest.json` | PWA manifest |
| `logo.png` | Al Dewaniah logo |
| `icon-192.png`, `icon-512.png` | PWA icons |

## How It Works

### Game Rules
- 4 players, each collects penalty points per round
- **بنت السبيت (♠Q)**: 13 points (or 26 if doubled)
- **١٠ ديمن (♦10)**: 10 points (or 20 if doubled)
- **هاص (♥ hearts)**: 1 point each, 13 total per round
- First player to reach the target (default 200) loses
- Lowest score wins

### Player Cards
- Player name (tap to rename), running total, progress bar
- **♠Q toggle**: off → ×1 → ×2 → off
- **♦10 toggle**: same 3-state
- **♥ Hearts stepper**: SVG heart with count, global 13 limit
- Round total preview (+N)

### Features
- Editable target (default 200), changeable any time
- Round history with highest scorer highlighted
- Game over ranking with medals
- P2P rooms (PeerJS WebRTC) with host edit lock
- In-app dialogs, dark mode, haptic feedback, accessibility

## Related
- **Baloot Calculator**: https://github.com/ealhamed/baloot-calculator
