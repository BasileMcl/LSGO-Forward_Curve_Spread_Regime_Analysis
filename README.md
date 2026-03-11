# LSGO Forward Curve & Spread Regime Analysis

**Systematic commodity market monitoring using forward curve structure analysis**

---

## Project Overview

Analysis of the **ICE Low Sulphur Gasoil (LSGO)** forward curve from January 2025 to February 2026, revealing persistent supply tightness and extreme stress episodes in the European diesel market.

**Period:** Jan 2025 - Feb 2026 (13 months, 288 trading days)  
**Asset:** ICE Low Sulphur Gasoil Futures  
**Focus:** Forward curve structure, spread analysis, regime detection

---

## Project Logic & Motivation

### Why This Project?

Commodity traders rely on forward curve analysis to detect structural market stress before it appears in volatility. I wanted to build a **complete, production-ready framework** that:

1. **Handles real data complexity**: Proper contract rolling with expiry detection (the hard part)
2. **Detects anomalies systematically**: Z-scores, distribution analysis, regime classification
3. **Provides actionable signals**: Not just charts, but trading rules and risk thresholds
4. **Demonstrates professional rigor**: Data validation, honest limitations, transparent methodology

### What I Built

**Step 1: Data Engineering**  
Started with raw ICE settlement data (16 contract months, 288 trading days). Built rolling front-month contracts (M1-M6) with proper expiry handling. This is the technical foundation - if you get rolls wrong, everything downstream is garbage.

**Step 2: Spread Analysis**  
Calculated M1-M2, M1-M3, M1-M6 spreads to capture prompt tightness and storage economics. Added 20-day rolling volatility to measure price instability.

**Step 3: Statistical Framework**  
Implemented 60-day rolling Z-scores to quantify how abnormal current spreads are vs recent history. Analyzed distribution (skewness, kurtosis) to detect fat tails.

**Step 4: Regime Classification**  
Defined 4 regimes (Normal/Tight/Stress/Crisis) based on M1-M6 thresholds. 

**Step 5: Validation & Analysis**  
Validated data quality (no artificial jumps at rolls, spreads consistent). Created 11 charts with concise analyses.



### What I Found

The analysis revealed a **5-sigma event in June 2025** (Z-score = 5.25) that should statistically occur once every 5,000 years. But it happened in a 13-month sample. This confirms **fat-tailed distribution** - extreme events occur 16x more frequently than normal distribution predicts.

The forward curve provided **9 days advance warning** before the crisis peak. Spreads widened before volatility spiked, confirming that **structure drives volatility** (correlation 0.48-0.53).

### Conclusion

This is a **complete analysis of 2025 European diesel market**, demonstrating:
- How to build production-ready commodity analytics (proper data handling, validation)
- How to detect structural stress using forward curves (Z-scores, regime classification)
- How to quantify tail risk in non-normal markets (fat tails, distribution analysis)
- How to build actionable trading frameworks from market data (signals, thresholds, example trade)
- How to present complex analysis clearly (concise bullets, summary tables, visual timelines)

The methodology is applicable to any commodity market (crude oil, natural gas, metals). The code is clean, the analysis is rigorous, the presentation is digestible, and the findings are honest about limitations.

---

## Key Findings

### 1. Chronic Supply Tightness
- Market in **backwardation 99.7% of the time** (287/288 days)
- Average M1-M3 spread: **18.4 USD/MT**
- Average M1-M6 spread: **33.7 USD/MT**
- Indicates persistent inventory shortage

### 2. Extreme Stress Event (June 2025)
- **June 19, 2025**: 5-sigma event (Z-score = 5.25)
- M1-M3 reached **85.25 USD/MT** (4.6x average)
- M1-M6 peaked at **118.5 USD/MT** (3.5x average)
- Volatility spiked to **78% annualized**

### 3. Fat-Tailed Distribution
- **Skewness: 2.12** (strong right tail)
- **Kurtosis: 5.72** (fat tails)
- Extreme events occur **16x more frequently** than normal distribution predicts
- 4.9% of days had Z-scores > 3 (vs 0.3% expected)

### 4. Structure Drives Volatility
- Correlation M1-M3 vs Volatility: **0.476**
- Correlation M1-M6 vs Volatility: **0.525**
- Physical tightness causes price instability (not vice versa)

