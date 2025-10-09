## 💳 Macro-Credit Stress Simulation Engine

This module implements a simulation framework to translate macroeconomic shocks  
(e.g., GDP declines, inflation spikes) into credit portfolio risk metrics  
such as **Probability of Default (PD)**, **Loss Given Default (LGD)**, and **Expected Credit Loss (ECL)**.

It is designed as a **learning and prototyping environment** for CCAR / IFRS-9 style stress testing,  
where macroeconomic scenarios are propagated through econometric models into loan portfolio losses.

---

## ✨ Features

### **Econometric Foundations**
- Fetch GDP and CPI data from FRED API  
- Perform **stationarity checks (ADF tests)**  
- Run **Johansen cointegration tests** to detect long-run equilibrium  
- Estimate **VECM / VAR models** and generate **Impulse Response Functions (IRFs)**  

### **Scenario Design**
- Build **inflation**, **recession**, and **stagflation** macro paths from IRFs  
- Overlay regulator-style stress magnitudes (scaling IRFs to simulate shocks)  
- Decompose variance via **Forecast Error Variance Decomposition (FEVD)**  

### **Credit Risk Mapping**
- Stylized loan portfolio with segments: **Retail**, **SME**, **Corporate**  
- Apply segment-specific **elasticities** to map macro shocks into PD changes  
- Impose PD floors / caps for realism  
- Compute **stressed ECLs** across 12-quarter horizons  

### **Visualization**
- Plot dynamic **ECL paths** for multiple scenarios  
- Compare **inflation-driven**, **recession-driven**, and **stagflation** responses  

---

## 📂 Folder Structure

```text
macro-credit-sim/
├── notebooks/             # Jupyter notebooks (interactive workflows)
│   └── macro-vecm-demo.ipynb
├── src/                   # Python modules (reusable functions)
├── data/                  # Input datasets (gitignored)
├── requirements.txt        # Python dependencies
└── README.md              # Project documentation


📊 Reports

+ Interactive Report (IRFs + ECL paths)
👉 Macro Credit Stress Simulation (VECM Demo)

+ Notebook (Code & Analysis)
📘 View macro-vecm-demo.ipynb on GitHub

+ Back to Main Page:
🏠 investment-analytics home

📈 Interpretation Highlights
Impulse Response Functions (IRFs)

+ GDP → CPI: A negative GDP shock dampens inflation temporarily, but the effect fades after several quarters.

+ CPI → GDP: Inflation shocks reduce output growth over time, showing a gradual adjustment path.
This aligns with macro intuition — inflation shocks slow real activity, while growth boosts CPI.

ECL Paths
| Scenario        | Pattern                                  | Portfolio Implication                                        |
| --------------- | ---------------------------------------- | ------------------------------------------------------------ |
| **Inflation**   | Slow and persistent rise                 | Corporate losses dominate; SME proportionally most sensitive |
| **Recession**   | Sharp initial spike, then mean reversion | GDP recovery tempers ECL after initial quarters              |
| **Stagflation** | Blend of both, moderate but persistent   | Dual impact on PDs and LGDs                                  |

🔮 Next Steps

+ Extend to multi-factor VARs (e.g., add interest rates, unemployment).

+ Compare statistical scenario overlays with event-driven simulations
(as in a two-layer resilience simulator combining macro + idiosyncratic shocks).