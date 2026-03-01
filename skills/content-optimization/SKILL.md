---
name: content-optimization
description: Use when optimizing a page for SEO, improving on-page elements like title tags, meta descriptions, headings, internal links, or evaluating content quality, E-E-A-T signals, semantic coverage, or content freshness for ranking improvement
---

# Content Optimization

## Overview

On-page optimization workflow for existing or new content. Analyzes a page's SEO elements — title, meta description, headings, content quality, semantic coverage, internal links — and produces a specific optimization brief with prioritized recommendations.


## The Iron Law

```
SPECIFIC RECOMMENDATIONS OR IT DIDN'T HAPPEN.
```

"Improve your title tag" is not a recommendation. "Change your title to `Best CRM Software for Small Business (2025 Guide)`" is. Every output from this skill must be concrete enough to implement without interpretation.

## Checklist

You MUST create a task for each of these items and complete them in order:

1. **Gather page data** — URL, target keyword(s), current rankings if known
2. **Fetch and analyze page** — Get page source, extract key elements
3. **Title tag analysis** — Length, keyword placement, CTR optimization, uniqueness
4. **Meta description** — Length, compelling copy, keyword inclusion, call-to-action
5. **Heading structure** — H1 presence/uniqueness, heading hierarchy, keyword usage in headings
6. **Content quality** — Depth, E-E-A-T signals, readability, unique value, freshness
7. **Semantic coverage** — Related entities and topics covered vs top-ranking pages
8. **Internal linking** — Anchor text, link equity flow, orphan page check, contextual relevance
9. **Image optimization** — Alt text, file size, format, descriptive filenames
10. **Cannibalization check** — Other pages targeting the same keyword
11. **Prioritize recommendations** — Impact vs effort for each finding
12. **Generate optimization brief** — Specific, actionable changes with expected impact

## The Process

### Step 1: Gather page data

Ask the user:
- What URL are we optimizing?
- What is the target keyword (primary + any secondary keywords)?
- What's the current ranking position, if known?
- What is the page's goal? (Rank, convert, inform, link magnet)

### Step 2: Fetch and analyze page

- Use WebFetch to retrieve the page source
- Extract: title tag, meta description, all headings (H1-H6), word count, internal/external links, images, structured data
- Note the page template/type (article, product, category, homepage, landing page)

### Step 3: Title tag analysis

Evaluate:
- **Length:** 50-60 characters (display limit in SERPs). Flag if truncated.
- **Keyword placement:** Primary keyword should appear early (first 40 characters preferred)
- **CTR optimization:** Is it compelling? Does it include a value proposition, number, or emotional hook?
- **Uniqueness:** Is this title unique across the site or duplicated?
- **Brand:** Does it include brand name? (Usually appended with `| Brand`)

Provide a recommended title tag if improvements are needed.

### Step 4: Meta description

Evaluate:
- **Length:** 150-160 characters. Flag if missing or truncated.
- **Keyword inclusion:** Primary keyword should appear naturally
- **Compelling copy:** Does it make someone want to click? Is there a clear value proposition?
- **Call-to-action:** Does it prompt the next step? ("Learn how...", "Discover...", "Find out...")
- **Uniqueness:** Not duplicated across the site

Provide a recommended meta description if improvements are needed.

### Step 5: Heading structure

Evaluate:
- **H1:** Exactly one H1 per page. Contains primary keyword. Matches search intent.
- **Heading hierarchy:** Proper nesting (H2 under H1, H3 under H2). No skipped levels.
- **Keyword usage:** Primary and secondary keywords in H2s where natural
- **Descriptive headings:** Headings should describe content below them, not be generic ("Our Services")
- **Scanability:** Can a reader understand the page structure from headings alone?

### Step 6: Content quality

Evaluate:
- **Depth:** Word count relative to top-ranking pages. Is the content comprehensive?
- **E-E-A-T signals:**
  - **Experience:** First-hand experience, original data, real examples
  - **Expertise:** Author credentials, accurate information, technical depth
  - **Authoritativeness:** Citations, references, external validation
  - **Trustworthiness:** Accuracy, transparency, clear sourcing
- **Readability:** Sentence length, paragraph length, jargon level appropriate for audience
- **Unique value:** What does this page offer that competitors don't?
- **Freshness:** Is the content up to date? Are dates, statistics, references current?
- **Above the fold:** Does the content immediately address the search query, or is it buried under preamble?

