# Fintech A/B Testing: From Hypothesis to Product Decision

An end-to-end **product analytics** case study evaluating whether a simplified virtual-card application flow improves completion conversion.

> **Project status:** Analysis notebook and supporting files are uploaded to the feature branch for review. The project uses synthetic educational data only. It contains no real customer or company data, and its results must not be interpreted as evidence about a real fintech product.

## Business Problem

A fintech product team is considering removing an optional step from its virtual-card application flow. The goal is to determine whether the simplified experience increases the share of users who complete an application without creating unacceptable negative effects.

### Experiment setup

- **Control (A):** current application flow.
- **Treatment (B):** simplified application flow.
- **Unit of randomization:** user.
- **Primary metric:** application completion conversion rate among all randomized users.
- **Guardrail metrics:** application error rate and completion time among users who complete the application.

## Hypotheses and planning assumptions

Let `p_A` and `p_B` denote application completion rates in groups A and B.

- **Null hypothesis (H₀):** `p_A = p_B`.
- **Alternative hypothesis (H₁):** `p_A != p_B`.
- **Significance level:** 5%, two-sided.
- **Target statistical power:** 80%.
- **Planning baseline:** 30% control conversion.
- **Minimum detectable effect (MDE):** +2 percentage points absolute.

These are explicitly stated planning assumptions, not observed business facts. The notebook calculates the sample size from these assumptions and generates a reproducible synthetic dataset.

## Analysis workflow

The notebook `notebooks/ab_test_analysis.ipynb` covers:

1. Business question, experimental design, primary metric, and guardrails.
2. Sample-size estimation for a two-sided two-proportion test.
3. Reproducible user-level synthetic data generation.
4. Data-quality assertions and allocation checks.
5. Conversion, absolute lift, relative lift, and denominators.
6. Two-proportion z-test, Wilson confidence intervals, and a confidence interval for the difference.
7. Pearson chi-square test as a cross-check.
8. Bootstrap confidence interval for absolute conversion lift.
9. Guardrail analysis for error rate and completion time.
10. A transparent, illustrative decision rule and limitations.

## Repository structure

```text
fintech-ab-testing/
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   └── ab_test_analysis.ipynb
├── data/
│   └── README.md
└── reports/
    └── README.md
```

## How to run locally

Use Python 3.10 or newer.

```bash
git clone https://github.com/VladislavTolmachev/fintech-ab-testing.git
cd fintech-ab-testing
git switch feature/experiment-analysis
python -m venv .venv
```

Activate the environment:

- **Windows PowerShell:** `.venv\\Scripts\\Activate.ps1`
- **Windows Command Prompt:** `.venv\\Scripts\\activate.bat`
- **macOS/Linux:** `source .venv/bin/activate`

Then install dependencies and launch Jupyter:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
jupyter notebook
```

Open `notebooks/ab_test_analysis.ipynb` and use **Kernel → Restart Kernel and Run All Cells**. The notebook has no saved outputs by design; execute it to generate results. The fixed random seed makes the simulation reproducible in the same compatible software environment.

## Interpretation principles

- Statistical significance is not the same as business significance.
- A non-significant result does not prove that variants are equivalent.
- Sample size, experiment duration, stopping rules, and guardrail thresholds should be defined before evaluating outcomes.
- Sample-ratio mismatch, missing outcomes, and instrumentation problems should be investigated before interpreting treatment effects.
- Completion time is conditional on completion and may be affected by changes in who completes the flow.
- Secondary metrics should not be overinterpreted without a plan for multiple comparisons.
- Synthetic data demonstrates an analysis workflow; it cannot establish the effect of a real product change.

## Limitations

This is a portfolio case study, not a production experimentation platform. The treatment effect is built into the simulation, so the resulting analysis is a demonstration rather than independent evidence. A real experiment would require validated exposure logging, a representative eligible population, a pre-defined stopping rule, instrumentation QA, sample-ratio checks, privacy review, and assessment of operational and business risks.

## Project status

- [x] Initial experiment specification
- [x] Reproducible synthetic-data notebook
- [x] Sample-size planning and primary statistical tests
- [x] Bootstrap and guardrail analysis
- [ ] Execute all cells in a clean local environment
- [ ] Review calculations and interpretation independently
- [ ] Incorporate review findings before merging to `main`
