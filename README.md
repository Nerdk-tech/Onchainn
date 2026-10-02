# Onchain Dapps — Static Site

Plain, readable source. No minification, no base64 blobs.
WalletConnect-inspired design language: near-black/white dual theme, blue accent (#3396ff), editorial serif headlines (Instrument Serif), Inter for UI text, pill buttons, centered layout.

## Structure

```
index.html          — the whole page (HTML + CSS in <style> + JS in <script>)
assets/
  fonts/            — self-hosted web fonts (offline-capable, no CDN)
  logos/            — real brand logos (full color) for the "Trusted by" section
```

## What's new in this pass

- Removed the "static demo" disclaimer line under Run Diagnostics.
- Full mobile pass — a `@media(max-width:600px)` block resizes type, padding and grids so the page no longer looks "zoomed in" on phones. Headline/section-title clamp() minimums were too large for narrow screens; now they scale down properly.
- Light/dark theme toggle (sun/moon button in the nav). Preference persists via localStorage and is applied before paint (no flash).
- Trusted-brands logos are real, full-color brand marks again (not silhouettes) with a soft blue glow + glass card, intensifying on hover.
- Features section redesigned: each card has its own accent color (blue / amber / teal / violet), a numbered tag (01–06), a colored top hairline and a soft corner glow — no longer six identical blue cards.

## How to edit

- **Colors** — CSS variables at the top of `<style>` (`--bg`, `--blue`, `--text`…). Light theme overrides live in the `html[data-theme="light"]` block right below.
- **Feature card accent** — each `.feat` div has an inline `style="--ac:...;--ac-soft:...;--ac-line:..."` — change those three values to recolor a single card.
- **Fonts** — files in `assets/fonts/`, wired via plain `@font-face` rules.
- **Logos** — drop a PNG into `assets/logos/` and add a `.logo-chip` line in the trusted section.
- **Prices / chart** — live CoinGecko + TradingView at view time, with static fallback values baked in for offline viewing.

## Button behavior (functional)

- Nav "Connect", hero "Connect Wallet ->", hero "Validate Wallet" — smooth-scroll to the Wallet Security Check section by default.
- "Run Diagnostics" — smooth-scroll to the Market Overview section.
- REDIRECTS — the team can add a link in EITHER of two ways, no JS knowledge needed:
  1. Direct href (works like any normal link): each button is a real `<a>` tag — just change its `href` (e.g. `<a class="btn btn-hero btn-primary" id="hero-connect" href="https://your-dapp.com">`).
  2. Config block: near the bottom of `index.html` find `BUTTON_LINKS` and set the button's URL (e.g. `"hero-connect": "https://your-link.com"`).
  Both do the same thing: the button opens that link in the same tab. If no URL is set, the button keeps its default smooth-scroll behavior.
- Theme toggle (sun/moon, nav) — light/dark, persisted via localStorage.

- "Connect" (nav) and "Connect Wallet →" / "Validate Wallet" (hero) — smooth-scroll to the Wallet Security Check section.
- "Run Diagnostics" — smooth-scroll to the Market Overview section.
- Theme toggle (sun/moon, nav) — light/dark, persisted via localStorage.

## Notes

- "Connect Wallet" / "Validate Wallet" / "Run Diagnostics" give tap feedback (status text + toast) by design — no redirects, modals or wallet connections.
- Keep `index.html` at the root with `assets/` next to it — deploy the whole folder to any static host.
