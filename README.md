# PipGarden — website

The public download page. **This folder is the entire site**: one self-contained
HTML file with no build step, no dependencies, and no reference to the app's
source code.

## Publish it on its own

Push **this folder only** — not the repository root.

The app's source is proprietary (see `../LICENSE`). If you push the whole
project to a public repository to get GitHub Pages working, you publish the
source with it. Keeping the site in its own repository makes that mistake
impossible rather than merely unlikely.

```bash
cd web
git init
git add .
git commit -m "PipGarden download page"
git branch -M main
git remote add origin https://github.com/<account>/pipgarden-site.git
git push -u origin main
```

Then on GitHub: **Settings → Pages → Source: `main`, folder `/ (root)`**.

The site is live at `https://<account>.github.io/pipgarden-site/` within a
minute or two.

## Wire up the download button

The buttons are deliberately inert until there is a real file to point at — a
live-looking button that 404s is worse than one that admits it isn't ready. The
page detects this and says so.

Edit the `DOWNLOAD` object near the top of the `<script>` in `index.html`:

```js
const DOWNLOAD = {
  installer: "https://yourname.itch.io/pipgarden",
  portable:  "https://yourname.itch.io/pipgarden",
};
```

Point both at the **itch.io page**, not at a bare `.exe`. itch serves the file,
shows its size, and a player who is already on itch is far more likely to click
through the unsigned-app warning than someone handed a raw download link.

If you would rather host the files yourself, GitHub Releases works too — use the
`/releases/latest/download/<file>` form so the links survive every future
release without editing this page.

## Editing

Open `index.html` in a browser. There is no build, no server, no npm install —
it renders straight from the file. The only external requests are the two Google
Fonts.
