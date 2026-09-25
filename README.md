# 👟 Stride & Co. — Sales Performance Analysis

### Turning three years of fragmented order data into a margin-recovery roadmap for a mid-size footwear manufacturer

<p>
  <img src="https://img.shields.io/badge/Domain-Retail%20%26%20Manufacturing-1f2937?style=flat-square" alt="Domain badge"/>
  <img src="https://img.shields.io/badge/Tools-Excel%20%7C%20SQL%20%7C%20Power%20BI-2563eb?style=flat-square" alt="Tools badge"/>
  <img src="https://img.shields.io/badge/Status-Complete-16a34a?style=flat-square" alt="Status badge"/>
  <img src="https://img.shields.io/badge/Type-Portfolio%20Case%20Study-a855f7?style=flat-square" alt="Type badge"/>
</p>

---

> **Note on data:** This repository is a portfolio demonstration. "Stride & Co." is a fictional company, and all figures, KPIs and dashboard visuals below are synthetic, constructed to illustrate the analytical approach. They are not real client results.

## 📌 Executive Summary


> Stride & Co. grew top-line revenue **11.5% YoY**, yet gross margin **contracted by 3.5 points** over the same period. Leadership assumed the cause was rising material costs. This analysis shows the real driver was a **regional discounting pattern hidden inside aggregate reporting** — and quantifies what fixing it is worth.

| Metric | Value |
|---|---|
| Revenue analyzed | $18.8M across 3 fiscal years |
| Order-level records | 142,000+ |
| Regions covered | 6 |
| Product lines | 4 (Running, Casual, Athletic, Kids) |
| Margin recovery identified | **~$740K annually** |

[Executive Summary dashboard]<img width="3200" height="2000" alt="01-executive-summary" src="https://github.com/user-attachments/assets/0f5c052c-2909-45f5-a791-d63585cfd985" />


---

## 🧭 Table of Contents

