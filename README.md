# Manulife AI

Public front door for Manulife's AI research and applied research, embedded within business and technology functions.

## Local Development

```bash
bundle install
bundle exec jekyll serve
```

Visit [http://localhost:4000](http://localhost:4000)

## Contributing

### Add a new publication/talk/patent
1. Create a new file in `_library/` (e.g., `_library/2026-<slug>.md`)
2. Fill required front matter + 5–10 line neutral summary
3. Tag one or more domains via `domains: ["underwriting"]`
4. Open a PR

### Add a new academic collaboration
1. Add an entry to `_data/collaborations.yml`
2. Include at least one public link

### Update OSS catalog
1. Edit `_data/open_source.yml`

## Site Structure

- **Overview** (`/`) - Homepage with latest updates, embedded domains, responsible AI
- **Embedded Domains** (`/domains/`) - Where AI is embedded in business/tech functions
- **Collaborations** (`/collaborations/`) - Academic and industry partnerships
- **Open Source** (`/open-source/`) - Public repositories
- **Library** (`/library/`) - Publications, talks, reports, patents

## Evidence Gating

Domains only appear publicly when they meet the evidence threshold:
- ≥2 public Library items, OR
- ≥1 public Library item AND ≥1 named collaboration
