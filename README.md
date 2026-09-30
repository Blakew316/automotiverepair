# Clinton Complete Auto Care: website

A fast, static, multi-page website for **Clinton Complete Auto Care, And Small Engine Repair**.
Each page is a complete, standalone HTML document with no framework and no build step, so it can be hosted anywhere (Netlify, GitHub Pages, Cloudflare Pages, any web server) or opened straight from disk.

- **Design**: light ivory surfaces, espresso ink and a soft holographic-foil accent taken from the brand's business card and its foil "And Small Engine Repair" tagline. Apple system typography (SF Pro on Apple devices, with Inter as the fallback elsewhere).
- **Motion**: automotive-themed animations throughout: the 3D brand card with a foil sheen and cursor tilt, a scroll-progress car under the header, a "road" process timeline the car drives along, a rolling odometer, a live "open now" status, and a custom animated line illustration on every page (spinning brake rotor, running mower, and so on). Everything respects *Reduce Motion*.
- **Navigation**: cross-document View Transitions (the header stays put while pages glide, and the active-tab pill slides between tabs), Speculation Rules prerendering on hover (Chrome/Edge) with a prefetch fallback for Safari and Firefox, a desktop mega menu, and an iOS-style bottom tab bar with a "More" sheet on phones and tablets.

## Pages

| Page | File |
| --- | --- |
| Home (landing page) | `index.html` |
| Services hub + symptom finder | `services.html` |
| Service pages (11) | `services/brakes.html`, `oil-change`, `diagnostics`, `engine-repair`, `transmission`, `heating-ac`, `tires-alignment`, `suspension-steering`, `electrical-battery`, `inspections`, `small-engine-repair` |
| About | `about.html` |
| Makes we service | `brands.html` |
| Fleet & business | `fleet.html` |
| Specials | `specials.html` |
| Car care guides (warning-light decoder, maintenance timeline, seasonal checklists) | `resources.html` |
| FAQ | `faq.html` |
| Contact | `contact.html` |
| Book a service (multi-step request form) | `appointment.html` |
| Careers | `careers.html` |
| Privacy | `privacy.html` |
| Not found | `404.html` |

## Before you launch: replace the placeholders

The shop's real details weren't available, so these are placeholders. They all live in **one file**:

1. Edit **`business.json`**: phone, email, street address, city/state/ZIP, Google Maps link, website URL, opening hours (and optionally a time zone like `America/Chicago` for the live "Open now" badge), social links.
2. Run `node scripts/sync.mjs`. Every page, the structured data (for Google), `sitemap.xml` and `robots.txt` are updated.

Also review:
- **`specials.html`**: the coupon offers are examples. Confirm or replace the amounts and terms.
- **`careers.html`**: the roles are the kinds of positions a shop like this typically hires for. Adjust to suit.
- **`privacy.html`**: a plain-language template. Have it reviewed.
- Copy throughout describes *how the shop works* (written estimates, approval before extra work). Make sure it matches how you actually operate.

## Editing

- **Page content**: edit the page's HTML directly. Shared regions are marked like `<!-- @partial header --> … <!-- @end header -->`; don't edit inside those markers, because they are regenerated.
- **Header, footer, mobile tab bar, call-to-action band, icons**: edit `partials/*.html` (services list: `partials/services.json`), then run `node scripts/sync.mjs`.
- **Styles and behaviour**: `assets/css/site.css` (design tokens at the top) and `assets/js/site.js`.
- **Check your work**: `node scripts/check.mjs` validates every page (one `<h1>`, links and assets resolve, labels, ids, no leftover placeholders).
- **Preview locally**: `npm run serve`, then open http://localhost:8080.

## Forms

The contact, appointment, fleet and careers forms work out of the box on **Netlify** (Netlify Forms picks them up automatically; submissions appear in the Netlify dashboard and can be emailed to you).
On any other host, set `"formEndpoint"` in `business.json` to a form service URL (for example Formspree) and run the sync script.
If a submission can't be sent, visitors see a friendly fallback that opens a pre-filled email or offers the phone number, so a request is never lost.

## Brand assets

`assets/img/` holds the logo extracted from the business-card photo (white-on-transparent, for the espresso card treatment), the header mark, favicons/app icons built from the wordmark's "C", and the social-share image `og-image.png`.
