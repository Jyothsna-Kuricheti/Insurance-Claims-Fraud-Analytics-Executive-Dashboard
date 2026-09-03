# Auto Insurance Claims & Fraud Analytics Executive Dashboard

An executive-grade Business Intelligence solution developed in **Power BI** to analyze financial loss exposure, claim velocities, demographic risk profiles, and suspicious filing behavior across an automobile insurance portfolio (Jan–Feb 2015).

---

## 🎯 Business Objectives
* **Quantify Loss Exposure:** Track portfolio liability distributions across policy limits and incident types.
* **Identify Fraud Hotspots:** Isolate high-risk intersections between incident severity and claim types to combat financial leakage.
* **Support Underwriting & Claims Operations:** Provide actionable demographic and temporal benchmarks for risk selection and fraud triage.

---

## 🔑 Key Portfolio Metrics (KPIs)
* **Total Claims:** 1,000
* **Total Claim Amount:** $52.76M
* **Average Claim Amount:** $52.76K
* **Fraud Claim Rate:** 24.70% (247 confirmed fraudulent claims totaling $14.89M)

---

## 💡 Core Analytical Insights
* **Collision Loss Dominance:** Single-Vehicle ($25.97M) and Multi-Vehicle ($25.83M) collisions account for over **98% of total dollar exposure**.
* **Disproportionate Fraud Rates:** Single-Vehicle Collisions carry the highest fraud propensity at **29.03%**, followed by Multi-Vehicle Collisions at **27.21%**.
* **Severity Bias:** Across all fraudulent claims, **67.61% fall under "Major Damage"**, demonstrating that fraudulent claims heavily simulate major damage to maximize payouts.
* **Demographic Exposure:** Policyholders aged **30–45** account for the largest financial exposure across both genders ($19M Female / $14M Male).

---

## 🛠️ Data Modeling & DAX Formulas

### Core DAX Measures
```dax
// Total Claim Count
Claim Count = COUNTROWS('insurance dataset - LMS (1)')

// Gross Incurred Exposure
Total Claim Amount = SUM('insurance dataset - LMS (1)'[total_claim_amount])

// Average Claim Exposure
Avg Claim Amount = AVERAGE('insurance dataset - LMS (1)'[total_claim_amount])

// Portfolio Fraud Percentage
Fraud Claim % = 
DIVIDE(
    CALCULATE([Claim Count], 'insurance dataset - LMS (1)'[fraud_reported] = "Y"),
    [Claim Count],
    0
)

```
## Demographic Binning (Calculated Column)

```Age Group = 
SWITCH(
    TRUE(),
    'insurance dataset - LMS (1)'[age] < 30, "1. Under 30",
    'insurance dataset - LMS (1)'[age] <= 45, "2. 30 - 45",
    'insurance dataset - LMS (1)'[age] <= 60, "3. 46 - 60",
    "4. Over 60"
)
 ```


- **Executive KPI Ribbon:** High-level operational cards displaying Claim Count, Gross Exposure, Average Claim, and Fraud Rate.
- **Dual-Axis Temporal Chart:** Tracking daily claim volume vs. aggregate dollar exposure across Jan-Feb 2015.
- **Severity and Policy Breakdown:** Donut chart for incident severity and horizontal bar chart for Policy CSL limits (100/300, 250/500, 500/1000).
- **Demographics:** Age group analysis broken down by gender.
- **Risk Matrix:** Tabular risk breakdown with conditional formatting highlighting fraud concentrations.
- **Interactive Slicer Panel:** Dedicated controls for Fraud Reported (Y/N), Policy Limit (CSL), and Date Range.

## 🚀 How to Run Locally
1. Clone this repository to your local machine:
   https://github.com/Jyothsna-Kuricheti/Insurance-Claims-Fraud-Analytics-Executive-Dashboard.git

2. Open the pbix file in Power BI Desktop.

3. Use the slicers to filter and explore the portfolio interactively.
