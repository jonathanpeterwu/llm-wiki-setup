---
name: ingest
description: Process new raw sources into wiki pages. Reads unprocessed files from raw/, extracts knowledge, creates or updates pages, and cross-links.
---

Ingest new sources into the wiki. Process: $ARGUMENTS

If no specific file is named, scan `{{WIKI_PATH}}/raw/` for files not yet referenced in any page's `sources:` frontmatter.

For each unprocessed source:

1. **Read** the full source file in `{{WIKI_PATH}}/raw/`.
2. **Extract** entities, concepts, facts, and decisions.
3. **Check for existing pages** — grep `{{WIKI_PATH}}/pages/` for overlapping topics before creating anything new. If 60%+ overlap, merge into the existing page.
4. **Create or update** wiki pages in `{{WIKI_PATH}}/pages/` following the page format in CLAUDE.md (YAML frontmatter with title, created, updated, tags, sources).
5. **Cross-link aggressively** — every entity with its own page gets linked. After creating a new page, scan existing pages and add backlinks to them.
6. **Update index** — add new entries to `{{WIKI_PATH}}/index.md` under the appropriate category.
7. **Log it** — append a timestamped entry to `{{WIKI_PATH}}/log.md` for each source processed.

After ingesting, report:
- How many sources processed
- Pages created vs. updated
- New cross-links added
