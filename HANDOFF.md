# Scheidel Interactive — Portfolio Site Handoff

## What this is

A single-file portfolio site (`index.html`) listing Scheidel Interactive's games and
tools. Hash-routed, no build step, drops straight into a GitHub Pages repo. Matches the
existing stack: single-file HTML/CSS/JS, Bungee + JetBrains Mono + Space Grotesk, dark
warm palette consistent with ARSENAL / Mission Tracker.

## Architecture

- **One file**, `index.html`. No dependencies beyond Google Fonts.
- **Two views** toggled by the `.active` class: `#view-home` (hero + tile grids) and
  `#view-detail` (per-project page).
- **Hash router** (`route()` fires on `hashchange`): `#arsenal` renders that project's
  detail page, empty hash shows home. Back button and shareable links both work.
- **Single data source**: the `PROJECTS` array drives everything — tiles, detail pages,
  and the stat counts in the hero. Add/edit a project = edit one object. Field docs are
  commented directly above the array in `index.html`.
- **Aesthetic**: CRT arcade — scanline overlay, ember drop-shadow logo, pulsing "live"
  dot, status badges (Live / Beta / In Dev).

## Current state (working)

- Home grids render Games (3) and Tools (3), counts auto-derived.
- Tiles are `<a href="#slug">` → route to detail pages with a trailer slot, About story,
  screenshot gallery + click-to-zoom lightbox, and a features / stack / meta sidebar.
- Logo system: `logo:` path per project (PNG or SVG). Missing/broken logos auto-fall back
  to a generated letter tile via `onerror`, so nothing ever renders broken.
- Placeholders for missing trailers ("coming soon") and screenshots.
- Quality floor: responsive to mobile, keyboard focus visible, `prefers-reduced-motion`
  honored. Embedded JS validated (parses clean).

## Data model — the `PROJECTS` array

Each object:

| field         | purpose                                                    |
|---------------|------------------------------------------------------------|
| `slug`        | URL hash, lowercase no spaces (`#arsenal`)                 |
| `title`       | display name                                               |
| `kind`        | label shown above title (Game / App / PWA / Tool)          |
| `type`        | `"games"` or `"tools"` — which grid it lands in            |
| `status`      | `"live"` / `"beta"` / `"dev"` — drives badge + hero counts |
| `accent`      | hex; tints border, badge, buttons, etc.                    |
| `logo`        | path e.g. `"logos/arsenal.svg"`. `""` = letter fallback    |
| `blurb`       | one line on the tile                                       |
| `lead`        | bold opening line on detail page (optional)                |
| `story`       | array of paragraphs for the About section                  |
| `features`    | bullet list in sidebar                                     |
| `stack`       | tech tags (first 3 also show on the tile)                  |
| `meta`        | array of `[key, value]` rows in the Details table          |
| `trailer`     | YouTube/Vimeo EMBED url. `""` = "coming soon" placeholder  |
| `screenshots` | array of image paths. Append `::wide` for a landscape shot |
| `links`       | buttons: `{label, url, primary?, disabled?}`               |

## TODO before launch

1. **Real links** — App Store, Google Play, and FIREBASE play URLs are all `#`
   placeholders. Edit each project's `links:` array.
1. **Logos** — add art to the `logos/` folder. Pre-filled guessed paths:
   `logos/arsenal.svg`, `logos/firebase.svg`, `logos/mission-tracker.svg`,
   `logos/leave-her-johnny.png`. Rename the files OR the `logo:` values so they match.
   Colony Commander + Range 1 are `""` (letter fallback) until art exists.
1. **Screenshots** — populate each `screenshots:[...]` from the `shots/` folder,
   append `::wide` for landscape images.
1. **Trailers** — paste YouTube/Vimeo *embed* URLs (not watch URLs) into `trailer:`.
1. **Verify guesses** —
   - GitHub footer link assumes `github.com/getarsenal`. ✅ Verified — matches the repo owner.
   - Footer branding reads "A Scheidel Holdings LLC brand".
   - "est. 2024" is hardcoded in the hero.
   - Confirm "Scheidel Interactive" vs "Scheidel Holdings LLC" public-facing intent.

## Deploy

Drop `index.html` at the repo root → enable GitHub Pages. As a standalone Pages site it's
just the one file. If this ever lands in a Capacitor-adjacent repo, watch the www-sync
trap (`cp index.html www/index.html`).

## Folder layout

```
/
├── index.html
├── HANDOFF.md
├── logos/
│   ├── arsenal.svg
│   ├── firebase.svg
│   ├── mission-tracker.svg
│   └── leave-her-johnny.png
└── shots/
    ├── arsenal-1.png
    └── ...
```
