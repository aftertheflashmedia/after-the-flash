# CLAUDE.md

Guidance for Claude (and other agents) working in this repository.

## This repo is PUBLIC

Anything committed here, including commit messages, PR titles and descriptions, code comments and docs, is visible to anyone.

- **Never** add client names, client addresses or other identifying client details.
- **Never** add pricing, rates, budgets, invoices or any other financial information.
- Never commit secrets. API keys (e.g. `RESEND_API_KEY`, `DISCORD_WEBHOOK_URL`) live in Vercel environment variables, and `.env*` files are gitignored.
- If a task would require adding any of the above, stop and ask first.

## Stack

| Layer | Tool |
|---|---|
| Framework | Next.js 16 (App Router, Turbopack) |
| UI | React 19 |
| Language | TypeScript |
| Styling | Global CSS design system in `app/globals.css` (no Tailwind or CSS-in-JS) |
| Fonts | Bodoni Moda + Archivo via `next/font/google` (`app/layout.tsx`) |
| Forms | `app/api/inquire/route.ts`, which emails inquiries via Resend |
| Deployment | Vercel, which auto-deploys on push to `main` |

Layout: pages are in `app/`, section components in `components/`, helpers in `lib/` and static media in `public/`.

## Commands

```bash
npm install       # or npm ci
npm run dev       # local dev server at http://localhost:3000
npm run lint      # ESLint (CI fails on errors; warnings are tolerated)
npm run build     # production build (also type-checks)
```

CI (`.github/workflows/ci.yml`) runs `npm ci`, `npm run lint` and `npm run build`. Run lint and build before opening a PR.

## Brand rules

The design concept is a modern art museum, where every photo is treated like a work of art on display.

### Palette

Use the CSS custom properties in `app/globals.css`, never hard-coded colors.

| Role | Token | Value |
|---|---|---|
| Warm cream (background) | `--cream`, `--cream-2` | `#F4EFE6`, `#ECE4D6` |
| Charcoal (text/ink) | `--ink`, `--ink-2`, `--ink-3` | `#1B1916`, `#57514A`, `#8A847B` |
| Dusty terracotta (accent) | `--terra` | `#B26450` |
| Hairlines | `--line`, `--line-2` | charcoal at 16% / 28% opacity |

Do not introduce new brand colors.

### Typography

- **Bodoni Moda** for display and headings (`--serif`).
- **Archivo** for body and UI text (`--sans`).
- Load fonts only through `next/font/google` in `app/layout.tsx`. Add no other font families.

### Copy

- The primary call to action reads **"Commission a Shoot"**. Never use "Book Now".
- Nav labels follow the live site. `components/Nav.tsx` is the source of truth, so reuse those labels exactly and don't invent synonyms. They are currently: The Collection, Before / After, The Work, The Gear, Pricing, Inquire.
- The voice is gallery and museum language ("collection", "commission", "the work"), not salesy.
