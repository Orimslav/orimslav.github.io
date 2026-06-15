# CLAUDE.md — orimslav.github.io

## Project overview
Personal freelance portfolio website for the brand Orimslav.
Single-page static HTML/CSS/JS site, hosted on GitHub Pages at `orimslav.github.io`.

## Stack
- Pure HTML/CSS/JS — no framework, no build tool
- Fonts: JetBrains Mono + DM Sans (Google Fonts)
- No dependencies, no npm

## Files
```
orimslav.github.io/
├── index.html                          # Main page (single file)
├── orimslav_logo_blue_transparent.png  # Logo — do not modify
└── CLAUDE.md
```

## Design system
- Background: `#0d0d12`
- Card background: `#13131a`
- Card hover: `#1a1a24`
- Border: `rgba(255,255,255,0.07)`
- Border hover: `rgba(82,162,255,0.4)`
- Blue accent: `#52a2ff`
- Text primary: `#e8e8f0`
- Text muted: `#7070a0`
- Tag color: `#89bcff`
- Tag background: `rgba(82,162,255,0.1)`
- Green (Python badge): `#4ade80`
- Amber (IoT badge): `#fbbf24`
- Grid background: 40px dot grid, `rgba(82,162,255,0.015)`
- Max width: `1200px`
- Font display: JetBrains Mono (logo, labels, tags, nav brand)
- Font body: DM Sans (headings, descriptions, buttons)

## Trilingual system (SK / EN / RU)
- Every text element uses `data-lang="sk"`, `data-lang="en"`, `data-lang="ru"` attributes
- Active language gets class `al` (display:contents), others hidden
- Language stored in `localStorage` key `lang`, default `sk`
- Language switcher: flag image buttons in nav, class `lb`, active gets class `active`
- JS function: `setLang(l)` — toggles `al` class + `active` class + saves to localStorage

```js
function setLang(l) {
  document.querySelectorAll('[data-lang]').forEach(e => {
    e.classList.toggle('al', e.dataset.lang === l);
  });
  document.querySelectorAll('.lb').forEach(b => {
    b.classList.toggle('active', b.title === {'sk':'Slovenčina','en':'English','ru':'Русский'}[l]);
  });
  localStorage.setItem('lang', l);
}
```

## Logo
- File: `orimslav_logo_blue_transparent.png`
- Used as `<img>` in nav, width/height 42px
- Nav brand text: `ORIMSLAV`, JetBrains Mono, gradient `#a8d4f8 → #52a2ff`
- In current index.html the logo is embedded as base64 — when deploying to GitHub Pages, switch to `src="orimslav_logo_blue_transparent.png"` (external file is cleaner)

## Sections
1. **Nav** — sticky, blur backdrop, logo + brand + nav links + lang switcher
2. **Hero** — label "available for freelance", h1 `ORIMSLAV` (JetBrains Mono, blue gradient), subtitle, 4 buttons
3. **Skills bar** — monospace pills, full width
4. **Projects** — 3-column grid, 6 cards, each links to existing GitHub Pages project
5. **Services** — 3-column grid (PLC automation, Python dev, Embedded/IoT)
6. **Contact** — single wide box, text left + links right
7. **Footer** — centered, monospace, muted

## Project cards
Each card has:
- Category badge: `cat-py` (green) or `cat-iot` (amber)
- Arrow `↗` top right, animates on hover
- Project name (white, 15px, 500)
- Description (trilingual, 12px, muted)
- Tech tags (JetBrains Mono, 10px, blue tint)

Current projects (do not remove, only add):
| Name | URL | Category |
|---|---|---|
| Archív bločkov | https://orimslav.github.io/archiv_blockov/ | Python |
| Camera Checker | https://orimslav.github.io/camera_checker/ | Python |
| Folder Backup Tool | https://orimslav.github.io/Backup_tool/ | Python |
| Level Sensor Monitor | https://orimslav.github.io/level_sensor/ | IoT/Modbus |
| Modbus IO Monitor | https://orimslav.github.io/modbus-monitor-waveshare/ | IoT/Modbus |
| Audio → Modbus TCP | https://orimslav.github.io/audio_converter/ | ESP32/IoT |

## Responsive breakpoints
- `≤860px`: projects grid → 2 columns
- `≤560px`: projects grid → 1 column
- `≤680px`: services grid → 1 column

## Planned improvements (TODO)
- [ ] Switch logo from base64 to external PNG file
- [ ] Add "O mne / About / О себе" section with photo
- [ ] Add email contact link (mailto)
- [ ] Add Hackster.io link to contact
- [ ] Add custom domain `orimslav.com` when ready (CNAME file + DNS)
- [ ] Add new projects as they are published

## How to add a new project
1. Add a new `<a class="pc">` card in the `.pg` grid
2. Use `cat-py` or `cat-iot` badge class
3. Add trilingual description with `data-lang` spans
4. Add relevant `.tag` elements
5. Link to the GitHub Pages URL of the project

## Deployment
```bash
git add .
git commit -m "update portfolio"
git push origin main
# GitHub Pages auto-deploys in ~1 min
```

## Custom domain (when ready)
1. Buy `orimslav.com` on Namecheap or Cloudflare Registrar
2. Create file `CNAME` in repo root with content: `orimslav.com`
3. In DNS: add CNAME record `www` → `orimslav.github.io`
4. Add A records pointing to GitHub Pages IPs
5. Enable HTTPS in GitHub Pages settings
