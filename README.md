# Loss Reserving in Auto Liability: Chain Ladder & Bornhuetter-Ferguson

> An end-to-end actuarial reserving analysis built in R Markdown — from synthetic claims data generation through loss triangle construction and two industry-standard reserve estimation methods.

---

## Overview

One of the most important challenges in insurance is knowing how much money to set aside today for claims that won't fully settle until years in the future. This project demonstrates two foundational actuarial methods for answering that question:

- **Chain Ladder (Development Method)** — uses historical loss development patterns to project future losses
- **Bornhuetter-Ferguson (BF)** — blends observed data with an independent a priori expected loss estimate for more stable projections on immature accident years

The analysis is written for a general professional audience: actuarial concepts are explained in plain language throughout, making it accessible to analysts, data scientists, and finance professionals who may be new to insurance reserving.

---

## Project Structure

```
├── auto_liability_loss_triangle.Rmd   # Main analysis — knit this to produce the report
├── auto_liability_claims.csv          # Synthetic claims dataset (generated on knit)
└── README.md                          # You are here
```

---

## What's Inside the R Markdown

| Section | Description |
|---|---|
| **Glossary** | Plain-language definitions of key actuarial terms: accident year, development lag, IBNR, LDF, a priori loss ratio, and more |
| **Synthetic Data Generation** | Simulates 8 accident years × 8 development lags of auto liability claims with realistic noise; exports to CSV |
| **Loss Triangle Construction** | Builds cumulative paid and reported loss triangles using `tidyr::pivot_wider` |
| **Chain Ladder Method** | Computes volume-weighted age-to-age factors, CDFs, projected ultimates, and IBNR by accident year |
| **Bornhuetter-Ferguson Method** | Derives expected unreported losses from a priori assumptions and blends with observed data |
| **Comparison & Visualizations** | Side-by-side tables and three `ggplot2` charts comparing method outputs across accident years |

---

## Key Concepts Demonstrated

**Accident Year** — Claims are grouped by the year the loss event occurred, not when they were reported or paid. This is the standard basis for reserving analysis.

**Loss Triangle** — A matrix of cumulative losses where rows are accident years and columns are development lags. The upper-left is observed; the lower-right must be estimated.

**Age-to-Age Factors (LDFs)** — Multipliers describing how much cumulative losses grow from one lag to the next. Volume-weighted averages across accident years are used as the industry standard.

**IBNR (Incurred But Not Reported)** — The reserve an insurer must hold for losses that have occurred but aren't yet fully reflected in the books. Computed as: `Ultimate − Reported to Date`.

**Why BF over Chain Ladder alone?** — Chain Ladder amplifies noise in immature accident years because it extrapolates from limited data. BF anchors recent years to an independent expectation, producing more stable estimates where data is thin.

---

## Getting Started

### Prerequisites

This project requires **R** (≥ 4.1) and **RStudio**. Install the required packages if you don't already have them:

```r
install.packages(c("tidyverse", "knitr", "kableExtra", "scales"))
```

### Running the Analysis

1. Clone or download this repository
2. Open `auto_liability_loss_triangle.Rmd` in RStudio
3. Click **Knit → Knit to HTML**

The report will render as a self-contained HTML file with a floating table of contents, syntax-highlighted code blocks, and all charts inline. The CSV file `auto_liability_claims.csv` will be written to your working directory automatically.

---

## Output Preview

The rendered report includes:

- 📋 A reference glossary of actuarial terms
- 📐 8×8 cumulative paid and reported loss triangles
- 📊 Age-to-age factor (LDF) and CDF tables
- 💰 Chain Ladder and BF ultimate loss and IBNR estimates by accident year
- 📈 Three `ggplot2` visualizations:
  - Ultimate loss projections (CL vs. BF)
  - IBNR reserves by accident year (CL vs. BF)
  - Cumulative reported loss development curves by accident year

---

## Data Notes

All claims data in this project is **fully synthetic** and generated programmatically using `set.seed(42)` for reproducibility. It is designed to mimic realistic auto liability development patterns but does not represent the financials of any real insurance company or book of business.

The a priori loss ratios used in the BF method (ranging from 0.70 to 0.73) are illustrative assumptions. In practice, these would be derived from pricing analyses, industry benchmarks, or actuarial judgment.

---

## Methods Reference

| Method | Source |
|---|---|
| Chain Ladder / Development Method | Standard actuarial practice; see CAS Study Note on Loss Development |
| Bornhuetter-Ferguson | Bornhuetter, R.L. and Ferguson, R.E. (1972). "The Actuary and IBNR." *PCAS*, Vol. LIX |

---

## Author

**Christopher Flynn**
- 🌐 [christopherflynn.dev](https://yourwebsite.com)
- 💼 [LinkedIn](https://www.linkedin.com/in/christopherflynndev/)
- 🐙 [GitHub](https://github.com/christopherFlynn)

---

## License

This project is open source and available under the [MIT License](LICENSE).

---

*Built with R, R Markdown, tidyverse, and kableExtra.*