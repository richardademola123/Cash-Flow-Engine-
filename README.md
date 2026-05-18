# Metric Flow Engine V1
### 12-Week Cashflow Visibility System for Construction SMEs

---

## The Problem

Most construction businesses don't know their cash position until it's already a problem.

Invoices go out. Suppliers need paying. Retentions sit unpaid. And the business owner is running on gut feel, not numbers — until a bad week arrives and they're scrambling.

**Metric Flow Engine** solves this by giving construction SMEs a clear, live view of their cash for the next 12 weeks — who owes them, what's coming due, and exactly which weeks are under pressure.

---

## What the Engine Does

| Feature | Detail |
|---|---|
| **AR Tracker** | Full accounts receivable view — every open invoice, days outstanding, debtor risk flag |
| **AP Schedule** | Supplier payment schedule by week — who's due, how much, which weeks are heavy |
| **12-Week Cashflow Forecast** | Week-by-week net position: inflow vs outflow vs cumulative cash |
| **Executive Dashboard** | Single-page summary for the business owner — no finance knowledge required |

---

## Tech Stack

| Layer | Tool | Purpose |
|---|---|---|
| Data Storage | Google BigQuery | Stores raw AR and AP data |
| Data Cleaning | SQL (BigQuery) | Cleans, transforms and models the data |
| Front End | Microsoft Excel | Cashflow engine and dashboard |
| Data Pipeline | CSV Export | BigQuery → Excel weekly refresh |

---

## Repository Structure

```
metric-flow-engine/
│
├── sql/
│   ├── 01_ar_model.sql           # Accounts receivable view
│   ├── 02_ap_model.sql           # Accounts payable view
│   ├── 03_cashflow_forecast.sql  # Weekly net cashflow query
│   └── 04_debtor_risk.sql        # AR risk classification
│
├── excel-engine/
│   └── metric_flow_engine_v1_template.xlsx  # Excel engine template
│
├── docs/
│   ├── SETUP.md                  # How to set up BigQuery and load data
│   ├── DATA_DICTIONARY.md        # Column definitions for all tables
│   └── WEEKLY_WORKFLOW.md        # Step-by-step weekly refresh process
│
└── assets/
    └── (dashboard screenshots)
```

---

## SQL Models

### AR Model — `sql/01_ar_model.sql`
Transforms raw invoice data into a clean accounts receivable view with:
- Days outstanding calculation
- Overdue flag (30 / 60 / 90+ day buckets)
- Week-by-week expected inflow

### AP Model — `sql/02_ap_model.sql`
Transforms raw supplier payment data into a structured AP schedule with:
- Payment size classification (Small / Medium / Large)
- Week-by-week outflow aggregation
- Supplier grouping

### Cashflow Forecast — `sql/03_cashflow_forecast.sql`
Joins AR and AP models to produce a 12-week net cashflow view:
- Weekly inflow (AR expected)
- Weekly outflow (AP due)
- Net position per week
- Cumulative cash position

---

## Excel Engine — Tab Structure

| Tab | Purpose |
|---|---|
| `AR_Tracker` | Paste AR export here — auto-calculates days outstanding and risk |
| `AP_Schedule` | Paste AP export here — builds weekly outflow schedule |
| `Cashflow_Forecast` | Live 12-week forecast pulling from AR and AP tabs |
| `Dashboard` | Executive summary — one page, plain English |

---