---

## Technical Highlights

### Data Engineering
- **Rolling contract construction** with proper expiry handling
- **Duplicate detection** for contract rolls
- **Data validation** (jumps, spreads, missing values)

### Statistical Analysis
- **Z-score normalization** (60-day rolling window)
- **Distribution analysis** (skewness, kurtosis)
- **Correlation analysis** (structure vs volatility)

### Regime Classification
- **Normal**: M1-M6 < 20 USD/MT
- **Tight**: M1-M6 20-50 USD/MT
- **Stress**: M1-M6 50-100 USD/MT
- **Crisis**: M1-M6 > 100 USD/MT

### Visualizations
- **11 professional charts** with concise analyses (5 bullets max per chart)
- **Summary table** with all key metrics
- **4-panel market dashboard** (price, spread, Z-score, volatility)
- **Regime classification timeline** (color-coded by regime)
- **"At a Glance" section** with visual timeline and key numbers

---

## Key Charts

| Chart | Description | Key Insight |
|-------|-------------|-------------|
| **Chart 1** | M1 Price & Volatility | Volatility peaked at 78% during June crisis |
| **Chart 2** | Forward Curve Snapshots | Curve shape evolved from mild to extreme backwardation |
| **Chart 3** | Short-Term Structure (M1-M2, M1-M3) | M1-M3 reached 85.25 USD/MT in June |
| **Chart 4** | Long Structure (M1-M6) | M1-M6 peaked at 118.5 USD/MT (storage uneconomic) |
| **Chart 5** | Z-Score M1-M3 | 5.25 Z-score = 5-sigma event |
| **Chart 6** | Z-Score M1-M6 | Entire curve dislocated simultaneously |
| **Chart 7** | Distribution (Histogram) | Fat tails confirmed (kurtosis 5.72) |
| **Chart 8** | Spread vs Volatility | Positive correlation (0.476-0.525) |
| **Chart 9** | Event Timeline | June crisis preceded by April weakness |
| **Chart 10** | Market Dashboard | 4-panel overview (price, spread, Z-score, vol) |
| **Chart 11** | Regime Classification | Market spent 2.1% of time in Crisis regime |

---

## How to Use

### Prerequisites
```bash
pip install pandas numpy scipy matplotlib jupyter
```

### Run the Analysis
```bash
cd LsGO_Analysis
jupyter notebook LSGO_Analysis_Report.ipynb
```

### Notebook Structure

**Executive Summary** (30 seconds)  
Key findings at a glance: 99.7% backwardation, 5-sigma event, fat tails, structure-volatility link.

**1. Introduction & Context** (5 min)  
What is a forward curve? Why analyze spreads? LSGO market characteristics. Backwardation vs contango.

**2. Data Preparation** (10 min)  
2.1-2.12: Import libraries → Load data → Clean → Build rolling contracts → Calculate spreads/volatility/Z-scores

**3. Data Validation** (5 min)  
3.1-3.5: Check for artificial jumps → Validate spreads → Missing values → Validation summary

**4. Market Analysis & Visualization** (30 min)  
- **Chart 1**: M1 Price & Volatility (38% swing, 78% vol peak)
- **Chart 2**: Forward Curve Snapshots (regime evolution)
- **Chart 3**: Short-Term Structure (M1-M3 reached 85.25 USD/MT)
- **Chart 4**: Long Structure (M1-M6 peaked at 118.5 USD/MT)
- **Chart 5**: Z-Score M1-M3 (5.25 = 5-sigma event)
- **Chart 6**: Z-Score M1-M6 (entire curve affected)
- **Chart 7**: Distribution (skewness 2.12, kurtosis 5.72)
- **Chart 8**: Spread vs Volatility (correlation 0.476-0.525)
- **Chart 9**: Event Timeline (April low → June peak)
- **Chart 10**: Market Dashboard (4-panel overview)
- **Chart 11**: Regime Classification (Normal/Tight/Stress/Crisis)

Each chart includes concise analysis (5 bullets max) with key observations and conclusions.

**5. Key Findings** (10 min)  
- **Summary Table**: All key metrics in one place
- **5.1**: Market Structure & Storage Economics
- **5.2**: Extreme Event Analysis (June-July 2025)
- **5.3**: Statistical Properties (fat tails, regime clustering)
- **5.4**: Actionable Framework (structure-volatility link)

