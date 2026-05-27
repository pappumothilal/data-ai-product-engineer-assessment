# data-ai-product-engineer-assessment
task-1-product-scoping/README.md

# TASK 1 — PRODUCT SCOPING

# Product Brief

## Product Name
PulseView — Marketing Performance Intelligence Dashboard

---

# Problem Statement

Marketing teams and client-facing analysts frequently need to answer one recurring question:

> “How is our marketing performing across channels right now, and where should we focus?”

Currently, answering this question requires:

- Logging into multiple platforms manually
- Exporting spreadsheets from various tools
- Combining data manually
- Creating inconsistent summaries depending on who prepares the report
- Delayed responses when key analysts are unavailable

This creates inefficiency, inconsistency, and dependency on individuals rather than systems.

The goal of this product is to reduce manual effort, standardize reporting, and provide fast actionable insights without changing the existing tools or workflows used by the team.

---

# Primary Users

## Primary User
Marketing Analysts

Why:
- Analysts currently spend the most time collecting and interpreting data.
- They need faster access to cross-channel performance.
- They require flexibility and trust in the data.

## Secondary Users
- Client Success Managers
- Brand Clients

These users primarily consume insights rather than manipulate raw data.

---

# Product Vision

Build a lightweight internal analytics platform that aggregates marketing performance data from existing tools into a unified dashboard and generates simple AI-powered insights.

The product should:

- Reduce manual reporting time
- Provide consistent performance summaries
- Surface opportunities and issues faster
- Improve trust in reporting
- Work alongside existing workflows

---

# Key User Pain Points

| Pain Point | Current Situation |
|---|---|
| Fragmented data | Data lives across multiple platforms |
| Manual reporting | Analysts manually create reports |
| Inconsistent insights | Different analysts interpret data differently |
| Delayed answers | Reports depend on analyst availability |
| Low scalability | Manual processes do not scale with more clients |

---

# Goals for Version 1

The first version should focus only on solving the core reporting problem.

## V1 Objectives

- Centralize campaign metrics
- Provide channel-level comparison
- Generate simplified insights automatically
- Improve reporting consistency
- Save analyst time

---

# Features Included in V1

## 1. Unified Dashboard

Displays marketing metrics across channels.

### Supported Channels
- Google Ads
- Meta Ads
- LinkedIn Ads
- Email Campaigns

### Metrics
- Spend
- Impressions
- Clicks
- CTR
- CPC
- Conversions
- Conversion Rate
- ROAS

---

## 2. Cross-Channel Comparison

Allows analysts to compare:

- Top-performing channels
- Cost efficiency
- Conversion efficiency
- Spend allocation

---

## 3. AI-Generated Summary

The system automatically generates concise summaries.

### Example

> “Meta Ads performance declined by 18% week-over-week while Google Search campaigns improved conversion rate by 11%.”

This reduces manual interpretation work.

---

## 4. Alerts & Anomaly Detection

Basic alerting for:

- Sudden spend spikes
- Conversion drops
- CTR decline
- ROAS anomalies

---

## 5. Export Functionality

Users can:

- Export reports as CSV
- Download summary PDFs

---

# Features Explicitly Excluded from V1

The following are intentionally excluded to keep the first release focused and maintainable.

| Feature | Reason Excluded |
|---|---|
| Real-time streaming dashboards | High infrastructure complexity |
| Campaign editing/management | Not core to reporting problem |
| Predictive forecasting | Requires historical maturity and trust |
| Advanced attribution modeling | Complex implementation |
| Budget automation | High operational risk |
| Conversational AI chatbot | Adds complexity without core value |
| Custom ML models | Premature optimization |

---

# Why These Features Were Excluded

The biggest risk for an internal analytics product is over-engineering before solving the basic reporting workflow.

The focus of V1 is:

- reliability,
- clarity,
- adoption,
- and speed.

A focused solution is more likely to gain trust and adoption internally.

---

# User Flow

```text
User logs in
      ↓
Selects client/account
      ↓
Dashboard loads aggregated metrics
      ↓
AI summary highlights performance trends
      ↓
User investigates anomalies
      ↓
Exports report or shares findings
```

---

# Data Sources

The product integrates with existing tools.

## Example Sources

| Platform | Data Type |
|---|---|
| Google Ads | Campaign metrics |
| Meta Ads | Paid social metrics |
| LinkedIn Ads | B2B campaign metrics |
| HubSpot | Lead and email data |
| Google Analytics | Website analytics |

---

# Data Pipeline Overview

```text
Marketing Platforms
(Google Ads / Meta / HubSpot)
            ↓
      API Connectors
            ↓
      ETL Processing
            ↓
      BigQuery Warehouse
            ↓
  Backend Analytics Service
            ↓
 Dashboard + AI Insight Layer
```

---

# Technical Architecture

## Frontend
- React
- Tailwind CSS

## Backend
- Python
- FastAPI

## Data Storage
- BigQuery

## AI Layer
- OpenAI API or Gemini API

## Hosting
- Google Cloud Platform

---

# Trust & Reliability Considerations

Trust is critical for analytics products.

To improve trust:

- Every metric displays source attribution
- Last synced timestamp is visible
- Failed syncs are logged
- Manual overrides are avoided
- Metrics definitions remain standardized

---

# Success Metrics

The success of V1 would be measured by:

| Metric | Goal |
|---|---|
| Reporting time reduction | 50% reduction |
| Dashboard adoption | Weekly analyst usage |
| Insight consistency | Reduced manual interpretation |
| Export usage | High reporting export frequency |

---

# Risks & Mitigations

| Risk | Mitigation |
|---|---|
| API instability | Retry logic and scheduled syncs |
| Data inconsistency | Validation layer |
| Low user trust | Transparent data sources |
| Feature creep | Strict V1 scope |

---

# Future Enhancements

Potential future features:

- Predictive forecasting
- Budget recommendations
- Natural language querying
- Real-time dashboards
- Attribution modeling
- AI optimization suggestions
- Slack/MS Teams integration

These features are intentionally postponed until the core reporting workflow proves valuable.

---

# Product Scoping Conclusion

The proposed solution focuses on solving a real operational bottleneck with a lightweight, practical product.

Rather than building an overly ambitious analytics platform, the goal is to create:

- fast insights,
- consistent reporting,
- lower manual effort,
- and scalable analyst workflows.

The product is intentionally scoped to maximize usability, reliability, and adoption.
