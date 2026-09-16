# Airbnb Clone — Single-File Edition

A complete, working Airbnb-style website in **one self-contained `index.html`**.
All CSS, JavaScript, and sample listing data are inlined — no build step, no
dependencies, no framework.

---

## Run it

### Option 1 — Open the file directly

Double-click `index.html`, or drag it into any browser.

### Option 2 — Serve it locally (recommended)

```bash
# Python (preinstalled on macOS/Linux)
python3 -m http.server 8000

# Node.js
npx serve -l 8000

# PHP
php -S localhost:8000
```

Then open **http://localhost:8000**.

### Option 3 — GitHub Pages

Push this repo and enable Pages (Settings → Pages → Source: `main` / root).
Your site will be live at `https://<username>.github.io/<repo>/`.

---

## What's included

Everything lives in `index.html` (≈228 KB) and switches between three views
in-page — no page reloads, no routing library.

### Home view
- **Hero search** — destination text input, check-in / check-out calendar
  (two-month picker, past dates disabled, range highlighting), guest stepper
  (adults / children / infants).
- **12 category chips** — Beachfront, Cabins, City, Amazing pools, Countryside,
  Luxe, Trending, Design, Tropical, Lakefront, Tiny homes, All.
- **Filter panel** — dual-handle price slider ($0–$800), minimum guests,
  10 property types, 8 popular amenities (with counts), all removable via pills.
- **Sorting** — Recommended, Price low→high, Price high→low, Top rated,
  Most reviewed.
- **View modes** — grid, compact grid, and list.
- **12 listing cards** — photo, superhost badge, title, city/country,
  beds/baths, star rating with review count, nightly price, and a heart button.
- Value-props strip and an inspiration section with 4 tabs.

### Listing detail view
- **Photo gallery** — mosaic layout, "Show all photos" tour, and a lightbox with
  prev/next and keyboard arrow navigation.
- **Header** — title, rating, review count, Superhost badge, location, plus
  Share and Save actions.
- **Host card** — avatar, join year, response rate, Superhost badge, and three
  highlight rows.
- **Description** — expandable with Show more / Show less.
- **Amenities** — one row per amenity with a matching inline SVG icon (23 mapped
  icons plus a generic fallback).
- **Reviews** — overall rating, a 5→1 star distribution with animated bars, and
  a card per review.
- **Map** — a stylised location card with a pin and coordinates.
- **Similar stays** — 4 listings ranked by type, country, and rating.
- **Sticky booking widget** — date picker, guest selector capped to the
  listing's capacity, and a **live price breakdown**.

### Wishlists view
- Saved stays grouped by region, with 4 sort modes.
- A summary of your last search with **Resume search** / **Forget**.
- Per-card removal and a confirm-guarded **Clear all**.
- Empty state when nothing is saved.

### Plus
- **Login / signup modal** with inline validation (email format, password
  length) and a one-click **Continue as demo guest**.
- **Booking confirmation modal** with the listing thumbnail, stay details, the
  full itemised breakdown, and the total.
- **State persistence** — search criteria, dates, guests, login, and favorites
  all survive a page reload via `localStorage`.
- **Responsive** from 1600px down to 375px.

---

## Pricing formula

The booking widget recalculates on every date or guest change:

| Line | Rule |
| --- | --- |
| Nightly | `price × nights` |
| Weekly discount | 10% off the subtotal when nights ≥ 7 |
| Cleaning fee | $65 flat (only when nights > 0) |
| Service fee | 14% of the discounted subtotal |
| Taxes | 8% of (discounted subtotal + cleaning + service) |
| **Total** | sum of the above |

**Worked example** — 3 nights at $189:
`$567 + $65 + $79 + $57 = **$768**`

**Worked example** — 7 nights at $189:
`$1,323 − $132 + $167 + $114 = **$1,537**`

---

## Sample data

12 listings across 12 cities, each with a title, type, location (city, country,
lat/lng), nightly price, rating, review count, superhost flag, amenity list,
host details, 4 photos, description, capacity, and 2–3 reviews.

| Id | Stay | City | Price |
| --- | --- | --- | --- |
| lst-001 | Sunny Loft with Skyline Views | New York | $189 |
| lst-002 | Cozy Beach Cottage by the Sea | Malibu | $342 |
| lst-003 | Modern Apartment near Sagrada Família | Barcelona | $128 |
| lst-004 | Traditional Ryokan-Style Townhouse | Kyoto | $205 |
| lst-005 | Cliffside Villa with Infinity Pool | Santorini | $612 |
| lst-006 | Rustic Cabin in the Pine Forest | Banff | $224 |
| lst-007 | Designer Studio in Shoreditch | London | $145 |
| lst-008 | Overwater Bungalow with Lagoon Access | Bora Bora | $780 |
| lst-009 | Loft Apartment in Kreuzberg | Berlin | $112 |
| lst-010 | Hillside Cottage with Vineyard Views | Tuscany | $268 |
| lst-011 | Oceanfront Suite in Bondi | Sydney | $176 |
| lst-012 | Desert Dome under the Stars | Joshua Tree | $231 |

Photos load from Unsplash and avatars from pravatar.cc, so an internet
connection gives the full visual experience. The layout and every interaction
work offline; only the images need the network.

---

## Try these

1. Type `kyoto` in the hero search → the grid narrows to one stay.
2. Open **Filters**, drag the price handles to `$0–$200`, tick a property type,
   then press **Show results**.
3. Click any card — the detail view opens in place (watch the progress bar at
   the top).
4. Pick dates in the booking widget and watch the breakdown update live, then
   press **Reserve**.
5. Heart a few stays — saving prompts a login; use **Continue as demo guest**.
6. Open **Wishlists** from the header.
7. Reload the page — your search, dates, guests, login, and favorites all come
   back.
8. Resize the window to phone width — the grid reflows, the header collapses to
   a "Where to?" pill, and the booking widget moves below the content.

---

## Project structure

```
.
├── index.html   # The entire site: markup, CSS, JavaScript, and data
└── README.md
```

Inside `index.html`:

| Section | Contents |
| --- | --- |
| `<style>` | Design tokens, reset, layout, all component styles, responsive breakpoints |
| `<div id="view-home">` | Hero search, category bar, filter panel, listing grid |
| `<div id="view-listing">` | Detail view mount (`#detailRoot`) |
| `<div id="view-favorites">` | Wishlists view |
| `<script>` | Data (`DATA_API`), store (`Store`), components (`UI`), modals (`Modals`), and the three view controllers |
| `<script>` | The in-page view switcher (`App`) |

The application exposes a handful of globals for debugging in the console:
`DATA_API`, `Store`, `UI`, `Modals`, and `App`.

---

## Browser support

Modern evergreen browsers (Chrome, Edge, Firefox, Safari). Uses CSS grid,
custom properties, `aspect-ratio`, optional chaining, and `localStorage`.
No polyfills required.

---

## Notes

- This is a front-end demo: there is no backend, and "login" and "booking" are
  simulated locally. Nothing is sent anywhere.
- All state lives in your browser's `localStorage` under keys prefixed
  `airbnb_clone_`. Clearing site data resets the app.
