---
name: analytics-mcp
description: Reference skill for using the analytics-mcp MCP server (GA4 Data API). Invoke this skill when you need to construct GA4 queries — property discovery, run_report parameters, dimension/metric combos, filters, date ranges. Not a workflow skill; other skills call this when they need GA4 data.
---

# Analytics MCP — GA4 Query Reference

## Overview

Reference for the `analytics-mcp` MCP server, which exposes the GA4 Data API. This skill teaches you how to discover properties, construct reports, filter to organic traffic, and use the right dimension/metric combinations for SEO analysis.

This is not a workflow skill — it has no checklist or tasks. Other skills (especially `seo-superpowers:analytics-review` and `seo-superpowers:seo-reporting`) invoke this when they need to pull GA4 data.

## The Iron Law

```
FILTER STRUCTURE KEYS USE SNAKE_CASE. DIMENSION AND METRIC NAMES KEEP THEIR GA4 CAMELCASE.
```

Two naming conventions coexist:
- **Filter/query structure keys** are snake_case (protobuf format): `field_name`, `string_filter`, `match_type`, `and_group`, `start_date`, `order_type`
- **Dimension and metric names** keep their GA4 camelCase: `sessionDefaultChannelGroup`, `totalUsers`, `pagePath`, `bounceRate`

Google's REST documentation shows camelCase for everything. The analytics-mcp tool uses protobuf format for structure keys. Dimension and metric names are the same in both formats.

## Detection

Before using analytics-mcp, check if it's available:

1. Call `get_account_summaries` with no arguments
2. If it succeeds, the MCP server is connected and authenticated
3. If it fails, fall back to asking the user for CSV exports

## Property Discovery

### Step 1: List accounts and properties

```
get_account_summaries()
```

Returns accounts with their properties. Each property has a `property` field like `properties/123456789`. Note the property ID for all subsequent calls.

### Step 2: Get property details

```
get_property_details(property_id: 123456789)
```

Returns property configuration: display name, time zone, currency, industry category, create time. Use this to confirm you have the right property and to understand the timezone for date-based queries.

### Step 3: Check custom dimensions (optional)

```
get_custom_dimensions_and_metrics(property_id: 123456789)
```

Returns custom dimensions and metrics configured on the property. Useful when standard dimensions don't cover the user's tracking setup.

## run_report Reference

### Required parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `property_id` | int or string | GA4 property ID. Accepts `123456789` or `"properties/123456789"` |
| `date_ranges` | array of objects | At least one date range (see Date Range Patterns below) |
| `dimensions` | array of strings | GA4 dimension names |
| `metrics` | array of strings | GA4 metric names |

### Optional parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `dimension_filter` | object | FilterExpression applied to dimensions |
| `metric_filter` | object | FilterExpression applied to metrics |
| `order_bys` | array of objects | Sorting — by dimension or metric |
| `limit` | int | Max rows returned (max 250,000) |
| `offset` | int | Row offset for pagination (0-indexed) |
| `currency_code` | string | ISO 4217 currency code |
| `return_property_quota` | bool | Include quota info in response |

## Date Range Patterns

### Last 30 days
```json
[{"start_date": "30daysAgo", "end_date": "yesterday", "name": "Last30Days"}]
```

### Month-over-month comparison
```json
[
  {"start_date": "30daysAgo", "end_date": "yesterday", "name": "Current"},
  {"start_date": "60daysAgo", "end_date": "31daysAgo", "name": "Previous"}
]
```

### Year-over-year comparison
```json
[
  {"start_date": "2026-01-01", "end_date": "2026-01-31", "name": "ThisYear"},
  {"start_date": "2025-01-01", "end_date": "2025-01-31", "name": "LastYear"}
]
```

### Last 7 days
```json
[{"start_date": "7daysAgo", "end_date": "yesterday", "name": "Last7Days"}]
```

### Yesterday only
```json
[{"start_date": "yesterday", "end_date": "yesterday", "name": "Yesterday"}]
```

Relative dates accepted: `today`, `yesterday`, `NdaysAgo` (e.g. `30daysAgo`, `90daysAgo`). Absolute dates use `YYYY-MM-DD` format.

## The Organic Traffic Filter

This is the single most important filter for SEO analysis. Use it whenever you need organic-only data:

```json
{
  "filter": {
    "field_name": "sessionDefaultChannelGroup",
    "string_filter": {
      "match_type": 1,
      "value": "Organic Search",
      "case_sensitive": false
    }
  }
}
```

`match_type` values: `1` = EXACT, `2` = BEGINS_WITH, `3` = ENDS_WITH, `4` = CONTAINS, `5` = FULL_REGEXP, `6` = PARTIAL_REGEXP.

### Filtering to Google organic only