**At a Glance: The June 2025 Crisis** (2 min)  
Timeline, key numbers, what it means - visual summary of the crisis.

**6. Conclusions** (10 min)  
- Summary of findings
- Trading & risk management framework
- **Example trade setup** (June 2025 with 9-day advance warning)
- Honest limitations & caveats
- Final thoughts

**7. Technical Note** (1 min)  
Methodology summary and applicability to other markets.

**Total reading time: ~1 hour**  
**Quick scan (Exec Summary + At a Glance + Summary Table): 5 minutes**

---

## Trading Framework

### Monitoring Dashboard
- Track M1-M3 and M1-M6 spreads daily
- Calculate 60-day rolling Z-scores
- Monitor 20-day rolling volatility
- Flag regime changes

### Signal Thresholds
| Z-Score | Interpretation | Action |
|---------|----------------|--------|
| **Z < -1** | Weak backwardation | Consider long calendar spreads |
| **Z > 2** | Notable tightening | Monitor closely |
| **Z > 3** | Strong anomaly | Reduce exposure or hedge |
| **Z > 4** | Extreme stress | Fundamentals dominate |
| **Z > 5** | Crisis-level event | Expect structural changes |

### Risk Management Rules
- Reduce position size when M1-M3 > 30 USD/MT
- Implement tail hedges when Z > 3
- Avoid volatility selling during backwardation extremes
- Use spread expansion as trigger for portfolio rebalancing

---

## Example Trade Setup (June 2025)

**Date:** June 10, 2025

**Market Observation:**
- M1-M3 = 45 USD/MT (rising from 20 USD/MT)
- Z-score = 2.8 (approaching 3)
- Volatility = 35% (rising from 25%)

**Signal:** Strong tightening, early warning of crisis

**Actions:**
1. Reduce long flat price exposure
2. Sell M1-M2 calendar spread (capture backwardation)
3. Buy volatility
4. Set alert for Z > 4

**Outcome:**
- June 19: Z hit 5.25, M1-M3 reached 85.25 USD/MT
- July 10: Volatility spiked to 78%
- **9 days advance warning** provided by framework

---

## Limitations

### Data Limitations
- 13-month sample is short for robust statistical inference
- No fundamental data (inventories, refinery runs) to confirm drivers
- Cannot determine if 2025 is typical without multi-year comparison

### Methodological Limitations
- Z-score window (60 days) is arbitrary - not optimized
- No out-of-sample testing for regime classification
- Correlation does not prove causation

### Honest Assessment
- **Findings are directionally correct** but magnitudes may vary
- **Framework is sound** but parameters need calibration
- **This is exploratory analysis**, not a production trading system
- More data and rigorous validation needed before deploying capital

---

## Future Work

### Short-term (1-2 weeks)
- [ ] Extend analysis to 2020-2024 data (establish historical baseline)
- [ ] Add fundamental data (EIA inventories, refinery runs)
- [ ] Optimize Z-score window (backtest different periods)

### Medium-term (1-2 months)
- [ ] Compare LSGO to other diesel benchmarks (US ULSD, Singapore gasoil)
- [ ] Build automated monitoring dashboard (real-time alerts)
- [ ] Develop predictive models using spread dynamics

### Long-term (3-6 months)
- [ ] Create systematic trading strategies based on regime classification
- [ ] Expand to other commodity markets (crude oil, natural gas, metals)
- [ ] Integrate machine learning for anomaly detection

---

## References

### Data Source
- ICE Low Sulphur Gasoil Futures settlement prices (Jan 2025 - Feb 2026)

### Key Concepts
- **Forward Curve**: Term structure of futures prices
- **Backwardation**: M1 > M2 (prompt barrels scarce)
- **Contango**: M1 < M2 (ample supply)
- **Z-Score**: Standardized measure of deviation from mean
- **Fat Tails**: Extreme events more frequent than normal distribution

### Related Markets
- ICE Brent Crude
- NYMEX WTI Crude
- NYMEX ULSD (US diesel)
- Singapore Gasoil

---

## Contact

For questions or collaboration opportunities, feel free to reach out.
