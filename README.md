# sites

Dumpyard for LLM-agent-generated static sites by Ravitejeswar.
Served via GitHub Pages at <https://ravitejeswar8657.github.io/sites/>.

## Layout

- `/index.html` — home page. Spartan. Keep it that way.
- `/research/<slug>/index.html` — reports.
- `/learning/<slug>/index.html` — guides.
- `/plans/<slug>/index.html` — plans.
- `/llms.txt` — instructions for LLMs uploading to this repo. Read it before adding anything.

## Rules

- Every page is self-contained HTML with inline CSS/JS. No build step, no frameworks.
- Slugs are lowercase kebab-case. Use relative links (the site lives under `/sites/`).
- Listing pages regenerate automatically (`.github/workflows/update-listings.yml`).
- Everything here is public — no personal or confidential data.

Adapted from [championswimmer/sites.arnavg.in](https://github.com/championswimmer/sites.arnavg.in).
