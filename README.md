# Cross-Channel Paid Media Audit: Google Ads, Meta Ads & CRM Pipeline Attribution

## 1. Executive Summary & Business Position
> **The Position We Take:** Immediately reallocate **$2,840/month in wasted Q4 ad spend** from *Meta Stories Broad Awareness (`CMP-M03`)* into *Google Search Enterprise BI Exact (`CMP-G01`)* and *Meta Feed Decision-Maker Retargeting (`CMP-M01`)*. Capping daily spend on top-of-funnel Reels at **$450/day** eliminates diminishing marginal returns and improves blended B2B ROAS from **1.84x to an estimated 2.45x** without increasing total marketing budget.

---

## 2. Real Business Problem (Multi-Departmental Scope)
Platform-reported ROAS inside Google Ads and Meta Ads Manager inflated Q3 performance due to duplicate pixel firing and unverified top-of-funnel leads. Three departments needed a unified source of truth:
* **CMO / Growth Leadership:** Where is our true blended Customer Acquisition Cost (CAC) across Google and Meta when measured against closed-won revenue rather than platform clicks?
* **Paid Media Operations:** At what exact daily spend threshold does each campaign hit audience saturation and diminishing marginal returns?
* **RevOps / Sales Leadership:** Which ad placements generate high-intent Sales Qualified Leads (SQLs) versus junk form fills that stall SDR pipeline velocity?

---

## 3. System Architecture & Multi-Source Data Enrichment
This project moves beyond static ad-platform exports by joining two distinct data sources across a 3-tool stack:
1. **Source 1 — Google Ads & Meta Marketing Graph APIs (`/data/cross_channel_ad_spend_daily.csv`):** Daily campaign spend, impressions, clicks, placement metadata, and raw platform conversions.
2. **Source 2 — HubSpot/Salesforce CRM Pipeline & GA4 Attribution Export (`/data/crm_pipeline_attribution_lookup.csv`):** Enriches campaign rows with verified MQL-to-SQL progression rates, sales cycle lag, and actual closed-won contract value.
3. **Tool Stack:** **Python** (`adspend_api_crm_pipeline.py` for API ingestion, data cleaning & CRM enrichment) $\rightarrow$ **SQL** (`roas_and_spend_efficiency.sql` for quartile marginal ROAS) $\rightarrow$ **Power BI DAX** (`paid_media_dax_measures.dax` for executive self-serve filtering).

---

## 4. Key Analytical Findings
| Platform & Campaign | Funnel Stage | Total Spend ($) | Verified SQLs | Blended CAC ($) | True ROAS | Action Taken |
| :--- | :--- | :---: | :---: | :---: | :---: | :--- |
| **Google Search - Enterprise BI Exact** | Bottom | $12,890 | 184 | $165.25 | **2.91x** | **Scale +25%** |
| **Meta Feed - Retargeting Decision Makers** | Bottom | $9,410 | 112 | $196.04 | **2.19x** | **Scale +15%** |
| **Google Search - Data Analytics Phrase** | Mid | $10,620 | 98 | $252.85 | **1.62x** | Maintain |
| **Google PMax - B2B LeadGen** | Mid | $15,480 | 94 | $387.00 | **0.93x** | Cap Daily Budget |
| **Meta Stories - Broad Awareness Q3** | Top | $8,540 | 14 | $1,423.33 | **0.15x** | **Pause / Reallocate** |

* **Diminishing Marginal Returns (`NTILE(4)` Spend Analysis):** When *Google PMax (`CMP-G03`)* scales from Quartile 2 ($480/day) to Quartile 4 ($595/day), marginal CAC surges by **+44%** while conversion volume remains flat.

---



---

## 5. Repository Structure
* `/python/adspend_api_crm_pipeline.py` — Automated API ingestion, UTM data cleaning, and CRM enrichment script.
* `/dax/paid_media_dax_measures.dax` — Production Power BI DAX measures for dynamic CAC, ROAS, and pacing cards.
* `/sql/roas_and_spend_efficiency.sql` — Analytical SQL queries for funnel efficiency, wasted spend, and quartile marginal returns.
* `/data/cross_channel_ad_spend_daily.csv` — Daily campaign performance dataset.
* `/data/crm_pipeline_attribution_lookup.csv` — Secondary CRM lead verification and margin enrichment table.
* `/visuals/roas_efficiency_audit.png` — Dark-mode campaign ROAS diagnostic chart.