```json
{
  "and_group": {
    "expressions": [
      {
        "filter": {
          "field_name": "sessionDefaultChannelGroup",
          "string_filter": {"match_type": 1, "value": "Organic Search", "case_sensitive": false}
        }
      },
      {
        "filter": {
          "field_name": "sessionSource",
          "string_filter": {"match_type": 1, "value": "google", "case_sensitive": false}
        }
      }
    ]
  }
}
```

## Ordering

### By metric descending (most common)

```json
[{"metric": {"metric_name": "sessions"}, "desc": true}]
```

### By dimension alphabetically

```json
[{"dimension": {"dimension_name": "pagePath", "order_type": 1}, "desc": false}]
```

`order_type` for dimensions: `1` = ALPHANUMERIC, `2` = CASE_INSENSITIVE_ALPHANUMERIC, `3` = NUMERIC.

Dimensions and metrics in `order_bys` must also appear in the report's `dimensions` and `metrics` lists.

## SEO Report Recipes

Pre-built queries for common SEO analysis. All recipes assume you already have the `property_id`.

### 1. Organic traffic overview (by date)

What: Daily organic sessions, users, and engagement over time.

```
dimensions: ["date", "sessionDefaultChannelGroup"]
metrics: ["sessions", "totalUsers", "newUsers", "engagementRate", "averageSessionDuration"]
dimension_filter: <organic traffic filter>
date_ranges: [last 30 days]
order_bys: [{"dimension": {"dimension_name": "date", "order_type": 1}, "desc": false}]
```

### 2. Channel breakdown

What: Compare organic vs paid vs direct vs referral vs social. No dimension_filter — this query is intentionally cross-channel.

```
dimensions: ["sessionDefaultChannelGroup"]
metrics: ["sessions", "totalUsers", "newUsers", "engagementRate", "conversions"]
date_ranges: [last 30 days]
order_bys: [{"metric": {"metric_name": "sessions"}, "desc": true}]
```

### 3. Landing page performance (organic only)

What: Top landing pages by organic traffic with engagement and conversion data.

```
dimensions: ["landingPage"]
metrics: ["sessions", "totalUsers", "bounceRate", "engagementRate", "averageSessionDuration", "conversions"]
dimension_filter: <organic traffic filter>
date_ranges: [last 30 days]
order_bys: [{"metric": {"metric_name": "sessions"}, "desc": true}]
limit: 50
```

### 4. Device breakdown (organic)

What: Mobile vs desktop vs tablet for organic traffic — reveals UX issues.

```
dimensions: ["deviceCategory"]
metrics: ["sessions", "totalUsers", "bounceRate", "engagementRate", "averageSessionDuration", "conversions"]
dimension_filter: <organic traffic filter>
date_ranges: [last 30 days]
```

### 5. Geographic breakdown (organic)

What: Traffic by country for organic visitors.

```
dimensions: ["country"]
metrics: ["sessions", "totalUsers", "engagementRate", "conversions"]
dimension_filter: <organic traffic filter>
date_ranges: [last 30 days]
order_bys: [{"metric": {"metric_name": "sessions"}, "desc": true}]
limit: 20
```

### 6. Conversion analysis by channel

What: Compare conversion performance across traffic sources.

```
dimensions: ["sessionDefaultChannelGroup"]
metrics: ["sessions", "conversions", "totalRevenue", "purchaseRevenue", "userConversionRate"]
date_ranges: [last 30 days]
order_bys: [{"metric": {"metric_name": "conversions"}, "desc": true}]
```

### 7. Content engagement (organic)

What: Which pages keep organic visitors engaged longest.

```
dimensions: ["pagePath"]
metrics: ["screenPageViews", "engagementRate", "averageSessionDuration", "eventCount"]
dimension_filter: <organic traffic filter>
date_ranges: [last 30 days]
order_bys: [{"metric": {"metric_name": "screenPageViews"}, "desc": true}]
limit: 50
```

### 8. New vs returning users by channel

What: Acquisition vs retention balance for organic traffic.

```
dimensions: ["newVsReturning", "sessionDefaultChannelGroup"]
metrics: ["sessions", "totalUsers", "engagementRate", "conversions"]
date_ranges: [last 30 days]
```

### 9. Organic traffic by source

What: Break down organic traffic by search engine (Google, Bing, Yahoo, etc.).

```
dimensions: ["sessionSource"]
metrics: ["sessions", "totalUsers", "bounceRate", "engagementRate", "conversions"]
dimension_filter: <organic traffic filter>
date_ranges: [last 30 days]
order_bys: [{"metric": {"metric_name": "sessions"}, "desc": true}]
```

### 10. Landing page + source combo (organic)

What: Which pages get traffic from which search engines.

```
dimensions: ["landingPage", "sessionSource"]
metrics: ["sessions", "totalUsers", "conversions"]
dimension_filter: <organic traffic filter>
date_ranges: [last 30 days]
order_bys: [{"metric": {"metric_name": "sessions"}, "desc": true}]
limit: 100
```

