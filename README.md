# LSGO Forward Curve & Spread Regime Analysis

**Forward curve monitoring of the European diesel market using ICE Low Sulphur Gasoil futures**

---

## Project Overview

This project analyzes the **ICE Low Sulphur Gasoil (LSGO)** forward curve over the period **January 2025 to February 2026** in order to study:

- forward curve structure,
- prompt tightness,
- spread behavior,
- volatility regimes,
- and the statistical properties of stress events.

**Period:** Jan 2025 – Feb 2026 (288 trading days)  
**Asset:** ICE Low Sulphur Gasoil Futures  
**Focus:** rolling contracts, spread monitoring, anomaly detection, regime analysis

The objective is not to build a predictive trading model, but to develop a **research-grade monitoring framework** showing how forward-curve information can be used to identify periods of structural stress in a refined products market.

---

## Project Logic & Motivation

### Why This Project?

In commodity markets, flat price alone rarely gives a complete picture of supply-demand conditions. Traders and risk managers often monitor the **shape of the forward curve** to understand whether the market is balanced, tightening, or under stress.

This project was built to address four practical questions:

1. **How should raw futures contracts be rolled properly?**  
   Rolling logic is critical in commodity analytics. Poor expiry handling can distort returns, spreads, and risk signals.

2. **How can curve structure be transformed into systematic indicators?**  
   The notebook builds rolling spreads, volatility measures, Z-scores, and a simple regime framework.

3. **What does the 2025–2026 sample suggest about diesel market structure?**  
   The analysis examines whether the curve remained stable or entered repeated stress regimes.

4. **How can these results be communicated in a way that is useful for monitoring?**  
   The notebook emphasizes concise charts, validation steps, and interpretable thresholds rather than complex modeling for its own sake.

---

## What Was Built

### 1. Data Engineering

The starting point is a matrix of daily ICE settlement prices across contract months. From this raw structure, I built rolling contracts:

- **M1**: front month
- **M2**: second nearby
- **M3**: third nearby
- **M6**: sixth nearby

Particular attention was given to:

- contract ordering,
- expiry handling,
- duplicated final settlement observations,
- missing values,
- and roll-date consistency.

This is the technical core of the project: without a coherent rolling methodology, all downstream analysis becomes unreliable.

### 2. Spread Construction

Using the rolling contracts, I calculated:

- **M1–M2**
- **M1–M3**
- **M1–M6**

These spreads are used to monitor:

- prompt tightness,
- near-term imbalance,
- and broader storage / structural conditions.

I also computed:

- daily log returns on M1,
- 20-day rolling annualized volatility.

### 3. Statistical Monitoring Framework

To measure how unusual current spread levels are relative to recent history, I implemented:

- **60-day rolling Z-scores** for M1–M3 and M1–M6,
- distribution diagnostics (skewness, kurtosis, histogram analysis),
- spread-volatility relationship analysis.

This allows the notebook to distinguish between ordinary backwardation and statistically unusual tightening episodes.

### 4. Regime Framework

A simple regime classification was added using M1–M6 thresholds:

- **Normal**
- **Tight**
- **Stress**
- **Crisis**

This classification is not presented as a universal truth, but as a practical monitoring framework for interpreting changes in curve structure.

### 5. Validation & Visualization

The notebook includes explicit validation steps:

- roll-date checks,
- jump diagnostics,
- spread consistency review,
- missing-value inspection.

It then summarizes the results through a structured set of charts and concise interpretation.

---

## Main Findings

The sample suggests that the European diesel market remained in backwardation almost continuously over the period, with several episodes of materially stronger prompt tightness.

The most notable episode occurred in **June 2025**, when both short-end and long-end curve spreads moved to extreme levels relative to their recent history.

The results show three main patterns:

1. **Persistent backwardation**  
   The market remained backwardated almost throughout the full sample, consistent with structurally firm prompt conditions.

2. **Non-normal spread behavior**  
   Spread distributions are right-skewed and fat-tailed. Extreme dislocations occur more frequently than a normal distribution would suggest.

3. **Strong association between curve stress and volatility**  
   Periods of spread expansion tend to coincide with, or slightly precede, higher realized volatility. This is consistent with the view that structural tightness contributes to price instability.

