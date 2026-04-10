---
name: lint
description: Health-check the wiki for orphan pages, dead links, stale content, and contradictions. Fixes what it can, flags the rest.
---

Run a full lint pass on the wiki at `{{WIKI_PATH}}/`.

## Checks

1. **Orphan pages** — find pages in `pages/` not listed in `index.md` and not linked from any other page. Fix by adding to `index.md`.

2. **Dead links** — find markdown links in `pages/` pointing to files that don't exist. Fix by creating stub pages or removing broken links.

3. **Stale pages** — find pages whose raw sources (listed in `sources:` frontmatter) have a newer modification date than the page's `updated:` date. Flag for re-ingest.

4. **Missing "See Also"** — find pages with no "See Also" section. Add 2-5 related page links based on tag overlap and content similarity.

5. **Missing frontmatter** — find pages missing required YAML fields (title, created, updated, tags, sources). Fix by adding them.

6. **Oversized pages** — find pages over 300 lines. Flag for splitting.

7. **Index sync** — verify every page in `pages/` has an entry in `index.md` and every `index.md` entry points to an existing page.

## Output

Report as a table:

| Check | Issues | Auto-fixed | Needs human |
|-------|--------|------------|-------------|

Fix everything you can automatically. For items needing human input, explain what's wrong and suggest a fix.

Append a lint summary to `{{WIKI_PATH}}/log.md`.
