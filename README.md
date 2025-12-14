# Credit Risk Probability Model for Alternative Data
# 1. Project Overview

This project aims to build a credit scoring (Probability of Default) model for Bati Bank’s Buy Now, Pay Later (BNPL) product using eCommerce transactional data.
Because traditional credit bureau data is unavailable or limited, the model relies on alternative behavioral signals to assess credit risk while remaining compliant with financial regulations.

The final output is an interpretable credit risk model that supports responsible lending decisions and regulatory transparency.

# 2. Credit Scoring Business Understanding
# A. Basel II Accord, Risk Measurement, and Model Interpretability
The Basel II Capital Accord places strong emphasis on how banks measure, manage, and disclose credit risk, particularly under:
Pillar 1: Minimum Capital Requirements
Pillar 3: Market Discipline and transparency

Under Basel II, banks must quantify Expected Credit Loss, which depends heavily on the Probability of Default (PD). This project directly supports that requirement by producing a PD model.
However, Basel II does not only focus on model accuracy. It also requires clear documentation, validation, and explainable decision logic.
This means that highly accurate but opaque “black-box” models are risky in regulated financial environments. Instead, interpretable models such as Logistic Regression with Weight of Evidence (WoE) are preferred.
Using an interpretable model allows credit officers to explain approval or rejection decisions, enables risk teams to validate assumptions, and allows auditors to trace how risk is calculated. Interpretability is therefore a core business requirement, not a technical preference.

# B. Necessity and Risks of the Proxy Target Variable

The transactional dataset used in this project does not contain a direct “default” label. Without a target variable, supervised learning cannot be applied. To address this limitation, a proxy target variable is created.

The proxy is built using RFM (Recency, Frequency, Monetary) analysis and clustering. Customers who show low engagement, such as long inactivity, low transaction frequency, and low monetary value, are labeled as higher credit risk. This proxy serves as a stand-in for default behavior.
This approach is necessary to enable supervised model training and transform behavioral data into a usable credit risk signal. However, it introduces important business risks.
Low engagement does not always indicate inability or unwillingness to repay. Some financially healthy customers may simply shop infrequently, leading to potential misclassification. Overly conservative proxy definitions can also result in rejecting good customers and losing revenue. In addition, customer behavior can change over time, causing model drift and requiring continuous monitoring and recalibration.
For these reasons, proxy design is a critical business decision, not just a technical one.

# C. Trade-Offs Between Interpretable and Complex Models

In regulated financial systems, model selection involves a trade-off between predictive performance and explainability.
Simple, interpretable models such as Logistic Regression with WoE are transparent, stable, easy to audit, and well-suited for scorecard development. Their main limitation is lower maximum predictive performance.
More complex models such as Gradient Boosting can achieve higher accuracy and capture non-linear relationships, but they behave as black boxes and are difficult to explain and justify to regulators.
From a regulatory perspective, interpretable models are strongly preferred for final credit decisions. Complex models may be used for benchmarking or pre-screening, but final approvals typically rely on explainable models or require additional explainability layers.

For this project, Logistic Regression with WoE is selected as the foundational approach due to its strong alignment with regulatory requirements, transparency, and operational trust.

# Summary
This project focuses on building a regulation-aware, explainable, and business-aligned credit scoring system using alternative data, suitable for real-world banking and BNPL environments.
