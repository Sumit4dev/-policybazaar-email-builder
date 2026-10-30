# Policybazaar Email Builder

A no-install tool for the marketing team: upload 3 banner images, edit the T&C / policy (ad) number text, preview, take a **screenshot (PNG)** and **download a ready ZIP** (HTML + images folder).

## For the team (no technical knowledge needed)
1. Open the tool link (or double-click `index.html`).
2. Type a campaign name (e.g. `oct-email-2`).
3. Upload Banner 1, 2, 3 (700 px wide JPG/PNG).
4. Edit the text under the images. Untick a box to remove that line.
5. Click **Screenshot (PNG)** or **Download ZIP**.

Only the images and the 3 footer text blocks can change. The layout, app-download badges and unsubscribe link are locked.

## Host on GitHub Pages (free)
1. Create a new GitHub repo and upload everything in this folder.
2. Repo → **Settings → Pages → Build and deployment → Source: "Deploy from a branch"**, branch `main`, folder `/ (root)`. Save.
3. After ~1 minute the tool is live at `https://<org-or-user>.github.io/<repo>/`.
(A GitHub Actions workflow is also included if you prefer Source: "GitHub Actions".)

> Company-internal use? Use a **private** repo with GitHub Enterprise Pages, or host the same folder on any internal web server — it's just static files.

## Folder map
| Path | Purpose |
|---|---|
| `index.html` | The page |
| `css/style.css` | Look & feel |
| `js/app.js` | Tool logic |
| `js/template.js` | **The approved email HTML** (with placeholders) |
| `js/vendor/` | html2canvas (screenshot) + JSZip (zip), bundled locally, no CDN |
| `samples/` | Sample images for the "Load sample images" button |

## Developer notes
- **Changing the email design**: edit `js/template.js`. Placeholders: `{{IMG1..3}} {{ALT1..3}} {{LINK1..3}} {{TC1}} {{TC2}} {{AD}} {{TITLE}}`.
- **Changing default footer text**: edit `DEFAULTS` at the top of `js/app.js`.
- Images are referenced as `images/<campaign>-01.jpg` etc. in the exported HTML. Upload them to your CDN and replace the path before sending, or keep the folder structure when importing to your ESP.
- Footer text is saved in the browser (localStorage); images are not stored anywhere — everything runs locally in the browser, nothing is uploaded to a server.
- Store badges load from `static.pbcdn.in`; if that host blocks cross-origin reads, the screenshot draws a plain black "Google Play / App Store" badge instead.
