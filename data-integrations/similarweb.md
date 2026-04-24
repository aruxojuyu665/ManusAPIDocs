# Similarweb

Manus integrates Similarweb data access directly into your workflow. Without additional configuration or API management, you can access comprehensive website analytics and digital market intelligence simply through natural language prompts.

## Overview

Manus integrates Similarweb data access directly into your workflow. Without additional configuration or API management, you can access comprehensive website analytics and digital market intelligence simply through natural language prompts.

## How to Use

Simply mention the data you need in your prompt. Manus will automatically use Similarweb to fetch the information when related info is detected.

**Traffic Analysis:**
```
Show me monthly visits, bounce rate, and pages per visit for example.com over the last 6 months. Include month-over-month changes.
```

**Marketing Channels:**
```
Break down the marketing channel mix for example.com. What percentage comes from direct, organic search, paid, social, referral, and display?
```

**Geographic Analysis:**
```
Show me the top 10 countries by traffic share for example.com in 2025 Q4. I need to understand their geographic footprint.
```

## Available Endpoints

### Endpoint Overview

| Type | Endpoint | Unit Cost (Credits) | Description |
|---|---|---|---|
| A | Get Unique Visit | 4 | Total number of unique visitors to a domain within a specific timeframe |
| A | Get Global Rank (Desktop+Mobile Web) | 4 | Website's ranking compared to all websites globally |
| A | Get Total Visits (Desktop+Mobile Web) | 4 | Total number of visits to the website |
| A | Get Bounce Rate (Desktop+Mobile Web) | 4 | Percentage of visitors who leave after viewing one page |
| B | Get Total Traffic by Country (Desktop+Mobile Web) | 28 | Geographic distribution of website traffic |
| B | Get Traffic Sources by Marketing Channel (Desktop) | 28 | Breakdown of desktop traffic channels |
| B | Get Traffic Sources by Marketing Channel (Mobile) | 28 | Breakdown of mobile traffic channels |

### Data Details

| Type | Endpoint | Regional Granularity | Accessible Information |
|---|---|---|---|
| A | Get Unique Visit | Worldwide | Share of desktop-only UV; share of mobile web-only UV; share of UV across both mobile web and desktop |
| A | Get Global Rank (Desktop+Mobile Web) | Worldwide | Monthly Global Rank |
| A | Get Total Visits (Desktop+Mobile Web) | Worldwide | Total visits to the website across desktop and web mobile |
| A | Get Bounce Rate (Desktop+Mobile Web) | Worldwide | Monthly Bounce Rate |
| B | Get Total Traffic by Country (Desktop+Mobile Web) | By Country | Country Name, Country Ranking by share, Share of traffic by country, Total visits by country, Pages per visit by country, Average time by country, Bounce rate by country |
| B | Get Traffic Sources by Marketing Channel (Desktop) | Worldwide | Estimated organic and paid desktop visits by channel (Organic Search, Paid Search, Direct, Display Ads, Email, Referrals and Social) |
| B | Get Traffic Sources by Marketing Channel (Mobile) | Worldwide | Estimated organic and paid mobile visits by channel (Organic Search, Paid Search, Direct, Display Ads, Email, Referrals and Social) |

## Price Model

This data integration follows Similarweb's multiplier-based pricing model, where costs are calculated by multiplying multiple factors.

### Pricing Factors

**Important Notes:**

- Data is available at **monthly granularity only**
- Maximum **12 months** of historical data available
- Available to **Pro plan users**
- Consumes **paid subscription or add-on credits only**
- **Available via Web interface only** (API-initiated sessions excluded)

Manus automatically optimizes queries to minimize costs while delivering accurate results. Session Credits Usage is tracked in your dashboard.

### Example Calculations

**Cost = Domains × Granularity × Countries × Time Span × Unit Cost**

| Endpoint | Prompt | Cost Calculation | Total |
|---|---|---|---|
| **Unique Visit** | Show me unique visitors change for `example.com` over the last year | 1 Domain × 1 Country × 12 Months × 4 Unit Cost | **48 Credits** |
| **Geography** | Get traffic breakdown by country for `example.com` in the past month, return only top 5 countries | 1 Domain × 5 Countries × 1 Month × 28 Unit Cost | **140 Credits** |
| **Market Channel** | Compare organic search traffic on mobile web for `example1.com` and `example2.com` in the past 3 months | 2 Domain × 1 Country × 3 Months × 28 Unit Cost | **168 Credits** |

> The above calculations reflect Data API costs only. Total session credits include additional charges for AI processing, computation, and other features used during the session.

Data accuracy is determined by Similarweb's statistical scope and algorithms. Estimates may vary by website. Always verify critical data with multiple sources.

## Reference

- [Similarweb Developer Documentation](https://developers.similarweb.com/)
- [Similarweb Data Credits System](https://support.similarweb.com/hc/en-us/articles/360000000000)
- [Data Accuracy and Methodology](https://support.similarweb.com/hc/en-us/articles/360000000001)