1. [Business Problem](#-business-problem)
2. [Why the Problem Exists](#-why-the-problem-exists)
3. [Tools & Environment](#️-tools--environment)
4. [Methodology](#-methodology)
5. [Key Findings](#-key-findings)
6. [Dashboard](#-dashboard)
7. [Recommendations](#-recommendations)
8. [Business Impact](#-projected-business-impact)
9. [Next Steps](#-next-steps)


---

## 🎯 Business Problem

Stride & Co.'s finance team flagged a recurring issue in quarterly reviews: **revenue was growing, but profitability was not keeping pace.** Prior to this analysis, margin erosion was attributed to input cost inflation (leather, rubber, freight) — a narrative that was directionally true but incomplete, and one that pointed leadership toward the wrong lever (supplier renegotiation) instead of the actual controllable variable (discount governance).


> The brief was not "build a dashboard." It was: **find the $700K+ that's leaking out of the P&L before the next board meeting, and tell us who is responsible for the leak.**

The scope of this project was to move the conversation from *"margins are down"* to *"margins are down 3.5 points, driven primarily by a specific region and channel, and here is the corrective action with a dollar value attached."*

---

## 🔍 Why the Problem Exists

Root-cause investigation, not just symptom reporting, was the priority. Three structural issues surfaced during data validation, before any dashboarding began:

| Root Cause | Evidence | Business Consequence |
|---|---|---|
| **Discount authority was decentralized** | Regional sales leads could apply discounts up to 25% without approval workflow | Discounting became a default negotiation tactic rather than an exception |
| **Reporting was aggregated at the company level** | Monthly P&L reviews showed blended margin only | Regional/rep-level discount abuse was invisible until this analysis disaggregated it |
| **No SKU-level cost visibility in sales reporting** | Sales team optimized for units sold, not contribution margin | High-volume, low-margin SKUs were treated as equally "successful" as high-margin SKUs |

This reframes the business problem from a *cost* problem (external, harder to control) to a *governance and visibility* problem (internal, immediately actionable) — which materially changes the recommendation set later in this document.

---

## 🛠️ Tools & Environment

| Stage | Tool | Purpose |
|---|---|---|
| Data extraction & querying | **SQL** (PostgreSQL) | Pulled and joined order, product, region, and rep tables from the transactional database |
| Data cleaning & shaping | **Excel** (Power Query) | Deduplication, type correction, outlier flagging, calculated fields |
| Modeling & KPI logic | **Excel** | DAX-style measures prototyped and validated before BI build |
| Visualization & reporting | **Power BI** | Interactive executive dashboard, drill-through by region/rep/SKU |
| Version control & documentation | **Git / GitHub** | Query versioning, changelog, this README |

---

## 🧪 Methodology

### 1. Data Cleaning & Validation

- Consolidated 4 source tables (`orders`, `products`, `regions`, `sales_reps`) via SQL joins into a single analysis-ready fact table.
- Identified and resolved **1,860 duplicate order records** (0.9M in double-counted revenue before dedup).
- Standardized inconsistent region naming (`"NE"`, `"North-East"`, `"Northeast"` → single canonical value).
- Flagged and reviewed **312 statistical outliers** in unit price and discount fields (>3 standard deviations) — 41 were confirmed data-entry errors and corrected; the remainder were legitimate bulk/wholesale orders and retained.
- Validated referential integrity: confirmed every `order_id` mapped to a valid SKU, region, and rep before proceeding — 0% orphaned records after cleanup.


### 2. KPI Framework

KPIs were defined *before* dashboard design, tied directly to the business question rather than to whatever fields happened to be available:

| KPI | Definition | Why It Matters |
|---|---|---|
| Gross Margin % | (Revenue − COGS) / Revenue | Primary health metric for the business problem |
| Net Discount Rate | Total discount $ / Gross Sales $ | Isolates the controllable margin lever |
| Contribution Margin per SKU | (Unit Price − Unit Cost − Avg. Discount) × Units | Reframes "top seller" away from volume alone |
| Rep-Level Discount Variance | Std. deviation of discount % by rep, within region | Identifies individual outlier behavior vs. regional norms |
| Revenue per Order | Total Revenue / Order Count | Detects channel mix shifts (bulk vs. retail) |

### 3. Exploratory Analysis

- Trended revenue, margin %, and discount rate monthly across 3 years to separate seasonal effects from structural decline.
- Segmented margin performance by region × product line × channel to locate where the blended average was masking outliers.
- Ran correlation checks between discount rate and rep tenure — ruled out "inexperienced reps" as the cause (correlation was negligible).

[Exploratory trend diagnostics]<img width="3200" height="2000" alt="04-exploratory-trends" src="https://github.com/user-attachments/assets/d44de3c9-80af-401f-b110-ac8f24184e86" />


### 4. Visualization & Dashboard Design

Built as a 3-page executive Power BI report, designed for a 5-minute leadership readout rather than open-ended self-serve exploration:

- **Page 1 — Executive Summary:** headline KPIs, YoY trend, margin bridge.
- **Page 2 — Regional Deep Dive:** discount rate and margin by region, drill-through to rep level.
- **Page 3 — SKU & Product Line:** contribution margin ranking, reframing "best sellers" by profitability.

[Regional deep dive dashboard]<img width="3200" height="2000" alt="02-regional-deep-dive" src="https://github.com/user-attachments/assets/90702998-ac6b-4499-a247-a85a00162133" />

[SKU and product line dashboard]<img width="3200" height="2000" alt="03-sku-product-line" src="https://github.com/user-attachments/assets/b54771bb-6d48-42d3-a5dd-fa157330dc5b" />


### 5. Business Interpretation

Every chart in the dashboard is paired with a plain-language "so what," because a stakeholder reading this in a board deck should not have to interpret the visual themselves. Interpretation was validated against the raw data before being finalized as a finding (see below).

---

## 📊 Key Findings

| # | Finding | Supporting Data |
|---|---|---|
| 1 | **One region drives 61% of total discount dollars** while contributing only 34% of revenue | Southeast region: 19.8% avg. discount vs. 8.1% company-wide |
| 2 | **A small group of reps (12% of the sales force) issued 47% of all discounts above policy threshold** | Top 6 reps by discount frequency, cross-referenced against approval logs |
| 3 | **The "best-selling" SKU by unit volume ranks 9th of 12 by contribution margin** | Running-line SKU RN-204: highest units, 6.2% margin vs. 22.4% category average |
| 4 | **Margin decline is not material-cost driven** | COGS as % of revenue held flat (±0.3pt) across the period; discounting explains ~85% of the margin gap |
| 5 | **Q4 discounting spikes independent of any promotional calendar event** | No corresponding marketing campaign or clearance event on record for 3 of 3 years reviewed |

---

## 📈 Dashboard

[Full report overview]<img width="818" height="506" alt="IMG_5587" src="https://github.com/user-attachments/assets/4ede8ec1-d0fb-4937-8ac3-9a80390a0384" />

*Interactive Power BI file available in [`/dashboard`](./dashboard) — includes drill-through by region, rep, and SKU, plus a bookmark-driven "Executive View" for presentation mode.*

---

## ✅ Recommendations

| Recommendation | Owner | Priority | Est. Annual Impact |
|---|---|---|---|
| Introduce tiered discount approval workflow (>10% requires manager sign-off) | Sales Operations | 🔴 High | ~$410K margin recovery |
| Move Southeast region to contribution-margin-based rep incentives (not revenue-only) | Regional VP, Southeast | 🔴 High | ~$220K margin recovery |
| Re-tier the SKU catalog by contribution margin, not unit volume, for sales coaching | Product & Sales Leadership | 🟠 Medium | ~$110K margin recovery |
| Add a real-time discount-rate alert to the CRM at the point of quote creation | Sales Ops / IT | 🟠 Medium | Prevents recurrence |
| Institute a monthly (not quarterly) regional margin review cadence | Finance | 🟡 Low effort, high leverage | Faster detection of future drift |

---

## 💰 Projected Business Impact

```
Current annual margin leakage from excess discounting:   ~$740,000
Addressable via approval workflow + incentive redesign:  ~$630,000 (85%)
Payback period on process change (no new tooling cost):   < 1 quarter
```



## 🗺️ Next Steps

- [ ] Validate the $740K estimate with Finance using actuals from the current quarter
- [ ] Pilot the tiered approval workflow in the Southeast region for one quarter before company-wide rollout
- [ ] Build a lightweight rep-level scorecard (contribution margin, not just revenue) for the next sales incentive cycle
- [ ] Extend the analysis to include return/refund data, which was out of scope for this phase
- [ ] Automate the monthly margin-review dashboard refresh (currently manual SQL pull)

