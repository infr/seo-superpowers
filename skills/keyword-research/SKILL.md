---
name: keyword-research
description: Use when researching keywords, identifying search terms to target, analyzing search intent, finding content opportunities, clustering keywords by topic, assessing keyword difficulty, or building a keyword strategy for a site or topic
---

# Keyword Research

## Overview

Process for discovering, evaluating, and organizing keyword opportunities. Moves from seed discovery through expansion, intent classification, clustering, and prioritization to produce a keyword map tied to content.


## The Iron Law

```
A KEYWORD LIST WITHOUT INTENT AND CONTENT MAPPING IS NOT RESEARCH. IT'S A SPREADSHEET.
```

The deliverable is not "100 keywords sorted by volume." It's prioritized topic clusters, classified by intent, mapped to specific pages. If the output doesn't answer "what content do we create or optimize, and why?", the research isn't done.

## Checklist

You MUST create a task for each of these items and complete them in order:

1. **Define scope** — Business goals, target audience, topic area, geographic focus
2. **Seed keyword discovery** — Brainstorm seeds from business, products, audience pain points
3. **Expand keyword universe** — Related terms, questions, long-tail, modifiers, semantic variations
4. **Classify search intent** — Informational, navigational, commercial, transactional for each keyword
5. **Assess difficulty & opportunity** — Volume, competition, current rankings, SERP features
6. **Cluster keywords** — Group by topic/intent, identify pillar and supporting content
7. **Prioritize** — Score by impact (volume x intent fit x ranking feasibility)
8. **Map to content** — Assign clusters to existing pages or new content needs
9. **Generate keyword map** — Output prioritized keyword clusters with intent, volume, difficulty, target URLs

## The Process

### Step 1: Define scope

Ask the user (one question at a time):
- What does the business do? What products/services?
- Who is the target audience? What problems do they have?
- What topic area or vertical are we focusing on?
- Any geographic focus (national, local, international)?
- What are the business goals? (Traffic, leads, sales, awareness)
- Are there existing rankings or is this a new domain?

### Step 2: Seed keyword discovery

Generate seed keywords from:
- Core products/services and their variations
- Audience pain points and questions
- Industry terminology and jargon
- Competitor brand and product names (for gap analysis)
- Use the user's domain expertise — they know their customers' language

Aim for 10-30 seed keywords covering the scope.

### Step 3: Expand keyword universe

For each seed keyword, expand using:
- **Modifiers:** "best", "how to", "vs", "review", "cheap", location modifiers
- **Questions:** "what is", "how does", "why", "when to", "can you"
- **Long-tail variations:** More specific phrases with lower competition
- **Semantic variations:** Synonyms, related concepts, LSI terms
- **Related searches:** Use WebSearch to check "People Also Ask" and related searches for seeds

Data gathering:
- **MCP path:** Use WebSearch for each seed to see actual SERPs, extract PAA and related searches
- **Manual fallback:** Ask user for keyword tool export (Ahrefs, SEMrush, Moz, Google Keyword Planner) in CSV format with columns: keyword, volume, difficulty, current rank

### Step 4: Classify search intent

For each keyword, classify intent:

| Intent | Signal | Example |
|--------|--------|---------|
| **Informational** | "what is", "how to", "guide", "tutorial" | "how to fix a leaky faucet" |
| **Navigational** | Brand names, specific product names | "ahrefs pricing" |
| **Commercial** | "best", "review", "vs", "top 10", comparison | "best CRM for small business" |
| **Transactional** | "buy", "price", "discount", "near me", "order" | "buy running shoes online" |

When unclear, check the actual SERP — what type of content ranks tells you what Google considers the intent.

### Step 5: Assess difficulty & opportunity