This should be interpreted as a **descriptive and monitoring result**, not as formal proof of causality.

---

## Key Findings

### 1. Persistent Tightness
- Market in backwardation on **287 out of 288 trading days**
- Average **M1–M3 spread: 18.4 USD/MT**
- Average **M1–M6 spread: 33.7 USD/MT**
- Consistent with a structurally firm prompt market over the sample

### 2. Extreme June 2025 Episode
- **June 19, 2025**: short-term structure reached a local extreme
- **M1–M3 peaked at 85.25 USD/MT**
- **M1–M6 peaked at 118.5 USD/MT**
- **20D annualized volatility reached 78%**

Under standard normal assumptions, such a move would appear exceptionally rare; the fact that it occurs within a short sample reinforces the importance of fat-tailed behavior in commodity spreads.

### 3. Fat-Tailed Distribution
- **Skewness: 2.12**
- **Kurtosis: 5.72**
- **4.9% of observations** recorded Z-scores above 3, versus roughly **0.3%** under a normal benchmark

This suggests that extreme spread dislocations are a structural feature of the sample rather than pure statistical accidents.

### 4. Structure and Volatility
- Correlation **M1–M3 vs Volatility: 0.476**
- Correlation **M1–M6 vs Volatility: 0.525**

These results suggest a meaningful association between spread widening and higher volatility, consistent with the idea that physical tightness and price instability often emerge together.

---

## Technical Highlights

### Data Engineering
- Rolling contract construction with explicit expiry handling
- Duplicate settlement treatment around roll dates
- Validation of jumps, missing values, and spread consistency

### Statistical Analysis
- 60-day rolling Z-score framework
- Distribution analysis using skewness and kurtosis
- Correlation review between curve structure and volatility

### Regime Classification
- **Normal:** M1–M6 < 20 USD/MT
- **Tight:** M1–M6 between 20 and 50 USD/MT
- **Stress:** M1–M6 between 50 and 100 USD/MT
- **Crisis:** M1–M6 > 100 USD/MT

These thresholds are intended as practical monitoring references for this sample, not universal market constants.

### Visualization
- 11 structured charts with concise interpretation
- Summary table of key metrics
- Multi-panel dashboard for market monitoring
- Regime timeline for fast visual interpretation

---

## Key Charts

| Chart | Description | Main Insight |
|-------|-------------|--------------|
| **Chart 1** | M1 Price & Volatility | Volatility rises during structural tightening |
| **Chart 2** | Forward Curve Snapshots | Curve shape shifts from moderate to extreme backwardation |
| **Chart 3** | Short-Term Structure (M1-M2, M1-M3) | Prompt tightness intensified materially in June 2025 |
| **Chart 4** | Long Structure (M1-M6) | Deep backwardation made storage economics unattractive |
| **Chart 5** | Z-Score M1-M3 | June 2025 stands out as an extreme short-end event |
| **Chart 6** | Z-Score M1-M6 | Broader curve dislocation accompanied the short-end move |
| **Chart 7** | Distribution (Histogram) | Spread behavior is clearly non-normal |
| **Chart 8** | Spread vs Volatility | Higher spreads are associated with higher volatility |
| **Chart 9** | Event Timeline | Structural moves can be interpreted alongside market events |
| **Chart 10** | Market Dashboard | Summary monitoring view across price, spread, Z-score, and volatility |
| **Chart 11** | Regime Classification | The sample spent only a limited fraction of time in the most extreme regime |

---

## What This Project Signals

This project is designed to demonstrate:

- **forward curve literacy**
- understanding of **physical commodity imbalance**
- ability to build **clean rolling futures analytics**
- ability to turn market structure into **interpretable monitoring signals**
- ability to present commodity analysis in a professional format

---

## Limitations

- 13-month sample only
- no direct fundamental inputs (inventories, refinery runs, freight)
- no out-of-sample validation
- regime thresholds are practical, not universal

This should be viewed as a **structured exploratory framework**, not a production trading system.

---

## Next Extensions

- extend to multi-year history
- add fundamental and flow data
- compare with other diesel benchmarks
- test alternative regime thresholds
- develop a systematic monitoring dashboard
