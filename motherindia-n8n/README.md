# Mother India Queen Street - n8n Growth System

Ready-to-import starter workflows built around the KPI **10 Queen Street orders/day**.

## Workflows
- `01_daily_revenue_monitor.json` - orders, sessions, revenue, CVR, order gap.
- `02_gsc_seo_opportunity_engine.json` - GSC query/page opportunity scoring.
- `03_apify_competitor_intelligence.json` - Apify SERP/Maps competitor collection.
- `04_daily_growth_agent.json` - turns KPI + SEO + competitor data into top 3 daily actions.

## Setup
Connect Google OAuth/Search Console, GA4, and Apify credentials in n8n. No API keys are stored in these files. Set the Queen Street location identifier used by your ecommerce analytics before activating.

Ahrefs is intentionally an extension point for the next production pass; enrich keyword records with volume, difficulty, CPC, traffic potential and competitor position.

## Deployment
Import each JSON into n8n, configure credentials/placeholders, test manually, then activate schedules. Keep CMS publishing approval-based until validated.