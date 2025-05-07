git pull origin main
# fix any file names in images/, and make sure README.md paths match
git add images README.md
git commit -m "Fix image paths and filenames"
git push origin main


# Stock Portfolio Optimizer

This is a personal data-analytics project where I built a decision-model in Excel to optimize a simple stock portfolio. It showcases:

- **Linear & Integer-linear programming** using Excel Solver  
- **Sensitivity analysis** to understand how changes in returns affect the optimal allocation  
- A step-by-step walkthrough of model setup, outputs, and interpretation

## 📂 Project structure

- **data/**  
  - `Tavakoli_Mehdi_224304485_MIS775.xlsx`  
    – My Excel workbook with all model formulations, Solver setups, and sensitivity sheets

- **report/**  
  - `Tavakoli_Mehdi_224304485_MIS775.pptx`  
    – A concise slide deck that walks through problem definition, model logic, results, and insights


## 🚀 How to explore

1. Open the Excel file in **data/**  
   - Inspect the LP vs. ILP setups  
   - Review Solver’s optimal allocations and sensitivity outputs

2. Browse the slides in **report/** for a narrated overview of my process and key takeaways

3. Feel free to fork this repo and adapt the model to your own portfolio ideas!

   ## 🛠️ What I Did

1. **Gathered data**: Collected historical stock returns and risk metrics.  
2. **Built LP & ILP models**: Set up allocation constraints in Excel Solver.  
3. **Ran sensitivity analysis**: Tested how portfolio weights shift when returns change.  
4. **Compiled insights**: Summarised optimal allocations and “what-if” scenarios.

   # Stock Portfolio Optimizer

A personal data-analytics project that walks through how I built an Excel-based decision model to optimise a simple stock portfolio—step by step, story-style, with screenshots from my PowerPoint.

---

## 📖 Table of Contents

- [Introduction](#introduction)  
- [Data Gathering](#data-gathering)  
- [Calculating Returns & Risk Classification](#calculating-returns--risk-classification)  
- [LP Model Formulation](#lp-model-formulation)  
- [LP Results & Sensitivity Analysis](#lp-results--sensitivity-analysis)  
- [ILP Model Formulation](#ilp-model-formulation)  
- [ILP Results](#ilp-results)  
- [Summary & Recommendation](#summary--recommendation)  

---

## Introduction

I kicked off this side-project by defining the core question:  
> “What’s the optimal mix of eight ASX-listed stocks to maximise expected return, while keeping risk and sector exposures under control?”  

This came straight from the guide’s Purpose & Context, which calls for 48 months of real price data and two optimisation methods—LP and ILP.

![Introduction Slide](Slide1.png)

---

## Data Gathering

1. **Stock Selection**  
   - Started with the four “given” tickers (PME, XRO, TLS, CBA)  
   - Added four more from diverse sectors via MarketIndex to capture different volatility profiles  

2. **Fetching Price History**  
   - Used Excel’s `STOCKHISTORY` function to pull Jan 2021–Jan 2025 monthly closes:  
     ```  
     =STOCKHISTORY("XASX.PME", "01-01-2021", "01-01-2025", 2, 1, 0, 1)  
     ```  

![Data Gathering](images/Slide2.png)

---

## Calculating Returns & Risk Classification

- **Monthly Returns**  
  \[
    \text{Return}_t = \frac{\text{Close}_t - \text{Close}_{t-1}}{\text{Close}_{t-1}}
  \]  
  formatted to two decimal places.

- **Risk Groups**  
  - Computed each stock’s average return and standard deviation.  
  - Defined three risk buckets (R1=low vol, R2=medium, R3=high), ensuring at least two assets per bucket.

![Returns & Risk](images/Slide3.png)

---

## LP Model Formulation

Following Section 2 of the guide, I set up a Linear Program to **maximise total return** subject to:

- High-risk assets ≤ 15% total  
- Lowest-risk group gets the largest share  
- Each sector ≥ 15% (one sector forced ≥ 20%)  
- Each asset ≥ 5%  
- My own extra “diversity” rule

I coloured decision cells green and constraint cells blue in Solver, just like in class.

![LP Model Setup](images/Slide4.png)

---

## LP Results & Sensitivity Analysis

- **Optimal weights** for each of the eight stocks  
- **Solver Sensitivity Report** showing shadow prices and reduced costs  
- Tested “what-if” tweaks on risk limits to see allocation shifts

![LP Results & Sensitivity](images/Slide5.png)

---

## ILP Model Formulation

Per Section 3, I converted to an Integer Linear Program:

- Binary decision \(x_i \in \{0,1\}\) for selecting exactly 5 assets  
- Must include all four sectors  
- At most one from R3, at least two from R1  
- Only allow an R3 pick if at least one R2 is chosen  
- One extra defendable rule of my own  

![ILP Model Setup](images/Slide6.png)

---

## ILP Results

Solver’s integer run picked the “best 5” (e.g. TLS, CBA, XRO…) for a **3.6% expected portfolio return**, trading some diversification for a slightly higher yield.

![ILP Results](images/Slide7.png)

---

## Summary & Recommendation

| Approach | Return | Diversification | Notes |
| :------- | :----- | :-------------- | :---- |
| **LP**   | 3.4%   | Smooth across 8 | Balanced, low concentration risk |
| **ILP**  | 3.6%   | Concentrated   | Higher return but more single-stock risk |

**Recommendation:** Use the LP solution for its balanced risk profile and smoother allocations, unless you need that extra 0.2% and can tolerate concentration.

![Summary & Recommendation](Investment_Portfolio_Optimisation-_Excel
/Slide8.PNG)

---

*Built with ☕ & 💡 by Matthew Tavakoli*  


