---
name: publish-site-artifact
description: Publish a static site artifact — a self-contained report, guide or plan page — to Ravitejeswar's static-site dumpyard (ravitejeswar8657.github.io/sites). Use when asked to publish, upload, or add a static page artifact.
---

# Publish to ravitejeswar8657.github.io/sites

Static-site dumpyard by Ravitejeswar. Repo `Ravitejeswar8657/sites`, branch `main`, served at https://ravitejeswar8657.github.io/sites/ (GitHub Pages project site — the site lives under the `/sites/` path, so use RELATIVE links inside pages, never root-absolute `/...` links).

## Add a page

1. Slug: lowercase kebab-case, e.g. `palnadu-irrigation-history`.
2. Write self-contained `index.html` (inline CSS/JS, no build, no frameworks; keep any assets inside your folder; include a `<title>` — it becomes the listing text) to:
   - report → `research/<slug>/index.html` (serves at `/sites/research/<slug>/`)
   - guide → `learning/<slug>/index.html` (serves at `/sites/learning/<slug>/`)
   - plan → `plans/<slug>/index.html` (serves at `/sites/plans/<slug>/`)
3. Never touch `.nojekyll`, `robots.txt`, `llms.txt`, `add-skill.sh`, `skills/`, `.github/`, `research/index.html`, `learning/index.html`, `plans/index.html` (listings regenerate automatically via a GitHub Action). Never commit tokens/secrets.
4. Everything here is PUBLIC. Never publish personal data, phone numbers, internal office/constituency data, or anything the human marked confidential.

## Upload (pick the first that applies; never hardcode or commit tokens)

### 1. gh CLI (shell, authenticated — no clone needed)

```sh
CONTENT=$(base64 < /local/path/to/index.html | tr -d '\n')
gh api "repos/Ravitejeswar8657/sites/contents/research/<slug>/index.html" \
  -X PUT -f message="add <slug>" -f branch="main" -f content="$CONTENT"
# updating an existing file: GET the path first for its "sha", then add -f sha="<sha>".
```

### 2. GitHub MCP server / GitHub connector (installed + authenticated)

Call `create_or_update_file` once per file with owner `Ravitejeswar8657`,
repo `sites`, branch `main`, path `research/<slug>/index.html`
(or `learning/...`, `plans/...`), your HTML as `content` (raw text, not base64),
message `add <slug>`. Omit `sha` for new files; for updates fetch it
first via `get_file_contents` (same owner/repo/path, ref `main`).

### 3. GitHub REST API (`GITHUB_TOKEN` in env, else ask the human for one)

```sh
CONTENT=$(base64 < /local/path/to/index.html | tr -d '\n')
curl -X PUT -H "Authorization: Bearer $GITHUB_TOKEN" \
  -H "Accept: application/vnd.github+json" \
  https://api.github.com/repos/Ravitejeswar8657/sites/contents/research/<slug>/index.html \
  -d "{\"message\":\"add <slug>\",\"content\":\"$CONTENT\",\"branch\":\"main\"}"
# updating an existing file: GET the path first, add its "sha" to the payload.
```

## Checklist before you finish

- [ ] Page renders standalone (open the file directly, no server needed).
- [ ] Only relative links/asset paths inside the page.
- [ ] You pushed only your page (listings update themselves via Action).
- [ ] No secrets, tokens, or personal data committed.
- [ ] Tell the human the public URL: https://ravitejeswar8657.github.io/sites/<section>/<slug>/ (live ~1 minute after push).
