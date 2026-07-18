# Decarbonizing Travel — Process Mining & ML Case Study

An end-to-end emissions analytics platform for corporate travel: process mining on real trip event logs, a leakage-safe ML model that flags high-carbon trips before they're booked, and a live 3-tab BI dashboard for self-serve exploration.

**Tech stack:** Celonis (Process Mining · PQL · Dashboarding) · Python · XGBoost · Pandas / NumPy

---

## What this project does

1. **Mines the actual process** — reconstructs how business-travel bookings, approvals, and reimbursements really unfold, using Celonis process mining on trip event logs (not just the policy on paper).
2. **Predicts risk pre-booking** — a gradient-boosted classifier (**ROC-AUC 0.999**) flags a trip as high-carbon using only information available at the moment of request, with target-leaking columns strictly excluded.
3. **Ships as a live tool** — a 3-tab interactive dashboard (Emissions Overview → Benchmarking → Emissions Drilldown), not a static report.

## Key findings

- **Travel mode — not business unit or trip purpose — drives emissions.** Business/First Class flights emit 2–2.6x more than Economy, 10x+ more than rail.
- **Regional efficiency varies ~5x.** Europe averages 602 kg CO₂e/trip vs. 2,956 kg in Asia, largely due to distance and rail availability.
- **Process friction correlates with emissions.** Out-of-policy bookings emit 43.5% more CO₂e; last-minute bookings emit 52.7% more.

## Recommendations (quantified)

| Lever | Est. annual impact |
|---|---|
| Cap premium cabins on routes <6 hrs | −34,738 t CO₂e/yr |
| Mandate rail on proven short-haul routes | −770 t CO₂e/yr |
| 5-day minimum booking window | −16,448 t CO₂e/yr |
| Real-time carbon score at booking | Enables all three levers |

Combined: **~52,000 t CO₂e/yr abated (≈29% of the current footprint)** if fully adopted.

## Repo contents

```
├── decarbonizing_travel_analysis.ipynb   # Full analysis + model training notebook
├── submission.csv                         # Model predictions (TripID, HighCarbon probability)
├── presentation/
│   └── Decarbonizing_Travel_Case_Study.pptx   # Project walkthrough deck
└── README.md
```

## Model notes

- Target: `HighCarbon` (binary), predicted as a probability in `submission.csv`.
- Feature set deliberately excludes any column that directly encodes or derives from the target (e.g. CO₂e and spend columns) to avoid data leakage.
- Evaluated on a held-out private split; only the public trip dataset was used for the dashboard and business analysis.

## Dashboard

Built natively in Celonis Studio with PQL-driven KPIs and charts across three tabs:
- **Emissions Overview** — footprint totals, trip volume, process flow (Variant Explorer)
- **Benchmarking** — region- and business-unit-level average CO₂e
- **Emissions Drilldown** — travel-mode-level emissions breakdown

Screenshots are included in the presentation deck.

---

*This is a personal data-analytics case study project. Not affiliated with or endorsed by Celonis.*
