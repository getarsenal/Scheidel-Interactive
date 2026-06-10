# Scheidel Interactive

Single-file portfolio site for **Scheidel Interactive** — a solo dev studio's games and
tools. No build step, no dependencies beyond Google Fonts. The whole site is one
`index.html`, hash-routed, ready to drop into GitHub Pages.

## Run it

Open `index.html` in any browser. There's nothing to build or install.

```sh
# optional: serve locally
python3 -m http.server
# → http://localhost:8000
```

## Add or edit a project

Everything on the site — tiles, detail pages, and the hero stat counts — is driven by the
`PROJECTS` array near the bottom of `index.html`. Add or edit one object and the rest
updates itself. Field documentation is commented directly above the array.

## Assets

- `logos/` — per-project logo art (PNG/SVG). Missing or broken logos fall back to a
  generated letter tile automatically, so nothing renders broken.
- `shots/` — screenshots for project detail pages. Append `::wide` to a path for a
  landscape (16:9) shot.

## Deploy

Push to the repo and enable **GitHub Pages** (Settings → Pages → deploy from the default
branch root). The site is just `index.html`.

## More

See [`HANDOFF.md`](HANDOFF.md) for architecture notes, the full data model, and the
pre-launch TODO list.
