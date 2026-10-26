# Fintech A/B Testing: From Hypothesis to Product Decision

An end-to-end **product analytics** case study evaluating whether a simplified virtual-card application flow improves completion conversion.

> **Project status:** In development. This repository uses synthetic data for educational purposes. It contains no real customer or company data, and its results must not be interpreted as evidence about a real fintech product.

## Business Problem

A fintech product team is considering removing an optional step from its virtual-card application flow. The goal is to determine whether the simplified experience increases the share of users who complete an application without creating unacceptable negative effects.

### Experiment setup

- **Control (A):** current application flow.
- **Treatment (B):** simplified application flow.
- **Unit of randomization:** user.
- **Primary metric:** application completion conversion rate.
- **Guardrail metrics:** application error rate and completion time among users who complete the application.

## Hypotheses

Let \(p_A\) and \(p_B\) denote the application completion rates in groups A and B.

- **Null hypothesis (H₀):** \(p_A = p_B\).
- **Alternative hypothesis (H₁):** \(p_A \ne p_B\).
- **Significance level:** 5%, two-sided.
- **Target statistical power:** 80%.
- **Planning baseline:** 30% conversion in the control group.
- **Minimum detectable effect (MDE):** +2 percentage points absolute.

These values are planning assumptions. They will be reviewed as part of the analysis; they are not observed business results.

## Planned Methodology

1. Define the experiment, primary metric, guardrails, and hypotheses.
2. Estimate the required sample size based on the baseline conversion, MDE, significance level, and target power.
3. Generate reproducible synthetic user-level experiment data.
4. Validate data quality, group allocation, and key assumptions.
5. Calculate conversion rates, absolute lift, and relative lift.
6. Apply a two-proportion z-test and Pearson chi-square test.
7. Estimate uncertainty using confidence intervals and bootstrap resampling.
8. Review guardrail metrics.
9. Translate the statistical results into a product recommendation, including limitations and next steps.

## Tools

- Python
- pandas and NumPy
- SciPy
- statsmodels
- Jupyter Notebook
- Matplotlib

## Planned Project Structure

```text
fintech-ab-testing/
├── README.md
├── requirements.txt
├── notebooks/
│   └── fintech_ab_test.ipynb
├── data/
│   └── README.md
└── reports/
    └── README.md
```

The notebook and supporting files will be added after the initial project specification is reviewed.

## How to Run

Run instructions and dependencies will be added with the first runnable notebook. The intended workflow is to install the listed Python dependencies and execute the notebook from top to bottom.

## Interpretation Principles

- Statistical significance is not the same as business significance.
- A non-significant result does not prove that the variants are equivalent.
- Sample size, experiment duration, and stopping rules should be defined before evaluating outcomes.
- Sample-ratio mismatch, missing outcomes, and instrumentation problems should be investigated before interpreting treatment effects.
- Guardrails and implementation costs matter alongside the primary metric.
- Synthetic data demonstrates an analysis workflow; it cannot establish the effect of a real product change.

## Limitations

This is a portfolio case study, not a production experimentation platform. The analysis will depend on stated simulation and statistical assumptions. A real experiment would require validated exposure logging, a representative eligible population, a pre-defined stopping rule, instrumentation QA, privacy review, and assessment of operational and business risks.

## Project Status

- [x] Repository created
- [x] Initial experiment specification documented
- [ ] Implement reproducible synthetic data generation
- [ ] Complete statistical analysis notebook
- [ ] Validate calculations and conclusions
- [ ] Add final charts and an evidence-based product recommendation