### Step 7: Semantic coverage

- Identify the top 3-5 ranking pages for the target keyword (use WebSearch)
- Compare topics and entities covered by competitors vs this page
- Flag missing subtopics that top-ranking pages consistently cover
- Identify terms and concepts related to the primary keyword that should appear naturally
- Don't stuff keywords — identify genuine topic gaps

### Step 8: Internal linking

Evaluate:
- **Inbound internal links:** How many other pages link to this page? Is it well-connected?
- **Outbound internal links:** Does this page link to relevant related content?
- **Anchor text:** Are internal link anchors descriptive and keyword-relevant (not "click here")?
- **Contextual relevance:** Are links placed within relevant content, not just footer/sidebar?
- **Link equity:** Does the page receive links from high-authority pages on the site?

### Step 9: Image optimization

Evaluate:
- **Alt text:** Descriptive, includes keywords where natural, not stuffed
- **File format:** WebP or AVIF preferred, appropriately sized
- **Dimensions:** Explicit width/height attributes (prevents CLS)
- **Filenames:** Descriptive filenames (not IMG_001.jpg)
- **Lazy loading:** Non-critical images should be lazy-loaded (but NOT the LCP image)

### Step 10: Cannibalization check

- Search the site for other pages targeting the same or very similar keywords
- Use `site:domain.com "keyword"` via WebSearch
- If multiple pages compete for the same keyword:
  - Identify the strongest page (most links, best content)
  - Recommend consolidation, canonical, or differentiation strategy
  - Flag to `seo-superpowers:content-coverage` for broader content planning

### Step 11: Prioritize recommendations

Score each recommendation:

| Priority | Criteria |
|----------|----------|
| **High impact, low effort** | Title tag changes, meta description, fixing missing H1 — do these first |
| **High impact, high effort** | Content depth improvements, semantic gaps, E-E-A-T — schedule these |
| **Low impact, low effort** | Image alt text, minor heading tweaks — batch these |
| **Low impact, high effort** | Skip or deprioritize |

### Step 12: Generate optimization brief

Output format:

**Page Summary:** URL, target keyword, current position, page type

**Quick Wins** (implement immediately):
- Specific title tag recommendation
- Specific meta description recommendation
- H1 fix if needed

**Content Improvements** (schedule):
- Specific sections to add/expand
- E-E-A-T improvements
- Semantic gaps to fill

**Technical Fixes:**
- Internal linking recommendations (specific pages to link to/from)
- Image optimizations
- Cannibalization resolution

**Recommended Title:** `[exact title tag]`
**Recommended Meta Description:** `[exact meta description]`
**Recommended H1:** `[exact H1]`

## Red Flags - STOP and Follow Process

If you catch yourself:
- Optimizing without checking what currently ranks — you're working blind
- Giving vague advice ("improve your headings") instead of exact recommendations — redo it
- Skipping the semantic coverage step — you're optimizing in a vacuum
- Not checking for cannibalization — you might be making the problem worse
- Treating E-E-A-T as a checklist ("add author bio, done!") — it's a quality framework, not a checkbox exercise
- Suggesting changes that hurt readability for the sake of keyword placement — reconsider

## Common Rationalizations

| Excuse | Reality |
|--------|---------|
| "The title just needs a small tweak" | Did you check what ranks? Did you analyze CTR? Write the exact recommended title. |
| "We don't need to check competitors" | You're optimizing in a vacuum. Check what Google thinks is the best answer. |
| "E-E-A-T doesn't apply to this niche" | E-E-A-T applies to every page Google ranks. The signals differ by niche, but the framework is universal. |
| "Internal linking isn't that important" | Internal links are the most underused lever in SEO. You control them completely. |
| "Let's just fix the obvious stuff" | "Obvious" without data is guessing. Follow the process. |
| "The content is fine, just needs on-page tweaks" | Did you check content depth vs competitors? Did you check semantic coverage? "Fine" is not an assessment. |

## Key Principles

- Optimize for users first, search engines second — if advice hurts readability, reconsider
- One primary keyword per page, with semantic supporting terms
- Always check what currently ranks — don't optimize in a vacuum
- E-E-A-T is a quality framework, not a checklist — signals should be natural, not forced
- Provide exact recommendations, not vague advice — "change title to X" not "improve your title"
