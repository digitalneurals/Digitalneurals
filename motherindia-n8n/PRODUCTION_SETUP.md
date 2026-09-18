# Mother India Queen Street Growth Engine v2

This is the production orchestration layer for the **10 orders/day** objective.

## Main workflow
Import `08_production_growth_engine_v2.json` into n8n.

It runs daily at 6:00 AM and executes:

1. GA4 Data API — yesterday's Queen Street sessions, ecommerce purchases and purchase revenue.
2. Google Search Console — 28-day query/page data.
3. Ahrefs API v3 — organic keyword, position, volume, difficulty and intent data.
4. Apify — live local competitor/Google Maps-style intelligence.
5. Deterministic scoring — calculates order gap and top SEO/conversion/local actions.
6. Google Sheets — appends one daily summary row.

## Required credentials in n8n

### Google OAuth2
Use a Google credential with access to:
- Google Analytics Data API
- Google Search Console API
- Google Sheets

### Ahrefs
Create HTTP Header Auth:
- Header: `Authorization`
- Value: `Bearer YOUR_AHREFS_API_KEY`

Attach it to **Ahrefs Organic Keywords**.

### Apify
Create HTTP Header Auth:
- Header: `Authorization`
- Value: `Bearer YOUR_APIFY_TOKEN`

Attach it to **Apify Local Competitors**.

## Required values

Update the Config node:
- `gaPropertyId`
- `gaLocationDimension`
- `gaLocationValue`
- `apifyActorId`
- `googleSheetId`

## Critical GA4 note

The workflow assumes Queen Street is available in GA4 as a dimension such as:

`customEvent:store_location = Queen Street`

If your ecommerce tracking uses a different custom dimension, URL, item category or event parameter, change the two GA location fields in Config before running.

## Google Sheet headers

Create a tab named `Daily Growth` with:

`date | location | target_orders | orders | order_gap | sessions | revenue | conversion_rate | average_order_value | top_actions_json`

## Recommended test sequence

1. Import but keep inactive.
2. Configure Google OAuth.
3. Run GA4 node by itself and verify Queen Street data.
4. Run GSC node.
5. Add Ahrefs bearer credential and run it.
6. Add Apify bearer credential + Actor ID and run it.
7. Connect the Google Sheet.
8. Run the full workflow manually.
9. Confirm the daily row.
10. Activate schedule.

## What is automated

The workflow automatically identifies:
- order gap against 10/day
- sessions and CVR
- GSC high-impression / low-CTR / positions 4-15 opportunities
- Ahrefs high-intent keyword opportunities
- local competitor inputs
- top three daily actions

## What is intentionally not automated

It does **not** auto-edit the website, auto-publish SEO pages or auto-send promotions. Those actions should remain approval-based until you have validated data quality and conversion tracking.
