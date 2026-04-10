# paper-notes — external memory for academic reading

This repo is Kunming's personal external memory for papers, talks, blog posts, and other research material — primarily neuroscience and NeuroAI. It follows a **two-layer** pipeline and is published as a Quartz site at https://kunmings.github.io/paper-notes/.

## Folder layout

```
drafts/         raw source material — fetched paper full-text, PDFs, verbatim web captures. IMMUTABLE INBOX.
  neuroscience/ papers fetched via USC library proxy or open-access sources
  science-meta/ meta-science, tools, landscape notes
notes/          working notes — structured paper summaries, thematic reviews. Obsidian frontmatter + [[wikilinks]].
wiki/           synthesis layer
  index.md      knowledge map (clusters + tag index)
  <topic>.md    per-cluster synthesis pages
site/           Quartz v4 static site generator. content/ symlinks → ../notes and ../wiki.
.claude/skills/distill-notes/   the skill that runs this pipeline
```

### Two-layer model

- **Drafts** (raw): fetched paper text, PDFs, verbatim captures. Named `<author>-<year>-<short-slug>.md` with frontmatter (`title`, `authors`, `source_url`, `fetched`). These are the immutable source of truth.
- **Notes** (working): structured paper notes and thematic reviews written by the user. Named `<kebab-slug>.md`. These are the user's own organized reading notes — they may be detailed and are not auto-generated. The wiki layer synthesizes across notes.

## How to act in this repo

### When the user provides a URL

**This is a primary trigger.** If the user gives any URL — arxiv, biorxiv, lab page, blog, Substack, X post, talk transcript, etc. — you should:

1. Fetch the content. Try `WebFetch` first; fall back to Chrome DevTools MCP (`mcp__chrome-devtools__navigate_page` + `take_snapshot`/`evaluate_script`) for JS-rendered or paywalled pages. For paywalled academic sources, use the USC library proxy (`libproxy1.usc.edu`) — the user's Chrome session is typically authenticated.
2. Save the captured content **verbatim** to `drafts/<category>/<author>-<year>-<short-slug>.md` with frontmatter (`title`, `authors`, `source_url`, `fetched`). Pick `<category>` to match an existing subfolder; create a new one only if there's no fit.
3. Do **not** auto-generate notes — the user writes their own structured notes in `notes/`.

Don't summarize before saving the draft — drafts are the raw source material.

### When the user says "update the wiki"

Run the `distill-notes` skill (`.claude/skills/distill-notes/SKILL.md`) to regenerate wiki synthesis pages from the current `notes/`. In short:

1. Reuse the existing tag vocabulary in `wiki/index.md` rather than inventing new spellings.
2. Update affected `wiki/<topic>.md` synthesis pages and regenerate `wiki/index.md` (clusters + tag index). Create a new cluster page only when ≥3 notes share a theme.
3. Cross-link densely: every note should link to ≥1 wiki topic and ≥1 sibling note where applicable.
4. Report concisely: notes scanned, wiki pages updated, any new tags or clusters.

### Hard rules

- **Never modify files in `drafts/`.** They are the immutable source. If the user wants a draft changed, ask whether to re-fetch.
- **Notes are user-authored.** Don't overwrite or auto-regenerate them. The user writes and maintains `notes/` directly.
- **Don't hallucinate** authors, years, DOIs, or claims not present in the source. If unknown, write `unknown`.
- **Slugs are kebab-case and stable** across runs. If a note already exists for a draft, update it in place — don't create a duplicate.
- **Don't delete notes or wiki pages** without telling the user first.

## Publishing

- Quartz lives in `site/`. Content is symlinked: `site/content/notes` → `../../notes`, `site/content/wiki` → `../../wiki`. Don't break those symlinks.
- The CI workflow at `.github/workflows/deploy.yml` resolves the symlinks (`cp -R`) on the runner, builds with Node 22, and deploys to GitHub Pages on every push to `main`.
- The splash page is `site/content/index.md`.
- Quartz config: `site/quartz.config.ts`. `baseUrl` is `kunmings.github.io/paper-notes` (project page, not user page).
- A push to `main` is enough to redeploy — don't run `npx quartz build` locally (the user's local Node is v20, which Quartz rejects; CI handles it).

## Style for the user

Kunming is a researcher who reads heavily and wants the wiki to be useful for *their own* future thinking, not a generic summary. When distilling:

- Lead with the surprising or load-bearing claim, not the abstract boilerplate.
- "Why it matters" should connect to themes already in `wiki/` — name them with `[[wikilinks]]`.
- Methods only when methodologically interesting; skip rote experimental detail.
- Prefer the author's own technical vocabulary over paraphrase.
