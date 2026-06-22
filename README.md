# SaaS Unit Economics Simulator

An interactive tool for exploring how CAC, churn, ARPU, gross margin, and net dollar retention interact to shape customer lifetime value, payback period, and long-run revenue — built as a self-directed project for a strategic finance portfolio.

**[View the live simulator →](https://philbertcychan.github.io/unit-econ-simulator/)**

## What it does

### Single-cohort analysis
Set your assumptions and instantly see:
- **LTV** (lifetime gross profit per customer)
- **LTV:CAC ratio** — color-coded against the 3:1 rule of thumb
- **Payback period** — derived from the cohort curve, not a simplified formula
- **Average customer lifespan** — 1 / monthly churn rate
- **24-month cohort curve** — starts negative by CAC, crosses zero at the payback point (annotated), then accumulates

### Churn sensitivity table
Shows LTV, LTV:CAC, and payback period across five churn scenarios (current plus and minus 2 percentage points), making it easy to see how fragile or robust the unit economics are to small retention changes.

### Churn-improvement scenario toggle
Overlays a second cohort curve assuming 1 percentage point lower monthly churn — a quick gut check on what a retention investment might be worth funding.

### Multi-cohort compounding
Add a monthly acquisition volume and see how total gross profit builds as overlapping cohorts layer on top of each other over 24 months. Shows both cumulative gross profit and the monthly run-rate, and flags whether the business is approaching a churn-limited steady state or still compounding at month 23.

### Net Dollar Retention (NDR)
Models expansion revenue: customers who stick around spend more over time (upsells, seat expansion, usage growth). NDR compounds monthly on surviving customers, partially offsetting churn loss. At NDR above 100%, expansion revenue lifts LTV above what the pure churn estimate would imply — the primary driver behind why best-in-class SaaS businesses can sustain high valuations even with meaningful gross churn.

## Presets

Three one-click starting points calibrated to realistic benchmarks:
- **Early-stage SaaS** — higher CAC, higher churn, lower ARPU
- **Mature SaaS** — lower churn, higher ARPU, stronger margins
- **Marketplace** — lower CAC, higher churn, compressed margins

## Key formulas

- **LTV** = (ARPU x gross margin %) / monthly churn rate, adjusted for NDR expansion
- **Payback period** = month at which cumulative cohort gross profit crosses zero (derived from cohort curve, not a simplified formula)
- **NDR monthly rate** = NDR^(1/12), compounds on surviving customers only
- **Multi-cohort monthly gross profit** = sum across all active cohorts of (acq x (1 - churn)^age x NDR_monthly^age x monthly gross profit per customer)

## Assumptions and limitations

This is an illustrative model, not a forecast:
- Churn rate, ARPU, and gross margin are held constant across all cohorts and months — real businesses show churn that decays over time (oldest customers churn less), which means this model somewhat understates LTV
- NDR is applied as a smooth monthly compounding rate; in practice, expansion revenue is lumpy and tied to specific upgrade or renewal events
- CAC is assumed constant — in reality, CAC tends to rise as a company exhausts its most efficient acquisition channels

## Stack

Single-file HTML, vanilla JS, Chart.js for visualization. No build step, no backend — fully static, deployed via GitHub Pages.

## Possible next steps

- Churn decay curve — model older cohorts churning less than newer ones
- Revenue bridge chart — decompose monthly revenue change into new, expansion, contraction, and churn components
- Named scenario save and compare — let users save and label multiple assumption sets side by side
