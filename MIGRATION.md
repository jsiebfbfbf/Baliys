# baileyz → @whiskeysockets/baileys Migration Guide

## What changed?

This project has been updated from the custom `baileyz` wrapper to the official
`@whiskeysockets/baileys` package (v7.0.0-rc.9).

## Files updated

| File | Change |
|------|--------|
| `package.json` | Removed `baileyz`, `libsignal`. Added `@whiskeysockets/baileys`, `dotenv` |
| `bot.js` | `require('baileyz')` → `require('@whiskeysockets/baileys')` |
| `lib/msg.js` | `require('baileyz')` → `require('@whiskeysockets/baileys')` |
| `plugins/main.js` | `require('baileyz')` → `require('@whiskeysockets/baileys')` |

## Setup steps

```bash
# 1. Install dependencies
npm install

# 2. Copy config template and fill in your details
cp config.env.example config.env
nano config.env

# 3. Start the bot
npm start
```

## Baileys v7 notes

- `makeWASocket` is still the default export — no change needed.
- `useMultiFileAuthState`, `DisconnectReason`, `Browsers`, `makeCacheableSignalKeyStore`,
  `jidNormalizedUser`, `downloadContentFromMessage`, `getContentType`, `proto`, `delay`
  — all still exported from the same package.
- Browser config array `["Ubuntu", "Chrome", "20.0.04"]` works as-is, or use
  `Browsers.ubuntu('Chrome')` for a more future-proof approach.
- Pairing code flow (`requestPairingCode`) works the same way.
- Session storage via `useMultiFileAuthState` is unchanged.

## Troubleshooting

**`Cannot find module '@whiskeysockets/baileys'`**
→ Run `npm install` again.

**Auth / QR loop after migration**
→ Delete your session folder (`rm -rf /tmp/session_*`) and pair again via `/code` endpoint.

**`newsletterReactMessage` not found**
→ This is already handled gracefully in `bot.js` with a `typeof` check.
