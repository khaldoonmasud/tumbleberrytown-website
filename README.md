# tumbleberrytown.com

The website for Tumbleberry Town: a landing page, the privacy policy and a help page.
Plain HTML and CSS, hosted free on GitHub Pages. No cookies, no analytics, no
third-party scripts or fonts (the Fredoka font is served from here, under its OFL
licence in `assets/fonts/OFL.txt`).

| Page | URL | File |
|---|---|---|
| Home | https://tumbleberrytown.com/ | `index.html` |
| Privacy policy (linked from the game and every store) | https://tumbleberrytown.com/privacy | `privacy/index.html` |
| Help (the stores' support URL) | https://tumbleberrytown.com/support | `support/index.html` |

The game's repository keeps the source text of the privacy policy
(`store/PRIVACY_POLICY.md`) and the screenshots this site uses; change both together.
The preview video (`assets/preview.mp4`) is a 720p copy of the game's
`store/video/app_preview_1920x1080.mp4`:
`ffmpeg -i app_preview_1920x1080.mp4 -vf scale=1280:720 -c:v libx264 -crf 26 -preset slow -c:a aac -b:a 128k -movflags +faststart preview.mp4`.

## Moving it to its own repository (once)

This folder starts inside the private game repository (`website/`); the site needs
its own **public** repository for free GitHub Pages.

1. On github.com, create an **empty, public** repository (for example
   `khaldoonmasud/tumbleberrytown-website`): no README, .gitignore or licence.
2. Copy everything in this folder, hidden files included, except `.gdignore`
   (which only matters inside the game repository), and push it to `main`:
   ```sh
   mkdir tumbleberrytown-website
   cp -R tumbleberry-town/website/. tumbleberrytown-website/
   cd tumbleberrytown-website && rm .gdignore
   git init -b main && git add . && git commit -m "tumbleberrytown.com: home, privacy, help"
   git remote add origin https://github.com/khaldoonmasud/tumbleberrytown-website.git
   git push -u origin main
   ```
3. Nothing else from the game repository belongs here: no code, no store videos.
4. Once the site is live, the copy in the game repository can be removed, so there
   is only one to keep up to date.

## Turning it on (once)

1. **GitHub Pages:** this repository > Settings > Pages > "Build and deployment":
   Source **Deploy from a branch**, branch **main**, folder **/ (root)**. Save.
2. **Custom domain:** on the same page, type `tumbleberrytown.com` and Save (the
   `CNAME` file here already says it).
3. **DNS** at the company where you bought the domain. Delete any existing A/AAAA
   records for the bare domain (`@`), then add:

   | Type | Name | Value |
   |---|---|---|
   | A | @ | 185.199.108.153 |
   | A | @ | 185.199.109.153 |
   | A | @ | 185.199.110.153 |
   | A | @ | 185.199.111.153 |
   | AAAA | @ | 2606:50c0:8000::153 |
   | AAAA | @ | 2606:50c0:8001::153 |
   | AAAA | @ | 2606:50c0:8002::153 |
   | AAAA | @ | 2606:50c0:8003::153 |
   | CNAME | www | `<your GitHub username>.github.io` |

   Keep your email (MX) records as they are: they are what makes
   support@tumbleberrytown.com work.
4. Wait for DNS (minutes to a day). When the Pages settings show the domain as
   checked, tick **Enforce HTTPS**.
5. Optional but recommended: GitHub > your profile Settings > Pages > **Add a
   verified domain**, so nobody else can claim tumbleberrytown.com on GitHub.

Check these addresses against GitHub's current guide before you add them:
https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site

## When the app is in the stores

Replace the three "Coming soon" badges in `index.html` with links to the store pages
(each store has official badge images and rules for using them).
