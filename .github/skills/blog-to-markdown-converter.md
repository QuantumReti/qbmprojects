# Blog-to-Markdown Converter Skill

**Purpose:** Convert blog articles/web content into formatted markdown files with proper frontmatter, preserved links, and source attribution. Designed for migrating website content into GitHub repositories while maintaining internal/external link integrity and linking back to the original source.

**Status:** Reusable skill for QBM Projects and partner websites

---

## Workflow Overview

### Input Requirements
User provides:
- **Blog content** (full text, including title, body, any metadata)
- **Website source URL** (where the blog lives)
- **Target repository** (owner/repo format)
- **Target directory** (e.g., `blog/`, `content/blog/`, `articles/`)
- **Optional:** Author, publication date, featured image URL

### Processing Steps

1. **Extract Metadata**
   - Parse title, date, author (if available)
   - Identify source URL and website domain
   - Determine service category or tags

2. **Format Content**
   - Convert plain text to markdown structure
   - Create proper heading hierarchy (H1 → H2 → H3)
   - Format lists, tables, and code blocks
   - Add line breaks for readability

3. **Preserve Links**
   - Identify all internal links (same domain) → keep as `/path/` or full URLs
   - Identify all external links (other domains) → preserve with full URLs
   - Convert reference links to numbered footnotes format `[text][n]`
   - Add source attribution section with footnote details

4. **Create Frontmatter**
   - YAML frontmatter with:
     ```yaml
     ---
     title: "Article Title"
     date: YYYY-MM-DD
     source_url: "https://original-website.com/article"
     website: "https://original-website.com"
     service: "Service Category"
     location: "Geographic Location (if applicable)"
     author: "Author Name (if available)"
     ---
     ```

5. **Add Table of Contents**
   - Generate auto-linked TOC from H2 headers
   - Include internal anchor navigation

6. **Include Call-to-Action**
   - Link back to original website/service page
   - Add "Recommended Reading" section with related internal links
   - Include source attribution at footer

7. **Commit to Repository**
   - File path: `{target_directory}/{slug-from-title}.md`
   - Commit message: `Add blog: {Article Title}`
   - Default branch: `main` (or specified branch)

---

## File Structure Template

```markdown
---
title: "Article Title"
date: YYYY-MM-DD
source_url: "https://website.com/article-path"
website: "https://website.com"
service: "Service Name"
location: "Location/Region"
author: "Author Name"
---

# Article Title

[Introductory paragraph or summary]

## Table of Contents
1. [Section One](#section-one)
2. [Section Two](#section-two)
...

[Full article content with headers, lists, tables]

---

## Call-to-Action Section

**[Learn More / Request Quote](https://website.com/service-page)**

---

## Recommended Reading
- [Related Article](https://website.com/related)
- [Related Guide](https://website.com/guide)

---

## Sources
[n]: Full source attribution with URL

---

**Original Article:** https://website.com/article-path

**Website:** https://website.com

*Content published by [Business Name](https://website.com)*
```

---

## Usage Instructions

### For QBM Projects Blogs

**Example Command:**
```
@Copilot Convert this blog to markdown:
- Website: https://www.qbmprojects.com.au
- Target Repo: QuantumReti/qbmprojects
- Target Directory: blog/
- Source Page: https://www.qbmprojects.com.au/services/bathroom-renovation
- Content: [paste full blog text]
```

**Expected Output:**
- Markdown file created at `blog/{slug}.md`
- Frontmatter pointing to https://www.qbmprojects.com.au/services/bathroom-renovation
- All links preserved
- Committed to `main` branch with descriptive message

### For Partner Websites

**Generic Template:**
```
@Copilot Convert blog using blog-to-markdown skill:
- Website: [website URL]
- Target Repo: [owner/repo]
- Target Directory: [directory path]
- Source URL: [source page URL]
- Content: [paste blog text]
```

---

## Customization Options

### Link Handling
- **Internal links:** Preserve as-is or convert to repo-relative paths
- **External links:** Keep full URLs with descriptive anchors
- **Reference links:** Use numbered footnote system `[text][n]` with source list

### Frontmatter Variants

**Minimal** (basic blogs):
```yaml
title, date, source_url, website
```

**Standard** (business services):
```yaml
title, date, source_url, website, service, location
```

**Extended** (news/articles):
```yaml
title, date, source_url, website, author, category, tags, featured_image
```

### Directory Structure Options
- Flat: `blog/article-title.md`
- By Category: `blog/services/article-title.md`
- By Date: `blog/2026/10/article-title.md`
- By Year/Month: `blog/2026-10-article-title.md`

---

## Quality Checklist

Before finalizing each markdown file:

- [ ] Frontmatter is complete and valid YAML
- [ ] Title matches original article
- [ ] Date is accurate (YYYY-MM-DD format)
- [ ] All internal links preserved and functional
- [ ] All external links have full URLs
- [ ] Source URL and website links point to originals
- [ ] Table of contents uses proper anchor links
- [ ] Call-to-action link points to appropriate service page
- [ ] No broken references or dead links
- [ ] Markdown formatting is clean (proper spacing, list items, etc.)
- [ ] File slug is descriptive and URL-safe (kebab-case)
- [ ] Commit message is descriptive

---

## Examples

### Example 1: QBM Projects Service Blog
**Input:** Blog from https://www.qbmprojects.com.au/services/bathroom-renovation
**Output:** `blog/should-you-keep-bath-or-replace-with-shower.md`
**Links:** Back to bathroom-renovation service page
**Repo:** QuantumReti/qbmprojects

### Example 2: Partner Business Blog
**Input:** Blog from partner website about industry topic
**Output:** `content/blog/industry-topic-title.md`
**Links:** Back to original business site
**Repo:** partner-owner/partner-repo

---

## Implementation Notes

- This skill is **repeatable** for any website + repository combination
- **No manual link checking needed** — all links are preserved from source
- **Frontmatter is flexible** — adjust fields based on website/business needs
- **Can be extended** — add custom fields, tags, or metadata as needed
- **Works with any markdown-capable repo** (GitHub, GitLab, etc.)

---

## Related Skills
- `file-understanding` — for deeper file/content analysis
- `semantic-code-search` — if searching for related content in repo
- `repo-grounding` — for identifying correct repo structure

---

**Last Updated:** 2026-10-01
**Maintained By:** QuantumReti
**Status:** Active
