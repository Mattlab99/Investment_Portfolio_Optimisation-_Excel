
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

![تصویر صفحه 2025-05-07 220654](https://github.com/user-attachments/assets/6fe9fca9-5d15-4849-a5fb-54f4e7d3ef75)


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


![Slide3](https://github.com/user-attachments/assets/032e00f1-2120-4262-92b1-aae292ea7123)

![Slide4](https://github.com/user-attachments/assets/386a29a2-ee44-4179-b39e-6d15f3575eb3)

---

## LP Model Formulation

Following Section 2 of the guide, I set up a Linear Program to **maximise total return** subject to:

- High-risk assets ≤ 15% total  
- Lowest-risk group gets the largest share  
- Each sector ≥ 15% (one sector forced ≥ 20%)  
- Each asset ≥ 5%  
- My own extra “diversity” rule

I coloured decision cells green and constraint cells blue in Solver, just like in class.

![Slide6](https://github.com/user-attachments/assets/0a034cfd-547c-4350-9088-3f50876d0401)

![Slide7](https://github.com/user-attachments/assets/d9e62627-0aa7-44f8-aad4-ac4abef740f4)

---

## LP Results & Sensitivity Analysis

- **Optimal weights** for each of the eight stocks  
- **Solver Sensitivity Report** showing shadow prices and reduced costs  
- Tested “what-if” tweaks on risk limits to see allocation shifts



![Slide8](https://github.com/user-attachments/assets/ccebb8c6-4dd7-4dc0-b62a-1a89e62f88f4)
![Slide9](https://github.com/user-attachments/assets/0d1bd972-49e5-45c7-8bce-3d6a33ff85ab)
![Slide11](https://github.com/user-attachments/assets/9c44f096-d58e-4dc7-8b60-057d5a3fcb27)
![Slide12](https://github.com/user-attachments/assets/6ed2f8fe-4775-4379-89f7-c2af711119f7)
![Slide13](https://github.com/user-attachments/assets/975dff3b-f706-4cb3-a3b6-47736d2f597d)


---

## ILP Model Formulation

Per Section 3, I converted to an Integer Linear Program:

- Binary decision \(x_i \in \{0,1\}\) for selecting exactly 5 assets  
- Must include all four sectors  
- At most one from R3, at least two from R1  
- Only allow an R3 pick if at least one R2 is chosen  
- One extra defendable rule of my own  
![Slide16](https://github.com/user-attachments/assets/7f843534-bc1e-4789-be90-d9894d574239)
![Slide17](https://github.com/user-attachments/assets/0e34de9b-65d3-471f-a650-21e79f87da6a)

---

## ILP Results

Solver’s integer run picked the “best 5” (e.g. TLS, CBA, XRO…) for a **3.6% expected portfolio return**, trading some diversification for a slightly higher yield.

![Slide18](https://github.com/user-attachments/assets/22216980-3832-4925-85e3-ebdc3506dff2)

---

## Summary & Recommendation

| Approach | Return | Diversification | Notes |
| :------- | :----- | :-------------- | :---- |
| **LP**   | 3.4%   | Smooth across 8 | Balanced, low concentration risk |
| **ILP**  | 3.6%   | Concentrated   | Higher return but more single-stock risk |

**Recommendation:** Use the LP solution for its balanced risk profile and smoother allocations, unless you need that extra 0.2% and can tolerate concentration.


![Slide19](https://github.com/user-attachments/assets/6da6838a-245d-4fb9-9b73-037572576779)

---

*Built with ☕ & 💡 by Matthew Tavakoli*  


