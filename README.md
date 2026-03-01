# SEO Superpowers

You've got a website. You want it to rank. Your first instinct is to jump into an audit, or maybe start researching keywords, or tweak some title tags.

SEO Superpowers doesn't let you do that. Instead, it steps back and asks what you're actually trying to achieve. What's the business goal? Who are you competing against? What do you already have to work with?

Once you've got a strategy, *then* it guides you through the tactical work — audits, keyword research, content optimization, link analysis, reporting — as systematic workflows with decision points and concrete deliverables. Not vague advice. Not a checklist of things to Google. Specific, prioritized, actionable recommendations.

And because the skills trigger automatically, you don't need to do anything special. Your coding agent just has SEO Superpowers.

## Installation

```bash
claude plugin marketplace add infr/seo-superpowers
claude plugin install seo-superpowers
```

Start a new session and ask for SEO help. The agent should automatically invoke the `seo-triage` router and guide you to the right skill.

### Updating

```bash
claude plugin update seo-superpowers
```

## How It Works

It starts the moment you mention SEO. A triage router kicks in and figures out what you need:

1. **seo-triage** - Activates on any SEO-related request. Routes you to the right skill, or asks clarifying questions if the goal is ambiguous. Suggests skill chains for complex goals.

2. **seo-brainstorming** - Activates before tactical work. Explores goals, competitive landscape, and resources. Proposes strategy options. *Hard gate: no audits, no keyword research, no optimization until strategy is approved.*

3. **keyword-research** - Activates with strategy. Discovers keywords, classifies intent, clusters by topic, maps to content. Outputs a prioritized keyword map, not a raw list.

4. **technical-audit** - Activates when auditing a site. Checks crawlability first — nothing else matters if search engines can't reach the pages. Works through indexation, speed, structured data, mobile, security. Every finding gets a severity and a fix.

5. **content-optimization** - Activates on a specific page. Analyzes title, meta, headings, content quality, semantic coverage, internal links. Outputs exact recommendations — "change title to X", not "improve your title."

6. **analytics-review** - Activates with performance data. Connects to GA4 via MCP when available, falls back to manual exports. Every insight comes with a "so what?" — what to actually do about the finding.

7. **seo-reporting** - Activates for stakeholder communication. Adapts depth and language to the audience. Executives get KPIs and narrative. Technical teams get fix instructions.

**The agent checks for relevant skills before any task.** Mandatory workflows, not suggestions.

## What's Inside

### Discovery & Strategy
- **seo-triage** - Routes to the right skill automatically
- **seo-brainstorming** - Strategy before tactics (hard-gated)
- **keyword-research** - Intent, clustering, difficulty, content mapping
- **competitor-analysis** - SERP competitors, content/keyword/backlink gaps

### Technical Foundation
- **technical-audit** - Crawlability, indexation, CWV, structured data, security
- **site-migration** - Domain changes, URL restructures, pre/post checklists

### Content & On-Page
- **content-optimization** - Title tags, headings, E-E-A-T, semantic coverage
- **content-writing** - SEO content creation from brief to draft — intent match, structure, E-E-A-T
- **content-coverage** - Topic clusters, cannibalization, content calendar

### Off-Page & Links
- **link-analysis** - Backlink profile, toxicity, anchor text, internal links
- **digital-pr-outreach** - Linkable assets, prospect identification, outreach templates

### Measurement & Reporting
- **analytics-review** - GA4/GSC analysis, anomaly detection, conversion insights
- **seo-reporting** - Audience-adapted reports (executive, client, technical)
- **serp-trends-analysis** - Trends, SERP features, seasonal planning

### Specialized
- **local-seo** - Google Business Profile, NAP, citations, reviews
- **international-seo** - Hreflang, URL structure, localization, market prioritization
- **ai-search-optimization** - AI Overviews, entity SEO, knowledge graph

### Reference
- **analytics-mcp** - GA4 query reference for the [analytics-mcp](https://github.com/googleanalytics/google-analytics-mcp) MCP server (property discovery, report recipes, filters)

## MCP Integrations

Skills use MCP servers when available, with manual data fallbacks:

| MCP Server | Used By | Purpose |
|-----------|---------|---------|
| [`analytics-mcp`](https://github.com/googleanalytics/google-analytics-mcp) (GA4) | analytics-review, seo-reporting, analytics-mcp (reference) | Traffic, conversion, landing page data |
| WebFetch | Most skills | Page source, headers, content analysis |
| WebSearch | Most skills | SERPs, competitors, feature checks |

No MCP configured? Skills ask for exported data (CSV from Ahrefs, SEMrush, GA4, GSC).

## Philosophy

- **Strategy before tactics** - Know what you're trying to achieve before optimizing anything
- **Workflows, not checklists** - Decision points, not flat lists
- **Actionable over comprehensive** - 5 prioritized actions beat 50 observations
- **Tools-agnostic** - Works with whatever data you have

## Contributing

Skills live directly in this repository. To contribute:

1. Fork the repository
2. Create a branch for your skill
3. Follow the format in `.claude/CLAUDE.md` for skill structure
4. Submit a PR

## Credits

Inspired by [obra/superpowers](https://github.com/obra/superpowers).

## License

MIT

## Support

- **Issues**: https://github.com/infr/seo-superpowers/issues
