# Emerging Technologies
**Module:** Emerging Technologies (Year 4, Semester 2)
**Author:** Matthew McCarthy

## About This Repository

This repository contains my assessment submission for the Emerging Technologies module. The primary deliverable is a Jupyter notebook (`problems.ipynb`) that explores the [Deutsch-Jozsa algorithm](https://doi.org/10.1098/rspa.1992.0167) — one of the earliest demonstrations of quantum computational advantage over classical computation.

### The Deutsch-Jozsa Problem

Given a black-box Boolean function that is promised to be either **constant** (same output for every input) or **balanced** (returns `True` for exactly half of its inputs), the goal is to determine which type it is using as few queries as possible. Classically, a 4-bit function requires up to 9 queries in the worst case. The Deutsch-Jozsa quantum algorithm solves the same problem with a single query — an exponential speedup achieved through [superposition](https://quantum.microsoft.com/en-us/insights/education/concepts/superposition) and [interference](https://quantum.microsoft.com/en-us/insights/education/concepts/interference).

### Notebook Overview

The notebook works through five problems that build on each other, progressing from classical computation to quantum circuit design:

1. **Generating Random Boolean Functions** — constructing classical oracle functions that are either constant or balanced, using truth tables and closures to simulate black-box behaviour.
2. **Classical Testing for Function Type** — building a deterministic classifier with early-exit optimisation, and analysing its worst-case query complexity (9 queries) using the pigeonhole principle.
3. **Quantum Oracles** — translating the four single-bit Boolean functions into reversible quantum gate circuits (identity, X, CNOT) following the XOR oracle model.
4. **Deutsch's Algorithm** — implementing the single-bit quantum algorithm with Qiskit, demonstrating phase kickback and interference to classify an oracle in one query.
5. **Scaling to Deutsch-Jozsa** — generalising to 4-bit inputs using multi-controlled X gates, showing that a single quantum query replaces up to 9 classical queries.

Two supplementary sections extend the analysis beyond the core brief:

- **Noise Simulation** — re-running the 4-bit algorithm under a depolarising noise model using `qiskit-aer`, and validating the diagnosis with a hand-optimised oracle that restores near-perfect accuracy for the constant cases.
- **Scaling Analysis** — running a generalised Deutsch-Jozsa circuit from $n=1$ to $n=10$ with `assert`-guarded correctness checks, and plotting classical ($2^{n-1}+1$) versus quantum (1) query counts on a log scale to make the exponential gap visible.

Each problem includes code implementations with type hints and docstrings, mathematical explanations with LaTeX, circuit visualisations, and independent verification tests.

## Getting Started

### Option 1: GitHub Codespaces (Recommended)

The easiest way to run this notebook is with [GitHub Codespaces](https://github.com/features/codespaces), which provides a pre-configured cloud environment with no local setup required:

1. Navigate to the repository on GitHub.
2. Click the green **Code** button and select **Open with Codespaces**.
3. Once the environment loads, open `problems.ipynb` and select **Kernel > Restart & Run All**.

### Option 2: Run Locally

#### Prerequisites

- [Python 3](https://www.python.org/downloads/) (3.10 or later recommended; developed and tested on 3.14)
- [Git](https://git-scm.com/)
- [Jupyter Notebook](https://jupyter.org/install) (`pip install jupyter`)

#### Clone the Repository

```bash
git clone https://github.com/MatthewMcCarthy1/emerging-technologies.git
cd emerging-technologies
```

#### Install Dependencies

It is recommended to use a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

#### Run the Notebook

```bash
jupyter notebook problems.ipynb
```

Then select **Kernel > Restart & Run All** to execute every cell from scratch.

## Repository Structure

```
emerging-technologies/
├── problems.ipynb      # Main assessment notebook
├── requirements.txt    # Python dependencies
├── .gitignore          # Standard Python/Jupyter ignores
└── README.md           # This file
```

## Technologies Used

- [NumPy](https://numpy.org/) — numerical arrays and random number generation for constructing oracle truth tables.
- [Matplotlib](https://matplotlib.org/) — plotting oracle output signatures and query count distributions.
- [pandas](https://pandas.pydata.org/) — displaying truth tables as formatted DataFrames.
- [Qiskit](https://qiskit.org/) — quantum circuit construction, visualisation, and statevector simulation. Used to implement the oracle circuits, Deutsch's algorithm, and the Deutsch-Jozsa algorithm.
- [Qiskit Aer](https://qiskit.github.io/qiskit-aer/) — high-performance shot-based simulator used in the noise simulation section to model realistic gate errors via a depolarising channel.
