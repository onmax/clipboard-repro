# Nuxt Error Overlay Clipboard Fix

Fix for the copy button in Nuxt's error overlay failing because `navigator.clipboard` is undefined inside the `data:` URL iframe.

## Solution

Uses postMessage bridge to delegate clipboard operations to parent window (which has secure context).

```bash
pnpm install
pnpm dev
```

Visit http://localhost:3000 → error overlay appears → click copy button → works!

## Patch

See `patches/@nuxt__nitro-server.patch` - adds ~15 lines to:
1. Override `copyErrorMessage` in iframe to send postMessage
2. Register clipboard handler in parent before host check
