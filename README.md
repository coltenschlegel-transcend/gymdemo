# Gymfinity Co. — Demo Site

A single-page marketing site for **Gymfinity Co.**, a fictional athleisure brand (“Athleisure for Urban Millennials”). This repo is set up as a demo environment for testing privacy and consent tooling (e.g. [Transcend](https://transcend.io)) with a realistic landing page and multiple third-party trackers.

## What’s in the repo

- **`gymdemo/`** — Demo site and scripts
  - **`gymfinity_co_index.html`** — Main landing page (hero, features, collections, reviews, email signup, footer)
  - **`trackers.js`** — Third-party tracker loader used by the page (loads on `DOMContentLoaded`)
  - **`scripts/trackers.js`** — Alternate/expanded tracker bundle (GA4, Meta, Mixpanel, FullStory, Heap, Snap, Reddit, Profitwell, Pinterest, Sentry, etc.) with placeholder IDs for detection only

## Tech stack

- **Frontend:** Vanilla HTML, CSS, and JavaScript (no build step)
- **Fonts:** [Inter](https://fonts.google.com/specimen/Inter) via Google Fonts
- **Privacy/consent:** Transcend (Airgap script) with:
  - Tracker overrides for **Google Consent Mode** and **Facebook LDU**
  - Privacy Center link and “Cookie preferences” (re-opens Transcend consent manager)
- **Trackers:** Demo placeholders for GA4, Google Ads, Meta Pixel, Mixpanel, FullStory, Heap, Snap, Reddit, Profitwell, Pinterest, Sentry (and in one bundle, GTM). All use dummy IDs; nothing is wired to real analytics.

## How to run

1. Open the demo page in a browser. From the repo root:

   ```bash
   open gymdemo/gymfinity_co_index.html
   ```

   Or serve the `gymdemo` folder with any static server, e.g.:

   ```bash
   cd gymdemo && python3 -m http.server 8000
   ```

   Then visit `http://localhost:8000/gymfinity_co_index.html`.

2. The Transcend script is loaded from `transcend-cdn.com`; the consent banner and Privacy Center depend on your Transcend configuration (e.g. bundle ID in the script `src`).

## Page structure

| Section        | ID / purpose                          |
|----------------|----------------------------------------|
| Nav            | Sticky header, brand, Shop / Join Crew |
| Hero           | Headline, CTA, hero image               |
| Features       | `#features` — Why Gymfinity (3 cards)  |
| Collections    | `#collections` — Women, Men, Accessories |
| Reviews        | `#reviews` — Testimonials              |
| Signup         | `#signup` — Email form (submit is client-side only) |
| Footer         | Year, social links, Privacy Center, Cookie preferences |

## Privacy Center & consent

- **Privacy Center** in the footer points to a Transcend-hosted URL (e.g. `gymfinity-transcend-io.trsnd.co`). Update the link if your Transcend tenant or domain changes.
- **Cookie preferences** calls `transcend.showConsentManager({ viewState: 'AcceptOrRejectAll' })` when the link is clicked (requires Transcend script loaded).

## Notes

- The HTML references `trackers.js` in the same directory (`gymdemo/`). Use either `gymdemo/trackers.js` or `gymdemo/scripts/trackers.js` and keep the `src` in the page in sync.
- All tracker IDs in the repo are placeholders (e.g. `G-DEMO123456`, `000000000000000`). Do not use them in production.