## Common GA4 Dimensions for SEO

| Dimension | Description |
|-----------|-------------|
| `date` | Date in YYYYMMDD format |
| `sessionDefaultChannelGroup` | Channel grouping (Organic Search, Paid Search, Direct, etc.) |
| `sessionSource` | Traffic source (google, bing, yahoo, etc.) |
| `sessionMedium` | Traffic medium (organic, cpc, referral, etc.) |
| `sessionSourceMedium` | Combined source/medium (google / organic) |
| `landingPage` | First page of the session (path only, e.g. /blog/post) |
| `pagePath` | Page path |
| `pageTitle` | Page title |
| `deviceCategory` | desktop, mobile, or tablet |
| `country` | Country name |
| `city` | City name |
| `newVsReturning` | "new" or "returning" |
| `firstUserSource` | Source that first acquired the user |
| `firstUserMedium` | Medium that first acquired the user |

## Common GA4 Metrics for SEO

| Metric | Description |
|--------|-------------|
| `sessions` | Total sessions |
| `totalUsers` | Total users |
| `newUsers` | First-time users |
| `bounceRate` | Percentage of sessions that were not engaged (< 10s, 0 conversions, < 2 pageviews) |
| `engagementRate` | 1 - bounceRate |
| `averageSessionDuration` | Average session length in seconds |
| `screenPageViews` | Total pageviews |
| `screenPageViewsPerSession` | Pageviews per session |
| `conversions` | Total conversion events |
| `userConversionRate` | Percentage of users who converted |
| `totalRevenue` | Total revenue (includes purchases, subscriptions, ads) |
| `purchaseRevenue` | Revenue from purchases only |
| `eventCount` | Total events |

## run_realtime_report

Use for live monitoring only — not for SEO analysis. Useful when:
- Verifying tracking is working after changes
- Checking if a new page is receiving traffic right now
- Monitoring a live campaign or launch

### Key differences from run_report

| | run_report | run_realtime_report |
|---|---|---|
| Time range | Historical (date_ranges) | Last 30 minutes (no date_ranges param) |
| Dimensions | All standard + custom | Realtime dimensions only |
| Metrics | All standard + custom | Realtime metrics only |
| Custom metrics | Supported | Not supported |

### Example: Current active users by page

```
property_id: 123456789
dimensions: ["unifiedScreenName"]
metrics: ["activeUsers"]
order_bys: [{"metric": {"metric_name": "activeUsers"}, "desc": true}]
limit: 20
```

### Example: Current active users by traffic source

```
property_id: 123456789
dimensions: ["sessionSource", "sessionMedium"]
metrics: ["activeUsers"]
order_bys: [{"metric": {"metric_name": "activeUsers"}, "desc": true}]
```

### Available realtime dimensions

Realtime reports use a restricted set of dimensions. Common ones: `unifiedScreenName`, `sessionSource`, `sessionMedium`, `country`, `city`, `deviceCategory`, `platform`, `audienceName`. Session-scoped dimensions like `landingPage` and `pagePath` are **not available** in realtime reports. For the full list, see the [GA4 Realtime API schema](https://developers.google.com/analytics/devguides/reporting/data/v1/realtime-api-schema#dimensions).

## Pagination

For reports with more rows than the `limit`, use `offset` to paginate:

1. First request: `limit: 10000, offset: 0`
2. Second request: `limit: 10000, offset: 10000`
3. Continue until rows returned < limit

The response includes total row count, so you know when to stop.

## Filter Gotchas

- `dimension_filter` and `metric_filter` are applied independently — you cannot combine them with OR logic across dimension+metric conditions
- If you need complex cross-filtering, run separate reports or filter results client-side
- String filter `match_type` is an integer, not a string: `1`=EXACT, `2`=BEGINS_WITH, `3`=ENDS_WITH, `4`=CONTAINS, `5`=FULL_REGEXP, `6`=PARTIAL_REGEXP
- Numeric filter `operation` values: `1`=EQUAL, `2`=LESS_THAN, `3`=LESS_THAN_OR_EQUAL, `4`=GREATER_THAN, `5`=GREATER_THAN_OR_EQUAL
- Numeric values use `int64_value` (string-encoded integer) or `double_value` (float)

## Key Principles

- Always discover the property first — don't assume property IDs
- Use relative date ranges (`30daysAgo`, `yesterday`) for repeatable queries
- Always include the organic traffic filter for SEO analysis — unfiltered GA4 data mixes all channels
- Request only the dimensions and metrics you need — smaller queries are faster and use less quota
- Use `limit` to control response size — default can return very large result sets
- For period comparisons, use multiple date ranges in a single request instead of running separate reports
- Check `return_property_quota: true` occasionally to monitor API quota usage
