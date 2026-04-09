# paper-notes — external memory for academic reading

This repo is Kunming's personal external memory for papers, talks, blog posts, and other research material — primarily neuroscience and NeuroAI. It follows a **drafts → distill → wiki** pipeline (inspired by Karpathy's note-taking workflow) and is published as a Quartz site at https://kunmings.github.io/paper-notes/.

## Folder layout

```
drafts/         raw, unedited captures — one file per source. IMMUTABLE INBOX.
notes/          atomic distilled notes, one per source. Obsidian frontmatter + [[wikilinks]].
wiki/           synthesis layer
  index.md      knowledge map (clusters + tag index)
  <topic>.md    per-cluster synthesis pages
site/           Quartz v4 static site generator. content/ symlinks → ../notes and ../wiki.
.claude/skills/distill-notes/   the skill that runs this pipeline
```

## How to act in this repo

### When the user provides a URL

**This is a primary trigger.** If the user gives any URL — arxiv, biorxiv, lab page, blog, Substack, X post, talk transcript, etc. — you should:

1. Fetch the content. Try `WebFetch` first; fall back to Playwright MCP (`mcp__plugin_playwright_playwright__browser_navigate` + `browser_snapshot`/`browser_evaluate`) for JS-rendered or paywalled pages. For paywalled academic sources, the `cookie-extract` skill can provide an authenticated session.
2. Save the captured content **verbatim** to `drafts/<category>/<kebab-slug>.md` with a frontmatter header containing `source_url` and `fetched` date. Pick `<category>` to match an existing subfolder (currently just `neuroscience/`); create a new one only if there's no fit.
3. Then run the distill step (next section) on the new draft.

Don't summarize before saving the draft — drafts are the long form. Distillation happens in the next layer.

### When the user adds new files to `drafts/` or says "distill" / "update the wiki"

Run the `distill-notes` skill (`.claude/skills/distill-notes/SKILL.md`). In short:

1. For each new or changed draft, write/update `notes/<slug>.md` using the standard atomic-note template (frontmatter with `title`, `authors`, `year`, `source`, `source_url`, `tags`, `created`; sections for TL;DR, Key claims, Methods, Why it matters, Related). Keep notes ≤ ~300 words. Be faithful — never invent claims, authors, or citations.
2. Reuse the existing tag vocabulary in `wiki/index.md` rather than inventing new spellings.
3. Update affected `wiki/<topic>.md` synthesis pages and regenerate `wiki/index.md` (clusters + tag index). Create a new cluster page only when ≥3 notes share a theme.
4. Cross-link densely: every atomic note should link to ≥1 wiki topic and ≥1 sibling note where applicable.
5. Report concisely: drafts ingested, notes touched, wiki pages updated, any new tags or clusters.

### Hard rules

- **Never modify files in `drafts/`.** They are the immutable source. If the user wants a draft changed, ask whether to re-fetch or hand-edit the corresponding `notes/` entry instead.
- **Don't hand-author `notes/` or `wiki/` content.** They are regenerated from drafts via the distill skill. One-off edits will get clobbered next run.
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
