# New to the Wall Foundation — website

Static site for https://newtothewallfoundation.com

## Structure

```
index.html              home
collection/index.html   the collection (React via CDN + Babel standalone, single file)
how-we-collect/         the essay
fragile-arles.jpg       Sartor / Fondation Van Gogh Arles image
netlify.toml            build + header config
```

## How the collection page works

`collection/index.html` is self-contained. All the data lives in one array near
the top of the `<script type="text/babel">` block:

```js
const COLLECTION = [
  { artist, title, medium, dimensions, gallery, year, region, market, driveId, provenance? },
  ...
];
```

- **`driveId`** — the Google Drive file ID of the artwork image. The page builds
  `https://lh3.googleusercontent.com/d/<driveId>`. The Drive file **must be shared
  "Anyone with the link → Viewer"** or the image will not load.
  Images live in `My Drive/Art & Culture/Art Collection/Images/`.
- **`region`** — must be one of `REGION_ORDER`. Add a new region there *and* in
  `REGION_LABELS` before using it.
- **`market`** — `Emerging` | `Ascending` | `Established` (drives the badge colour).
- **`provenance`** — optional; renders as a note under the card (loans, exhibitions).

Header counts (works / artists / galleries / regions) are derived, not hard-coded.

## Adding a work

1. Put the image in the Drive Images folder, set link-sharing to Anyone with the link.
2. Copy the file ID out of the Drive URL (`/file/d/<ID>/view`).
3. Add one line to `COLLECTION`.
4. Commit and push — Netlify deploys automatically.

Keep the site in step with `Foundation_Dashboard_v1` (the Artworks tab is the
source of record). Works classified `Paris apartment (not collection)` in the
dashboard are deliberately excluded from the acquisition ledger but are shown
here under Amelie, Maison d'art.

## Deploying

Netlify builds from `main`. There is no build step — the repo root is published
as-is.

Before this repo existed the site was updated by drag-and-drop (Netlify Drop).
Once the site is connected to this repo in Netlify (Site configuration → Build &
deploy → Link repository), drop deploys should stop being used, or they will be
overwritten by the next push.
