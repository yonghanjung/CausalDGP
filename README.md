# CausalDGP: A Python Engine for Structural Causal Models

**A powerful and flexible Python library for creating, manipulating, and generating data from Structural Causal Models (SCMs) and analyzing causal graphs.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## 📖 Overview

**CausalDGP** is a Python engine for causal inference research and experimentation. It provides a robust framework for defining complex causal systems, generating data from them, and analyzing their underlying graphical properties.

While the engine is a general-purpose tool, it also serves as a comprehensive benchmark, providing a standardized collection of data generating processes (DGPs) from the causal inference literature. It's designed to help researchers evaluate and compare estimators under challenging scenarios, including:

* Back-door and front-door adjustment
* Unobserved confounding and complex "napkin" graphs
* Longitudinal models with time-varying treatments
* Advanced identification strategies beyond simple adjustments

---

## ✨ Key Features

The power of `CausalDGP` comes from its modular design:

* **Flexible SCM Engine (`scm.py`)**: Define any SCM by specifying variables, their causal parents, and their functional relationships. The engine handles the recursive data generation process automatically.
* **Rich Graph Toolkit (`graph.py`)**: A suite of utility functions for causal graph analysis, including d-separation checks, finding ancestors, implementing do-calculus rules, and generating interactive visualizations.
* **Benchmark Suite (`generator.py`)**: A ready-to-use collection of famous and challenging SCMs from the literature, perfect for evaluating new methods.


For detailed API documentation, please see our `docs/` folder (coming soon).

---

## 🚀 Quick Start: The Benchmark Application

The easiest way to see `CausalDGP` in action is through the included benchmark generators (`generator.py`). These pre-built SCMs from the literature demonstrate the capabilities of the engine.

### Setup

1.  Make sure you have the necessary libraries installed:
    ```bash
    pip install networkx scipy matplotlib numpy pandas pyvis
    ```
2.  Install `CausalDGP` as an editable package to ensure all imports work correctly.

### Example: Generating Data

You can import any SCM from the `generator` module and use it to create a dataset. Here’s how to generate 1,000 samples from the **Kang & Schafer (2007)** simulation:

```python
# 1. Import a pre-built SCM generator from the CausalDGP package
from CausalDGP.generator import Kang_Schafer

# 2. Get the SCM object, treatment, and outcome variable names
scm, treatments, outcomes = Kang_Schafer(seednum=42)

# 3. Use the SCM object to generate a pandas DataFrame
sample_data = scm.generate_samples(num_samples=1000)

# 4. Display the first few rows of your new dataset
print(sample_data.head())
```

---

## 📊 Available Benchmark Models

CausalDGP includes a variety of pre-built SCMs from the causal inference literature. Below is a summary. For detailed mathematical descriptions and graph visualizations for each model, please see our [**Benchmark Details Documentation**](docs/benchmark_details.md).

| Model Function          | Brief Description                                           | Key Features & Notes                 |
| :---------------------- | :---------------------------------------------------------- | :------------------------------- |
| `BD_SCM` | A model for the standard back-door adjustment | User-defined covariate dimensions. |
| `Kang_Schafer`          | A classic model from [Kang & Schafer (2007)](https://projecteuclid.org/journals/statistical-science/volume-22/issue-4/Demystifying-Double-Robustness--A-Comparison-of-Alternative-Strategies-for/10.1214/07-STS227.full).   | - |
| `CCDDHNR2018_IRM`         | Interactive-Regression-Model (IRM) from [Chernozhukov et al. (2018)](https://academic.oup.com/ectj/article/21/1/C1/5056401).     | High-dimensional confounders     |
| `CCDDHNR2018_PLR`         | Partially-Linear-Regression (PLR) model from [Chernozhukov et al. (2018)](https://academic.oup.com/ectj/article/21/1/C1/5056401).       | Continuous treatment, high-dimensional confounders. |
| `SBD_SCM` | Standard sequential back-door adjustment.	 | Time-varying covariates and treatments. | 
| `mSBD_SCM` | Multi-outcome sequential back-door adjustment. | Multiple sequential outcomes. | 
| `luedtke_2017_sim1_scm` | Longitudinal model from [Luedtke et al., (2017)](https://arxiv.org/abs/1705.02459). | Sequential data with time-varying treatments. |
| `Canonical_FD_SCM` | Canonical front-door graph.	| No observed confounders of T and Y.  |
| `Fulcher_FD`            | A model for the Front-Door criterion, used in [Fulcher et al., (2020)](https://arxiv.org/pdf/1711.03611)  | Front-door with observed confounders.   |
| `FD_SCM`            | A model for the Front-door with covariates | Front-door model with high-dimensional confounders   |
| `Bhattacharya2022_Fig2b_SCM`            | A model used in [Bhattacharya et al., (2022)](https://www.jmlr.org/papers/v23/20-296.html) Figure 2b | Solvable by advanced identification, not front/back-door. |
| `Bhattacharya2022_Fig3_SCM`            | A model used in [Bhattacharya et al., (2022)](https://www.jmlr.org/papers/v23/20-296.html) Figure 3 | -  |
| `Bhattacharya2022_Fig5_SCM`            | A model used in [Bhattacharya et al., (2022)](https://www.jmlr.org/papers/v23/20-296.html) Figure 5 | -  |
| `Bhattacharya2022_Fig5_SCM`            | A model used in [Bhattacharya et al., (2022)](https://www.jmlr.org/papers/v23/20-296.html) Figure 5 | - |
| `ConeCloud_15_SCM`| A model for the 15-node Cone Cloud graph from Figure 3b of [Raichev et al., 2024](https://arxiv.org/abs/2408.14101)  | 	Large graph with categorical variables. |
| `Napkin_SCM`| The minimal "Napkin" graph. | Irreducible ratio of probabilities estimand. |
| `Napkin_SCM_dim`| 	Napkin graph with high-dimensional covariates. | Irreducible ratio with high-dimensional covariates. |
| `Napkin_FD_SCM`| Combines Napkin and Front-Door structures. | Irreducible ratio with front-door adjustment. |
| `Nested_Napkin_SCM`| Nested graph from [Tian (2002) Thesis](https://apps.dtic.mil/sti/tr/pdf/AD1007081.pdf) | Estimand is a ratio of two sequential back-door formulas. |
| `Double_Napkin_SCM`| Two stacked Napkin graphs.	 | Estimand is a ratio-of-ratios. |
| `Plan_ID_SCM`| A model from Figure [Figure 1b of Jung et al., 2021](https://yonghanjung.me/assets/pdf/R_5.pdf) | Not solvable by simple back-door or front-door. | 

## 📜 Citation
If you use CausalDGP in your research, please consider citing it:
```
@software{CausalDGP_2025,
  author = {Jung, Yonghan},
  title = {{CausalDGP: A Python Engine for Structural Causal Models}},
  url = {[https://github.com/yonghanjung/CausalDGP](https://github.com/yonghanjung/CausalDGP)},
  version = {0.1.0},
  year = {2025}
}
```
