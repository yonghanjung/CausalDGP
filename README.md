# CausalDGP: A Python Engine for Structural Causal Models

**A powerful and flexible Python library for creating, manipulating, and generating data from Structural Causal Models (SCMs) and analyzing causal graphs.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## 📖 Overview

**CausalDGP** provides a robust framework for causal inference research and experimentation. At its core, the library offers a `StructuralCausalModel` class and a suite of graph utility functions designed to handle complex causal structures.

While the engine is general-purpose, this package also serves as a benchmark, providing a standardized collection of data generating processes (DGPs) from the causal inference literature. It's designed to help researchers evaluate causal estimators under various challenging scenarios, such as:

* Back-door and front-door adjustment
* Unobserved confounding and "napkin" graphs
* Longitudinal and sequential time-series data
* Complex graphical structures requiring advanced identification strategies

---

## ⚙️ The Core Engine

The power of `CausalDGP` comes from two main components:

* **`scm.py`**: Provides the `StructuralCausalModel` class, which allows you to define complex data generating processes by specifying variables, their causal parents, and their functional relationships.
* **`graph.py`**: A suite of utility functions for graph manipulation and analysis, including topological sorting, finding ancestors, d-separation checks, and interactive graph visualization.

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
