# Manulife AI Research Website

[![GitHub Pages](https://img.shields.io/badge/Deployed%20on-GitHub%20Pages-blue)](https://sabyasm.github.io/manulife-ai-research)

This repository powers the Manulife AI Research public-facing website, built with Jekyll and hosted on GitHub Pages.  The site showcases AI research publications, patents, talks, open source projects, academic collaborations, and embedded AI domains across the organization.

---

## Table of Contents

- [Quick Start](#quick-start)
- [Site Architecture](#site-architecture)
- [Content Types & How to Add Them](#content-types--how-to-add-them)
  - [Publications, Patents & Talks (Library Items)](#1-publications-patents--talks-library-items)
  - [Open Source Projects](#2-open-source-projects)
  - [Academic & Industry Collaborations](#3-academic--industry-collaborations)
  - [Embedded Domains](#4-embedded-domains)
- [Evidence Gating Rules](#evidence-gating-rules)
- [Contribution Workflow](#contribution-workflow)
- [PR Checklist](#pr-checklist)
- [Local Development](#local-development)
- [Deployment](#deployment)
- [Troubleshooting](#troubleshooting)

---

## Quick Start

| I want to add... | Where to edit | Jump to section |
|------------------|---------------|-----------------|
| New publication/paper | `_library/YYYY-slug.md` | [Library Items](#1-publications-patents--talks-library-items) |
| New patent | `_library/YYYY-slug.md` | [Library Items](#1-publications-patents--talks-library-items) |
| New conference talk | `_library/YYYY-slug.md` | [Library Items](#1-publications-patents--talks-library-items) |
| New open source repo | `_data/open_source.yml` | [Open Source](#2-open-source-projects) |
| New collaboration | `_data/collaborations.yml` | [Collaborations](#3-academic--industry-collaborations) |
| New research domain | `_domains/slug.md` | [Domains](#4-embedded-domains) |

---

## Site Architecture

```
/
├── _config.yml           # Jekyll configuration
├── _data/                # YAML data files
│   ├── collaborations.yml    # Academic/industry partnerships
│   └── open_source.yml       # Open source project catalog
├── _domains/             # Research domain collection (Markdown)
│   ├── fraud.md
│   ├── underwriting.md
│   └── platforms.md
├── _library/             # Publications, patents, talks (Markdown)
│   ├── 2025-fraud-gnn.md
│   ├── 2024-anomaly-detection.md
│   └── ... 
├── _includes/            # Reusable HTML components
├── _layouts/             # Page templates
├── assets/               # CSS, images, static files
├── index.md              # Homepage (Overview)
├── domains/index.md      # Domains listing page
├── library/index.md      # Library listing page
├── collaborations/index.md
└── open-source/index.md
```

### Collections

| Collection | Location | Purpose |
|------------|----------|---------|
| `library` | `_library/*.md` | Publications, patents, talks, reports |
| `domains` | `_domains/*.md` | Research focus areas embedded in business units |

### Data Files

| File | Location | Purpose |
|------|----------|---------|
| `open_source.yml` | `_data/open_source.yml` | Catalog of open source repositories |
| `collaborations.yml` | `_data/collaborations.yml` | Academic and industry partnerships |

---

## Content Types & How to Add Them

### 1. Publications, Patents & Talks (Library Items)

Library items are the core research artifacts displayed on the site. These include **publications**, **patents**, **talks**, and **reports**.

#### File Location
```
_library/YYYY-descriptive-slug.md
```

**Naming Convention:** `{year}-{short-descriptive-slug}.md`
- Example: `2025-fraud-gnn.md`, `2024-mlops-talk.md`, `2023-underwriting-patent.md`

#### Template: Publication

```yaml
---
title: "Your Publication Title Here"
year: 2025
type: publication
venue: "Conference or Journal Name (e.g., AAAI, NeurIPS, ICML)"
org_unit: "Manulife AI (Business Unit)"
domains: ["fraud", "underwriting"]  # Must match slugs in _domains/
external_url: https://arxiv.org/abs/your-paper-id
code_url: https://github.com/manulife/your-repo  # Optional
pdf_url: https://example.com/paper.pdf  # Optional
summary: "1-2 sentence neutral summary of the research contribution."
---

Detailed description of the research (5-10 lines, neutral tone).

**Problem:** What problem does this work address?

**Approach:** Brief description of the methodology.

**Results:** Key quantitative or qualitative outcomes.

**Deployment:** Status of production deployment (if applicable).
```

#### Template: Patent

```yaml
---
title: "Systems and Methods for [Description]"
year: 2023
type: patent
venue: "US Patent Office"
org_unit: "Manulife AI (Business Unit)"
domains: ["underwriting"]
external_url: https://patents.google.com/patent/US12345678
summary: "Brief description of what the patent covers."
---

**Patent Number:** US 12,345,678

**Abstract:** High-level description of the invention.

**Claims:** Key claims covered by the patent.

**Status:** Granted [year] / Pending
```

#### Template: Talk

```yaml
---
title: "Your Talk Title"
year: 2024
type: talk
venue: "Conference Name"
org_unit: "Manulife AI (Team)"
domains: ["platforms"]
external_url: https://conference.com/talk-link
pdf_url: https://example.com/slides.pdf  # Optional: link to slides
video_url: https://youtube.com/watch?v=xxx  # Optional: link to recording
summary: "Brief description of the talk topic."
---

Description of the talk content.

**Topics covered:**
- Topic 1
- Topic 2

**Audience:** Who this talk is intended for.
```

#### Required vs Optional Fields

| Field | Required | Description |
|-------|----------|-------------|
| `title` | ✅ | Full title of the artifact |
| `year` | ✅ | Publication/grant year (integer) |
| `type` | ✅ | One of: `publication`, `patent`, `talk`, `report` |
| `venue` | ✅ | Conference, journal, or issuing body |
| `org_unit` | ✅ | Business unit (e.g., "Manulife AI (Claims)") |
| `domains` | ✅ | Array of domain slugs (must match `_domains/*.md` slugs) |
| `external_url` | ✅ | Public link to the artifact |
| `summary` | ✅ | 1-2 sentence description |
| `code_url` | ❌ | Link to associated code repository |
| `pdf_url` | ❌ | Direct link to PDF |
| `video_url` | ❌ | Link to video recording |

#### Valid `type` Values
- `publication` - Peer-reviewed papers, preprints
- `patent` - Granted or pending patents
- `talk` - Conference presentations, keynotes
- `report` - Technical reports, white papers

---

### 2. Open Source Projects

Open source projects are maintained in a centralized YAML file.

#### File Location
```
_data/open_source.yml
```

#### How to Add a New Project

Open `_data/open_source.yml` and add a new entry:

```yaml
- name: "Project Display Name"
  repo_url: "https://github.com/manulife/repo-name"
  status: "active"  # One of: maintained, active, archived
  team_owner: "Team Name (e.g., AI Platforms)"
  license: "Apache-2.0"
  last_release: "v1.2.0 (2025-01)"
  description: "Brief description of what this project does (1-2 sentences)."
```

#### Field Reference

| Field | Required | Description |
|-------|----------|-------------|
| `name` | ✅ | Display name of the project |
| `repo_url` | ✅ | Full GitHub URL to the repository |
| `status` | ✅ | One of: `maintained`, `active`, `archived` |
| `team_owner` | ✅ | Team responsible for the project |
| `license` | ✅ | SPDX license identifier (e.g., Apache-2.0, MIT) |
| `last_release` | ✅ | Latest release version and date |
| `description` | ✅ | Short description (displayed on cards) |

#### Status Definitions
- `active` - Under active development with recent commits
- `maintained` - Stable, receiving bug fixes and security updates
- `archived` - No longer maintained, kept for reference

#### Example Entry

```yaml
- name: "Fraud Detection Toolkit"
  repo_url: "https://github.com/manulife/fraud-detection-toolkit"
  status: "active"
  team_owner: "Claims AI"
  license: "Apache-2.0"
  last_release: "v2.1.0 (2025-01)"
  description: "Graph neural network utilities for insurance fraud detection patterns."
```

---

### 3. Academic & Industry Collaborations

Collaborations showcase partnerships with universities, research labs, and industry organizations.

#### File Location
```
_data/collaborations.yml
```

#### How to Add a New Collaboration

Open `_data/collaborations.yml` and add a new entry:

```yaml
- partner: "University Name or Organization"
  type: "academic"  # One of: academic, industry
  domain: "fraud"   # Must match a slug in _domains/
  years: "2024–2026"
  area: "Brief description of the collaboration focus area."
  links:
    - label: "Project Page"
      url: "https://university.edu/project"
    - label: "Related Publication"
      url: "https://arxiv.org/abs/xxx"
```

#### Field Reference

| Field | Required | Description |
|-------|----------|-------------|
| `partner` | ✅ | Name of collaborating organization |
| `type` | ✅ | One of: `academic`, `industry` |
| `domain` | ✅ | Related domain slug |
| `years` | ✅ | Active years (e.g., "2024–2026") |
| `area` | ✅ | Description of collaboration focus |
| `links` | ✅ | Array of public links (at least one required) |

#### Links Structure
Each link must have:
- `label`: Display text for the link
- `url`: Public URL (must be accessible without authentication)

#### Example Entry

```yaml
- partner: "MIT CSAIL"
  type: "academic"
  domain: "underwriting"
  years: "2023–2025"
  area: "Interpretable machine learning for automated underwriting decisions"
  links:
    - label: "Lab Page"
      url: "https://csail.mit.edu/research/project"
    - label: "Joint Publication"
      url: "https://arxiv.org/abs/2024.12345"
```

---

### 4. Embedded Domains

Domains represent research focus areas embedded within business and technology functions. **Only add new domains when you have sufficient evidence** (see [Evidence Gating Rules](#evidence-gating-rules)).

#### File Location
```
_domains/slug.md
```

**Naming Convention:** The filename (without `.md`) becomes the `slug` used to reference the domain elsewhere.

#### Template

```yaml
---
title: "Domain Display Name"
slug: "domain-slug"  # Must match filename
blurb: "One sentence description shown on cards."
contact: "team-alias@manulife.com"  # Optional
---

- Bullet point describing a capability or focus area
- Another key area of work
- Additional capability
```

#### Example

```yaml
---
title: "Fraud Detection"
slug: "fraud"
blurb: "Pattern recognition and anomaly detection to identify and prevent fraudulent claims and transactions."
contact: "fraud-ai@manulife.com"
---

- Real-time transaction monitoring systems
- Graph-based network analysis for organized fraud detection
- Behavioral pattern recognition and anomaly scoring
- Claims validation and document authenticity verification
- Continuous learning from investigator feedback
```

#### Linking Domains to Other Content

To associate a library item with a domain, add the domain's slug to the `domains` array:

```yaml
# In _library/2025-fraud-gnn.md
domains: ["fraud", "platforms"]  # References fraud.md and platforms.md
```

---

## Evidence Gating Rules

**Important:** Domains only appear publicly on the website when they meet the evidence threshold:

| Threshold | Requirement |
|-----------|-------------|
| **Option A** | ≥2 library items tagged with the domain |
| **Option B** | ≥1 library item AND ≥1 collaboration tagged with the domain |

This ensures we only showcase domains with demonstrated, public evidence of research activity.

### Implications for Contributors

- **Before adding a new domain:** Ensure you have at least 2 library items OR 1 library item + 1 collaboration ready to publish
- **When adding library items:** Tag them with appropriate domain slugs to build domain visibility
- **Hidden domains:** Domains that don't meet the threshold still exist but won't appear in navigation or listings

---

## Contribution Workflow

### Standard Process

1. **Fork or create a branch** from `main`
2. **Make your changes** following the templates above
3. **Test locally** (see [Local Development](#local-development))
4. **Open a Pull Request** with a clear description
5. **Address review feedback**
6. **Merge** once approved

### File-by-File Guide

| Change Type | Files to Edit |
|-------------|--------------|
| Add publication | Create `_library/YYYY-slug.md` |
| Add patent | Create `_library/YYYY-slug.md` with `type: patent` |
| Add talk | Create `_library/YYYY-slug.md` with `type: talk` |
| Add OSS project | Edit `_data/open_source.yml` |
| Add collaboration | Edit `_data/collaborations.yml` |
| Add new domain | Create `_domains/slug.md` (ensure evidence threshold is met) |

---

## PR Checklist

Before submitting your PR, verify:

- [ ] **All links are public** – No internal/authenticated URLs
- [ ] **No restricted/confidential details** – Content is appropriate for public disclosure
- [ ] **No marketing adjectives without artifacts** – Claims are backed by evidence
- [ ] **Domain tags are correct** – Slugs match existing `_domains/*.md` files
- [ ] **Required fields are present** – Check field requirements for your content type
- [ ] **File naming follows convention** – `YYYY-descriptive-slug.md` for library items
- [ ] **YAML syntax is valid** – No parsing errors
- [ ] **Local build passes** – Run `bundle exec jekyll build` without errors

---

## Local Development

### Prerequisites

- Ruby 2.7+ with Bundler
- Git

### Setup

```bash
# Clone the repository
git clone https://github.com/sabyasm/manulife-ai-research.git
cd manulife-ai-research

# Install dependencies
bundle install
```

### Running Locally

```bash
bundle exec jekyll serve
```

Visit [http://localhost:4000/manulife-ai-research/](http://localhost:4000/manulife-ai-research/) in your browser.

### Live Reload

For automatic browser refresh on changes:

```bash
bundle exec jekyll serve --livereload
```

### Building Without Serving

```bash
bundle exec jekyll build
```

Built files are output to the `_site/` directory.

---

## Deployment

The site is automatically deployed to GitHub Pages when changes are merged to `main`.

- **Production URL:** https://sabyasm.github.io/manulife-ai-research/
- **Build process:** GitHub Pages builds the Jekyll site automatically
- **No manual deployment required**

### CI/CD

Pull requests trigger a CI build to catch errors before merge. Check the status checks on your PR to ensure the build passes.

---

## Troubleshooting

### Common Issues

#### YAML Parsing Errors
```
Error: YAML parsing error in _library/my-file.md
```
**Solution:** Check for:
- Missing quotes around values with special characters
- Incorrect indentation (use 2 spaces)
- Missing colons after field names

#### Domain Not Appearing
**Problem:** Added a domain but it's not showing on the site.

**Solution:** Ensure the domain meets the evidence threshold:
- Add at least 2 library items with `domains: ["your-slug"]`, OR
- Add 1 library item AND 1 collaboration referencing the domain

#### Links Not Working
**Problem:** External links return 404.

**Solution:** Verify:
- URLs are publicly accessible (try in incognito mode)
- No typos in the URL
- The resource hasn't been moved or deleted

#### Invalid Domain Reference
```
Warning: Domain 'xyz' not found
```
**Solution:** Ensure the `domains` array in your library item matches an existing file in `_domains/`. The slug must match the filename exactly (without `.md`).

### Getting Help

- Check existing library items for examples
- Review the [plan.md](plan.md) file for detailed architecture decisions
- Open an issue if you encounter persistent problems

---

## Content Guidelines

### Writing Style

- **Neutral tone** – Avoid superlatives and marketing language
- **Evidence-based** – Claims must be backed by artifacts
- **Concise** – Summaries should be 1-2 sentences; full descriptions 5-10 lines
- **Technical accuracy** – Ensure methodology and results are correctly described

### What NOT to Include

- ❌ Internal/confidential information
- ❌ URLs requiring authentication
- ❌ Unreleased or embargoed research
- ❌ Personal contact information (use team aliases)
- ❌ Competitive intelligence or trade secrets

---

## Questions?

For questions about contributing, open an issue in this repository or contact the relevant domain team using the contact information on each domain page.