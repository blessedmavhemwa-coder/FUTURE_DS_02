# FUTURE_DS_02
# Telco Customer Churn Analysis 📊

[![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=power%20bi&logoColor=black)](https://powerbi.microsoft.com/)
[![DAX](https://img.shields.io/badge/DAX-FFB800?style=for-the-badge&logo=microsoft&logoColor=black)](https://docs.microsoft.com/en-us/dax/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

## 📋 Overview

This project analyzes customer churn for a telecommunications company using a dataset of 7,043 customers. The analysis identifies key drivers of churn, creates customer segments, and provides actionable recommendations to improve customer retention.

**Key Question**: Why are customers leaving, and what can we do about it?

---

## 📊 Dashboard Preview

<img width="937" height="540" alt="Screenshot_27-4-2026_223941_" src="https://github.com/user-attachments/assets/f9b3c06c-70f8-4058-a2a3-74d15b7c34ce" />

---

## 📁 Dataset

The dataset contains 7,043 customer records with 21 features:
---

## 🔍 Key Findings

### 📈 Overall Metrics

| Metric | Value |
|--------|-------|
| Total Customers | 7,043 |
| Churned Customers | 1,869 |
| **Overall Churn Rate** | **26.5%** |
| Average CLV | $2,285 |
| Average Tenure | 32 months |

### 🎯 Top Churn Drivers

| Driver | Insight |
|--------|---------|
| **Contract Type** | Month-to-month customers churn at **42.5%** (5x higher than annual contracts) |
| **Payment Method** | Electronic check payers churn at **45.3%** |
| **Tech Support** | Fiber optic customers without tech support churn at **44%** |
| **Tenure** | 45% of churn occurs in first 6 months |

## 📊 Power BI Dashboard

The dashboard includes the following pages:

### Page 1: Dashboard
- KPI Cards (Total Customers, Churn Rate, Active Customers, Churned Customers)
- Churn Rate by Contract Type
- Churn by Payment Method
- CLV Distribution Histogram
- Retention by Tenure

---

## 📐 DAX Measures

Key measures used in the dashboard:

```dax
// Core Metrics
Total Customers = COUNTROWS(Telco)

Churned Customers = CALCULATE(COUNTROWS(Telco), Telco[Churn] = "Yes")

Churn Rate = DIVIDE([Churned Customers], [Total Customers], 0)

Total Revenue = SUM(Telco[TotalCharges])

Average CLV = AVERAGE(Telco[CLV])

// Segment Metrics
MonthToMonth Churn = 
CALCULATE(
    [Churn Rate],
    Telco[Contract] = "Month-to-month"
)

HighRiskCustomers = 
CALCULATE(
    COUNTROWS(Telco),
    Telco[Contract] = "Month-to-month",
    Telco[tenure] < 6,
    Telco[TechSupport] = "No"
)

// Retention Metrics
Retention Rate = 1 - [Churn Rate]

Cohort Retention = 
VAR CurrentCohort = SELECTEDVALUE(Telco[CohortMonth])
VAR OriginalCount = 
    CALCULATE(
        COUNTROWS(Telco),
        Telco[CohortMonth] = CurrentCohort,
        ALL(Telco[Churn])
    )
RETURN
    DIVIDE([Total Customers], OriginalCount, 0)
```

---

## 💡 Recommendations

Based on the analysis, here are the top retention strategies:

| **Priority** | **Action** | **Expected Impact** |
|--------------|------------|---------------------| 
| High | Incentivize month-to-month customers to switch to annual contracts (offer $50 bill credit) | 15-20% churn reduction |
| High | Implement 90-day onboarding program for new Fiber optic customers | 10-15% churn reduction |
| Medium | Offer $5/month discount for switching from electronic check to autopay | 8-10% churn reduction |
| Medium | Bundle Tech Support + Online Security for Fiber customers | 5-8% churn reduction |
| Low | Create loyalty program rewarding customers every 6 months | 3-5% churn reduction |

---

## 🛠️ Tools Used

| **Tool**	| **Purpose** |
|-----------|-------------|
| Power BI Desktop | Data visualization and dashboard creation |
| DAX | Measures and calculations |
| Power Query | Data cleaning and transformation |
| Excel | Initial data exploration |
| GitHub | Version control and project hosting |

---

## 📧 Contact

Blessed Mavhemwa - blessedmavhemwa@gmail.com
