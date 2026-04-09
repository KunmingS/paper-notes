---
name: distill-notes
description: Distill raw paper-reading drafts into atomic notes and a cross-linked wiki. Use when the user adds new files to `drafts/`, gives a URL to a paper/blog/website to ingest, or asks to "update the wiki", "rebuild the knowledge map", "ingest this link", or "redistill my notes".
---

# distill-notes

This is an external-memory pipeline for `paper-notes/`, inspired by Karpathy's drafts → distill → wiki workflow.

## Folder layout

```
drafts/        raw, unedited dumps (one file per source — paper, blog, talk)
notes/         atomic distilled notes, one per source, Obsidian wikilinks
wiki/          synthesis layer
  index.md     top-level knowledge map + tag index
  <topic>.md   per-cluster synthesis pages
```

`drafts/` is append-only from the user. `notes/` and `wiki/` are regenerated/extended by this skill — never hand-edited by the user.

## Triggers

1. **New draft files** added under `drafts/` → distill them.
2. **URL provided by user** (arxiv, biorxiv, blog, substack, X post, lab page) → fetch, save to `drafts/<category>/<slug>.md`, then distill.
3. **"Update the wiki" / "rebuild knowledge map"** → re-cluster everything.

## Procedure

### A. Ingesting a URL

1. Try `WebFetch` first — fastest for static pages and arxiv abstracts.
2. If `WebFetch` fails, returns paywalled/JS-rendered content, or the user explicitly says "use playwright", fall back to the Playwright MCP tools (`mcp__plugin_playwright_playwright__browser_navigate` then `browser_snapshot` or `browser_evaluate` to extract text). For paywalled academic content, try the `cookie-extract` skill to get an authenticated session.
3. Save the captured content verbatim to `drafts/<category>/<kebab-slug>.md` with a header:
   ```
   ---
   source_url: <url>
   fetched: <YYYY-MM-DD>
   ---
   ```
   Pick `<category>` to match existing subfolders (e.g. `neuroscience/`); create a new one if no fit.
4. Then run step B on the new draft.

### B. Distilling drafts → atomic notes

For each new (or changed) file in `drafts/`, write `notes/<slug>.md` with this template:

```markdown
---
title: <paper title>
authors: <or "unknown">
year: <or omit>
source: drafts/<path>
source_url: <if known>
tags: [tag1, tag2]
created: <YYYY-MM-DD>
---

# <Title>

## TL;DR
2–3 sentence punchline.

## Key claims
- bullets

## Methods
- bullets (omit if not relevant)

## Why it matters
1–2 sentences linking to broader themes.

## Related
- [[other-note-slug]]
- [[wiki/topic]]
```

Rules:
- Slugs are lowercase-kebab-case and stable across runs. If a note already exists for a draft, **update in place**, don't duplicate.
- Use a controlled tag vocabulary — before adding a new tag, check `wiki/index.md`'s tag index and reuse existing spelling.
- Be faithful to the source. Don't invent claims, citations, or numbers.
- Keep notes ≤ ~300 words. Drafts are the long form.

### C. Updating the wiki

After any distill run:

1. Re-read all `notes/*.md` frontmatter (titles + tags) — cheap.
2. Decide if existing clusters in `wiki/` still cover everything. If a new theme has emerged (≥3 notes), create a new `wiki/<topic>.md`.
3. Update the affected `wiki/<topic>.md` synthesis pages — short (~150–300 words), cite notes via `[[wikilinks]]`, never invent.
4. Regenerate `wiki/index.md`:
   - Cluster headings with 1–2 sentence descriptions and bulleted `[[note]]` lists.
   - "Tag index" section: each tag → notes under it.
5. Cross-link densely: every atomic note should link to ≥1 wiki topic and ≥1 sibling note where applicable.

### D. Reporting

After running, report concisely:
- N drafts ingested, N notes written/updated, N wiki pages touched.
- Any new tags or clusters introduced.
- Any drafts that didn't fit cleanly (flag for the user).

## Don'ts

- Don't modify files in `drafts/` once written — they are the immutable source.
- Don't delete notes/wiki pages without telling the user.
- Don't hallucinate authors, years, or DOIs. If unknown, write `unknown`.
- Don't create a new cluster for a single note — leave it under the closest existing topic until it has siblings.