For each keyword, evaluate:
- **Search volume:** Monthly search volume (if available from user's tool data)
- **Competition:** Who currently ranks? How strong are they? How many domains compete?
- **Current position:** Does the site already rank? Where?
- **SERP features:** Featured snippets, PAA, video carousels, AI Overviews — these change the click-through opportunity
- **Content gap:** Does the site have content for this keyword? How does it compare to what ranks?

### Step 6: Cluster keywords

Group keywords into topic clusters:
- **Pillar topic:** Broad topic that could be a comprehensive page (e.g., "CRM software")
- **Supporting keywords:** Specific subtopics that link to the pillar (e.g., "CRM for real estate", "CRM vs spreadsheet", "how to choose a CRM")
- Keywords sharing the same intent and similar SERP results belong in the same cluster
- Each cluster should map to one page (avoid splitting a cluster across multiple pages)

### Step 7: Prioritize

Score each cluster using:

**Impact Score = Volume x Intent Fit x Ranking Feasibility**

- **Volume:** Total monthly searches across the cluster
- **Intent fit:** How well the intent matches business goals (transactional > commercial > informational for revenue goals)
- **Ranking feasibility:** How realistic is it to rank given current authority, content, and competition?

Rank clusters by impact score. Flag quick wins: keywords where the site ranks positions 5-20 (within striking distance).

### Step 8: Map to content

For each prioritized cluster:
- **Existing page?** Assign cluster to the best matching existing page for optimization
- **New content needed?** Define the content type, format, and scope
- **Cannibalization risk?** Check if multiple existing pages target the same cluster — consolidate if needed
- **Content format:** Match format to intent (how-to → step-by-step guide, comparison → feature table, etc.)

### Step 9: Generate keyword map

Output a structured keyword map:

| Priority | Cluster | Primary Keyword | Volume | Intent | Difficulty | Target URL | Action |
|----------|---------|----------------|--------|--------|------------|------------|--------|
| 1 | ... | ... | ... | Commercial | Medium | /existing-page | Optimize |
| 2 | ... | ... | ... | Informational | Low | (new) | Create |

Include:
- Supporting keywords for each cluster
- Quick wins highlighted separately
- Content brief notes for new content needs

## Red Flags - STOP and Follow Process

If you catch yourself:
- Sorting keywords by volume and calling it a strategy — volume is one signal, not the strategy
- Skipping intent classification — a 10k-volume informational keyword is worthless to a site that needs sales
- Delivering individual keywords instead of clusters — isolated keywords don't map to content
- Not checking the actual SERP — what ranks tells you what Google thinks the intent is
- Ignoring the user's domain knowledge — they know their customers' language. Tools don't.
- Producing a keyword list with no content mapping — that's a spreadsheet, not research

## Common Rationalizations

| Excuse | Reality |
|--------|---------|
| "Let's just target the highest volume keywords" | High volume with wrong intent = wasted effort. A 100-volume "buy X" keyword drives more revenue than a 10k-volume "what is X" keyword. |
| "We'll figure out content mapping later" | Keywords without content mapping are just data. The mapping IS the deliverable. |
| "Intent is obvious from the keyword" | Often wrong. "CRM software" could be informational, commercial, or navigational. Check the SERP. |
| "We don't need to cluster, just prioritize" | Individual keywords compete with each other. Clustering prevents cannibalization and builds topical authority. |
| "Difficulty scores tell us what to target" | Difficulty scores are estimates from tools, not Google. A DR-20 site can rank for "high difficulty" keywords if the content is the best answer. |
| "We have enough keywords, skip expansion" | The best opportunities are often in the long-tail variants you haven't found yet. |

## Key Principles

- Intent is more important than volume — a 100-volume transactional keyword can beat a 10k informational one
- Cluster first, prioritize second — individual keywords are less useful than topic clusters
- Always map keywords to content — a keyword list without content mapping is incomplete
- Consider the full SERP — if a keyword triggers featured snippets, video carousels, or AI overviews, that changes the strategy
- Use the user's domain expertise — they know their customers' language better than any tool
