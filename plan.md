# plan.md — Manulife AI (GitHub Pages / Jekyll) “Front Door”

## 0) Goal and guardrails
**Goal:** a minimal, Manulife-branded public front door that supports **Evident analyst validation** by making **public evidence** easy to discover.

**Positioning:** AI research and applied research are **embedded within business functions and technology functions**. The site should *not* read like a standalone “AI research lab.”

**Credibility rules**
- **No adjectives without artifacts:** any claim like “cutting-edge / state-of-the-art / leading” must be in the same paragraph as a public artifact link (paper, repo, talk, patent, partner page).
- **Evidence-first, neutral tone:** hybrid institutional + research voice.
- **Minimal UI, minimal pages:** dense, high-signal content. No marketing graphics, no animations by default.

---

## 1) Top navigation (minimal IA)
1) **Overview** (homepage)  
2) **Embedded Domains** (`/domains/`)  
3) **Collaborations** (`/collaborations/`)  
4) **Open Source** (`/open-source/`)  
5) **Library** (`/library/`)

> Responsible AI is a section on **Overview** (high-level + links), not a separate top-nav node, to keep the site minimal.

---

## 2) Stack choice and why
**Jekyll (GitHub Pages native)** is the default because it’s the easiest to maintain:
- No custom deployment pipeline required for GitHub Pages.
- Engineers update Markdown/YAML via PRs.
- Works well for small inventory: ~10 publications, ~3 OSS repos, many collaborations.

Optional: keep a very light CI that runs `jekyll build` on PRs to catch mistakes early.

---

## 3) Repo structure (implemented in the scaffold)
```
/
  _config.yml
  Gemfile
  README.md
  SECURITY.md
  assets/css/main.css

  _includes/
    header.html
    footer.html

  _layouts/
    default.html
    domain.html
    library_item.html

  _data/
    collaborations.yml
    open_source.yml

  _domains/                 # collection: embedded domains
    underwriting.md
    fraud.md
    platforms.md
    ...

  _library/                 # collection: public artifacts
    2025-sample-paper.md
    2024-sample-talk.md
    2023-sample-oss.md
    ...

  index.md                  # Overview
  domains/index.md          # Embedded Domains listing
  collaborations/index.md   # Collaboration directory
  open-source/index.md      # OSS catalog
  library/index.md          # Library landing
  library/{publications,talks,reports,patents}/index.md

  .github/
    workflows/ci.yml
    pull_request_template.md
```

---

## 4) Content model

### 4.1 Embedded Domains (`_domains/*.md`)
**Purpose:** represent where AI is embedded (business + tech functions).

Front matter fields (required):
- `title`: Domain name (display)
- `slug`: stable identifier (used for tags/joins)
- `blurb`: short description shown on tiles
- `contact`: team alias (public)

Body content: 3–8 bullets describing focus areas (neutral, no hype).

### 4.2 Library items (`_library/*.md`)
**Purpose:** the evidence ledger (public artifacts).

Front matter fields (required):
- `title`
- `year`
- `type`: `publication | talk | report | patent | blog | other`
- `venue`
- `org_unit`: “Manulife AI (Team Name)” or equivalent (do not foreground individuals)
- `domains`: list of domain slugs (e.g., `["fraud"]`)
- `external_url`: DOI/arXiv/video/slides/patent page/repo page (must be public)
- `summary`: one-line contribution statement (factual)

Optional:
- `code_url`: related code (if public)
- `pdf_url`: direct PDF link (if public)

Body content: short neutral summary (what problem, what approach, what evidence).

### 4.3 Collaborations (`_data/collaborations.yml`)
**Purpose:** highlight breadth/depth of academic collaborations (structured, non-marketing).

Fields (suggested):
- `domain`: domain slug
- `partner`: university/lab/institute name
- `type`: `academic | industry`
- `years`: “2024–2026”
- `area`: short description of focus
- `links`: list of `{label, url}` to public pages/artifacts

### 4.4 Open Source (`_data/open_source.yml`)
**Purpose:** a small catalog (~3 repos).

Fields (suggested):
- `name`
- `repo_url`
- `status`: `maintained | active | archived`
- `team_owner`
- `license`
- `last_release`
- `description`

---

## 5) Anti AI-washing gating (implemented)
Domains are only shown publicly when they meet the evidence threshold:

A domain appears on `/domains/` and on the homepage tiles only if:
- **≥2 public Library items**, OR
- **≥1 public Library item AND ≥1 named collaboration** (in collaborations.yml)

Anything below threshold stays in `_domains/` but is not promoted/listed.

This prevents “placeholder pillars” from appearing without evidence.

---

## 6) Page behaviors (how it renders)
### 6.1 Overview (index.md)
- “Latest updates”: auto lists newest Library items
- “Embedded domains”: auto shows only published domains (gating rules)
- Responsible AI: high-level bullets + links (no internals); includes mention of “three lines of defense / model risk validation gates” at a high level
- Open source: renders cards from `_data/open_source.yml`

### 6.2 Domain pages (`_layouts/domain.html`)
For a given domain slug, it auto-renders:
- Library items tagged to that domain
- Collaborations tagged to that domain

### 6.3 Library landing and type pages
- `/library/` lists all items
- Type pages filter by `type` (publication/talk/report/patent)
- No search box (simplicity). Browsing is via these curated type pages + domain pages.

---

## 7) Branding (Manulife theme hook)
**Minimal Manulife look** is achieved via design tokens in `assets/css/main.css`:
- `--brand-primary`, `--brand-secondary`, `--brand-accent`
- type stack, spacing, borders, card styles

Implementation approach:
- Replace placeholder token values with **official Manulife brand guideline values**.
- Swap the header “mark” block for an approved SVG/logo lockup (respect clearspace rules).
- Keep components minimal: headings, lists, cards, callouts.

---

## 8) Contribution workflow (engineer-friendly)
### Add a new publication/talk/patent
1) Create a new file in `_library/` (e.g., `_library/2026-<slug>.md`)
2) Fill required front matter + 5–10 line neutral summary
3) Tag one or more domains via `domains: ["underwriting"]`
4) Open a PR

### Add a new academic collaboration
1) Add an entry to `_data/collaborations.yml`
2) Include at least one public link

### Update OSS catalog
1) Edit `_data/open_source.yml` (3 repos expected)

**PR checklist** is in `.github/pull_request_template.md` (links public, no restricted detail, no adjectives without artifacts, correct domain tags).

---

## 9) Local dev and deployment
### Local run
```bash
bundle install
bundle exec jekyll serve
```

### Deploy (GitHub Pages)
- Push to `main`
- GitHub Pages: set source to `main` / root (or the GitHub Pages defaults for Jekyll)
- Optional: keep `.github/workflows/ci.yml` to build on PRs

No analytics scripts. No cookies banners required.

---

## 10) Launch checklist (practical)
1) Replace placeholder repo URLs and contact aliases
2) Add the ~10 publications (high signal only)
3) Add all academic collaborations (with public links)
4) Add the ~3 open-source repos
5) Ensure each public domain meets gating threshold
6) Apply Manulife brand tokens + logo lockup
7) Sanity check: mobile, contrast, broken links

---

## 11) “Done” definition
- Minimal nav (5 pages) with dense evidence
- Domains only visible when evidence threshold is met
- Library is small and high-signal (~10 publications + a few talks/patents/reports)
- Collaborations directory is rich and structured
- Open source page lists ~3 repos with owners and status
- Branding matches Manulife guidelines via tokens + approved logo usage
