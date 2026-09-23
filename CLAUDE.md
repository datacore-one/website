# Datacore Website

This is the official website for Datacore at https://datacore.one

## Overview

Static landing page showcasing Datacore - "Your own superintelligence." Features a tesseract animation with sacred geometry themes, dark/light theme toggle, and an easter egg journey.

## Tech Stack

- Pure HTML/CSS/JS (no build step)
- System preference detection for theme
- Scroll-based animation effects

## Structure

```
website/
├── index.html          # Main landing page
├── assets/             # Images, fonts, static assets
├── docs/               # Website documentation
├── README.md           # Project overview
└── CLAUDE.md           # This file
```

## Development

```bash
# Local development server
python3 -m http.server 8000
# Then visit http://localhost:8000
```

## Deployment

**Target**: https://datacore.one — the campaigns server, `209.38.243.88`.
There is no CI. A git push changes nothing that a visitor sees.

```bash
rsync -avz -e 'ssh -i ~/Data/.datacore/env/credentials/deploy_key' \
  index.html features.html services.html app.html install install.txt llms.txt \
  robots.txt sitemap.xml \
  deploy@209.38.243.88:/var/www/sites/datacore.one/
```

Rsync only the files that changed; there is no build step and no reason to push
the whole directory.

Then verify over HTTP rather than assuming — the deploy is only real once the
server serves it:

```bash
curl -s -o /dev/null -w '%{http_code}\n' https://datacore.one/install.txt
curl -s https://datacore.one/ | grep -c 'the-thing-you-just-changed'
curl -s -o /dev/null -w '%{http_code}\n' https://datacore.one/not-a-page   # must be 404
```

That last check matters: this is a multi-page static site, not a SPA. The Caddy
block must use `try_files {path} {path}.html`. With the SPA fallback every
unknown path returned 200 with the homepage, so `/features` and `/app` silently
served the front page and a guessed `/install.sh` piped HTML into bash.

> The script this file used to name,
> `~/.datacore/modules/datacore-campaigns/scripts/deploy-site.sh`, no longer
> exists — the campaigns module was absorbed into `comms`. Corrected
> 2026-09-23, after the command had to be recovered from engram memory to
> deploy at all.

## Key Features

| Feature | Description |
|---------|-------------|
| Tesseract animation | Sacred geometry SVG with scroll-based evolution |
| Theme toggle | Dark/light with system preference detection |
| Easter egg | Wait 5s at bottom for surprise journey |
| Responsive | Mobile-first design |

## Related

- Campaign module: `~/.datacore/modules/datacore-campaigns/`
- Analytics: PostHog (see campaigns module for API access)
- Parent space: `/Users/gregor/Data/2-datacore/`

## AI Guidelines

When modifying this website:
1. Preserve the tesseract animation and scroll effects
2. Maintain the sacred geometry aesthetic
3. Test both light and dark themes
4. Verify easter egg still works after changes
5. Deploy and verify HTTP 200 response

## Datacore Space Context

This project lives inside a Datacore space. Session lifecycle commands are available:

- `/wrap-up` — write session entry to team journal, commit and push
- `/continue` — resume from yesterday's continuation notes; `--save` persists current work
- `/standup` — generate/post standup from recent team journals
- `/today` — daily briefing (incremental if already generated)

| Key | Value |
|-----|-------|
| Space | `2-datacore` |
| Journal | `~/Data/2-datacore/journal/YYYY-MM-DD.md` |
| Org | `~/Data/2-datacore/org/next_actions.org` |

When `/wrap-up` runs, use the team journal schema: `## @contributor` narrative sections + `## Session Metadata` YAML block.
