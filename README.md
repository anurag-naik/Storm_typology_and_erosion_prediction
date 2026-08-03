# Storm Typology & Coastal Erosion Prediction

Research project investigating how storm wave characteristics along the Canterbury coast, New Zealand, relate to observed shoreline erosion — combining wave buoy observations, a regional wave hindcast model, and satellite-derived shoreline data.

Conducted as part of the Master of Applied Data Science programme at the **University of Canterbury** (DATA601), supervised by **Prof. Phil Davies** (Senior Professor, Data Science) in collaboration with PhD researcher **Sarah McSweeney**.

**Team:** Anurag Naik, Omokova Mary Attah, Rohith Blesso Dharmaraj

---

## Overview

Storm wave conditions are a major driver of short-term coastal erosion, but linking offshore storm forcing to shoreline change is difficult due to sparse observations and uncertainty in wave models. This project builds a repeatable pipeline that:

1. Detects and classifies storm events into physically meaningful **storm typologies**
2. Validates a regional wave **hindcast model** against real buoy observations
3. Tests whether storm characteristics can **predict monthly coastal erosion**

## Research Questions

- Can storm events be objectively identified and classified using wave characteristics?
- How accurately does the regional wave hindcast reproduce observed storm conditions?
- Do different storm types correspond to systematic differences in shoreline change?

## Data Sources

| Source | Description | Coverage |
|---|---|---|
| **ECan Wave Buoy** | In-situ hourly wave measurements (Hs, peak period, direction) off Banks Peninsula | Feb 1999 – Sept 2025 |
| **NZ Wave Hindcast** | Regional numerical wave model output | Jan 1993 – Dec 2019 |
| **CoastSat** | Satellite-derived monthly shoreline positions along Canterbury transects | Multi-year |

## Methodology

1. **Storm detection** — Peak-Over-Threshold (POT) method applied to significant wave height, with a minimum 24-hour storm duration and recurrence interval.
2. **Storm typology** — K-Means clustering (k selected via the elbow method) on storm wave height, duration, and direction, producing 3 distinct storm regimes.
3. **Hindcast validation** — Matched hindcast storms to buoy storms by time overlap; computed bias, RMSE, and correlation to quantify model accuracy.
4. **Shoreline response analysis** — Monthly shoreline change (CoastSat) grouped by storm type to assess differential coastal impact.
5. **Erosion prediction** — Logistic regression modelling the probability of a net-erosive month from storm duration, wave height, and direction (circular-encoded via sine/cosine).

## Key Results

- Storms cluster into **3 physically interpretable types**: Lower-Energy Short-Period, Moderate-Energy Mixed, and High-Energy Swell storms.
- The hindcast reproduces storm **direction** reasonably well but **overestimates wave height** (bias ≈ +2.0 m) and **underestimates storm duration** (bias ≈ −13.2 hrs) relative to buoy observations.
- Shoreline response varies systematically by storm type — high-energy, long-duration storms are associated with the most severe erosion events.
- A logistic regression model using storm characteristics achieved **AUC = 0.56** in predicting erosive months — storm duration and mean wave height were the strongest predictors, but overall predictive skill was limited (R² ≈ 0.06), indicating shoreline change is strongly influenced by factors beyond offshore storm forcing (e.g. antecedent beach state, sediment supply, storm sequencing).

## Tech Stack

- **Python** — Pandas, NumPy, Scikit-learn
- **Visualisation** — Matplotlib, Seaborn
- **Methods** — K-Means clustering, logistic regression, ROC/AUC evaluation

## Repository Structure

├── CSV FILES/ # Raw and processed datasets (buoy, hindcast, shoreline)
├── Jupyter Notebooks/ # Analysis notebooks (storm detection, clustering, validation, modelling)
├── Figures/ # Generated plots and visualisations
├── Report Final 2.pdf # Full written research report
├── EROSION POSTER.pdf # Project poster
└── README.md

## Full Report

The complete write-up — including detailed methodology, all figures, validation tables, and appendices — is available in [`Report Final 2.pdf`](./Report%20Final%202.pdf). A summary poster is also available in [`EROSION POSTER.pdf`](./EROSION%20POSTER.pdf).

## Acknowledgements

Wave buoy data provided by Environment Canterbury (ECan). Hindcast wave model data from regional NZ wave simulations. Shoreline data derived using the [CoastSat](https://github.com/kvos/CoastSat) framework.

## License

This project is for academic and portfolio purposes. Feel free to reference the methodology with attribution.
