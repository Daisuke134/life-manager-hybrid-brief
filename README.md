# Life Manager — Hybrid Daily Brief

A daily briefing that drafts privately **on-device** and polishes in the **cloud**, built with **Firebase AI Logic** for the #BuildHybridAI 2026 hackathon (Firebase / Google / Devpost).

**Live demo:** https://daisuke134.github.io/life-manager-hybrid-brief/

## What it does

Paste the day's private notes and schedule. The app:

1. Runs a first pass that prefers **on-device** inference (Firebase AI Logic `PREFER_ON_DEVICE` — Gemini Nano on Chrome / Apple Foundation Models on iOS) to draft a private summary locally.
2. Runs a **cloud** pass (Firebase AI Logic `ONLY_CLOUD` — Gemini) to turn the material into a structured daily briefing: schedule first, then one focus block, then a short closing review prompt.
3. Labels every section with the route that produced it, so the hybrid behavior is visible — not hidden.

If the SDK build in the browser does not expose an on-device mode, the route label says so honestly and the call runs in the cloud.

## How it is built

- Single-page Web app (`index.html`), no build step.
- Firebase AI Logic SDK (firebase-ai v12.5.0, loaded from gstatic) is imported and **actually called at runtime** via `getGenerativeModel(...).generateContent(...)`, with the Gemini Developer API backend.
- Firebase App Check is enabled: reCAPTCHA Enterprise (Fraud Defense) on production hosts, the official Debug Provider on localhost.
- Deterministic local fallback exists only as a clearly labeled PROTOTYPE path for offline development; the submitted demo uses the live SDK call.

## Run it locally

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

On localhost the App Check debug token printed in the browser console must be registered in Firebase Console > App Check > Apps > Manage debug tokens for live calls to succeed.

## License

MIT — see `LICENSE`.
