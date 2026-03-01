# Migration Checklist

Detailed pre-launch and post-launch checklists for site migrations. Used by the site-migration skill.

## Pre-Launch Checklist

### URL & Redirect Preparation
- [ ] Complete URL inventory exported (all URLs from crawl + sitemap + GSC + analytics)
- [ ] URL mapping document complete (old URL → new URL for every page)
- [ ] 301 redirects implemented for all mapped URLs
- [ ] Redirect chains eliminated (no A → B → C, only A → C)
- [ ] Redirect loops tested and eliminated
- [ ] Regex redirect patterns tested with edge cases
- [ ] High-traffic pages individually verified (top 50 by organic traffic)
- [ ] Backlinked pages individually verified (top 50 by referring domains)

### DNS & Server
- [ ] DNS TTL lowered 48 hours before migration (to 300 seconds)
- [ ] SSL certificate installed and valid for new domain (if domain change)
- [ ] Server capacity tested for expected traffic load
- [ ] CDN configured for new domain/URLs (if applicable)
- [ ] HTTP/2 or HTTP/3 enabled

### Robots & Indexation
- [ ] robots.txt on new site allows crawling (not blocking important paths)
- [ ] robots.txt references new sitemap URL
- [ ] No unintentional noindex tags on new site
- [ ] Old site's robots.txt allows crawlers to follow redirects (don't block before redirects fire)

### Sitemap
- [ ] New XML sitemap generated with all new URLs
- [ ] Old URLs removed from sitemap
- [ ] Sitemap validates (no errors, correct format)
- [ ] Sitemap size under 50MB / 50,000 URLs per file (use sitemap index if needed)

### Canonical & Hreflang
- [ ] Self-referencing canonical tags on all new URLs
- [ ] No canonical tags pointing to old URLs
- [ ] Hreflang tags updated to new URLs (if international)
- [ ] Return hreflang tags verified (every hreflang pair must be reciprocal)

### Content & On-Page
- [ ] Content parity verified (spot-check 20-30 pages across page types)
- [ ] Title tags preserved or improved (not made generic by template)
- [ ] Meta descriptions preserved or improved
- [ ] Heading structure maintained
- [ ] Images migrated with alt text intact
- [ ] Internal links updated to new URLs (not relying on redirects internally)

### Structured Data
- [ ] JSON-LD structured data present on new site
- [ ] URLs in structured data updated to new URLs
- [ ] Structured data validates without errors

### Analytics & Tracking
- [ ] GA4 tracking code on all new pages
- [ ] Goals/conversions configured
- [ ] Search Console property verified for new domain (if domain change)
- [ ] Annotation added in GA4 for migration date
- [ ] Third-party tracking updated (ads, heatmaps, etc.)

### Staging Validation
- [ ] Full crawl of staging site — no unexpected 404s
- [ ] Page speed comparable to or better than current site
- [ ] Mobile rendering verified
- [ ] JavaScript rendering verified (check rendered HTML)
- [ ] Forms and interactive elements functional
- [ ] Cross-browser testing complete

### Sign-Off
- [ ] SEO team sign-off
- [ ] Development team sign-off
- [ ] Stakeholder approval
- [ ] Rollback plan documented and tested

---

## Post-Launch Checklist

### Immediately (Day 0)

- [ ] Verify redirects working in production (test 20+ URLs manually)
- [ ] Submit new sitemap to Google Search Console
- [ ] Request indexing for top 10-20 priority pages in GSC
- [ ] Verify analytics tracking is recording data
- [ ] Check for 5xx server errors
- [ ] Monitor real-time analytics for traffic
- [ ] Check robots.txt is accessible and correct
- [ ] Verify SSL/HTTPS across all pages

### 24 Hours

- [ ] Check GSC for crawl errors
- [ ] Review server error logs for 404s and 5xx errors
- [ ] Verify Google is crawling the new site (check server logs)
- [ ] Compare traffic to same day previous week
- [ ] Check that old URLs redirect (test 50+ URLs)
- [ ] Monitor for user-reported issues

### 1 Week

- [ ] GSC Coverage report — indexing new URLs?
- [ ] GSC Coverage report — any new errors?
- [ ] Traffic comparison to baseline (weekly)
- [ ] Keyword ranking check for top 20 target keywords
- [ ] Check for old URLs still showing in Google search results (site: search)
- [ ] Fix any 404 errors found in GSC
- [ ] Raise DNS TTL back to normal

### 1 Month

- [ ] Full traffic comparison to baseline (monthly)
- [ ] Keyword ranking recovery assessment
- [ ] Indexed page count trending toward baseline
- [ ] Backlink profile check — links resolving to new URLs?
- [ ] No remaining redirect chains or loops
- [ ] User engagement metrics comparison (bounce rate, time on site)
- [ ] Conversion rate comparison

### 3 Months

- [ ] Full traffic comparison to baseline (quarterly)
- [ ] Complete ranking recovery assessment
- [ ] Indexed pages at expected levels
- [ ] Backlink equity fully transferred
- [ ] Remove any remaining temporary redirects
- [ ] Document lessons learned for future migrations
- [ ] Final migration report to stakeholders

