# Nuxt Error Overlay Clipboard Bug Reproduction

The copy button in Nuxt's error overlay fails because `navigator.clipboard` is undefined inside the `data:` URL iframe (opaque origin = not a secure context).

## Reproduce

```bash
pnpm install
pnpm dev
```

Visit http://localhost:3000 → error overlay appears → click copy button → check console for error.

## Root Cause

Nuxt's error overlay renders youch's error page inside a `data:` URL iframe. The `data:` URL has an opaque origin which is not considered a secure context, so `navigator.clipboard` is undefined.

## Fix

See `fix/nuxt-patch` branch for a pnpm patch that fixes this via postMessage bridge.
