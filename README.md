# Summer Analytics 2026 — Capstone: Decarbonizing Travel

**Program:** Summer Analytics 2026, Consulting & Analytics Club, IIT Guwahati (in partnership with Celonis)
**Author:** Gautam Bhardwaj

This repository contains my work for the Summer Analytics 2026 Capstone Project — a two-part sustainability challenge analyzing ~65,000 corporate business travel records to help a company (fictional scenario, sponsored by Celonis) work toward a Net Zero 2030 emissions goal.

## Project Structure

```
├── data/
│   ├── public/           # Labeled training data (trip details, event logs, attributes)
│   ├── private/          # Unlabeled test data (features only, used for scoring)
│   └── sample_submission.csv
├── notebook/
│   └── GreenTravel_HighCarbon_Prediction.ipynb   # Full ML pipeline, executed with outputs
├── results/
│   └── submission.csv    # Final predictions on the private test set
├── presentation/
│   └── Gautam_Bhardwaj_SummerAnalytics_Sustainability.pptx   # Executive slide deck
└── docs/                 # Original project brief, outline, and data dictionary
```

## Part 1 — Process Mining & Executive Presentation

Analyzed the trip dataset to answer five key business questions: emissions profile, regional benchmarking, hotspot identification, inefficiency/pain-point analysis, and quantified policy recommendations. Delivered as a data-driven executive slide deck (`presentation/`).

**Key findings:**
- 178,090 tonnes CO2e emitted across 65,289 trips ($140.5M total spend)
- Premium cabin flights (Business + First Class) are 45% of trips but drive 44.8% of emissions — the single biggest lever
- Asia-Pacific-origin travel is 32.5% of trips but 50.2% of total emissions
- Out-of-policy trips run 44% higher CO2e per trip than in-policy trips
- Quantified recommendations: cabin-class capping (~38.8M kg CO2e/yr saved), EV fleet conversion (~6.6M kg CO2e/yr saved), and automated policy-breach flagging

## Part 2 — GreenTravel Intelligence Challenge (ML)

Binary classification task: predict whether a trip will be `HighCarbon` (1) or not (0) using only pre-booking information, explicitly excluding all CO2e-derived columns to avoid label leakage.

**Approach:**
- Feature engineering from trip data, process event logs (duration, event sequence flags), and event attribute tables (cancellations, delays, reimbursements)
- LightGBM binary classifier, 5-fold stratified cross-validation
- **Result: ~0.999 ROC-AUC (OOF)** — driven primarily by legitimate, allowed features (cabin class, costs, hotel nights), not leakage

Full methodology, EDA, and results are documented in the executed notebook.

## Note on Celonis Process Mining Component

The project brief also called for building a live process-mining dashboard in the Celonis Platform (Process & Variant Explorer, 3 dashboard tabs). Celonis Academic Alliance self-serve signup was unavailable at the time of submission ([Celonis Community reports of Free Plan access changes](https://community.celonis.com)), so this component could not be completed. The process-mining angle is instead reflected through event-log-derived features in the ML notebook (process duration, event sequence patterns) and the Inefficiencies slide in the presentation.
