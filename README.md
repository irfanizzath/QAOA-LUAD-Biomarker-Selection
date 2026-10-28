# QAOA-LUAD-Biomarker-Selection

# Gene42: Quantum-Optimized Biomarker Discovery for Lung Adenocarcinoma

**A quantum-classical framework for selecting compact gene panels to distinguish lung adenocarcinoma (LUAD) from non-cancerous samples.**

Developed for the **Qiskit Fall Fest 2026 — Quantum Biology Track**, Khalifa University.

## Overview

We explored whether quantum optimization can help identify compact, interpretable gene panels for lung adenocarcinoma classification.

The pipeline combines bioinformatics, machine learning, combinatorial optimization, and quantum computing to select four-gene panels from transcriptomic data.

Rather than treating classification accuracy as the only objective, Gene42 investigates the trade-off between predictive relevance and redundancy among candidate genes.

## Key Features

- **Bioinformatics preprocessing:** Gene-expression cleaning and feature preparation.
- **Feature selection:** Stability analysis, differential-expression signals, and predictive relevance.
- **QUBO optimization:** Formulation of four-gene selection as a Quadratic Unconstrained Binary Optimization problem.
- **Quantum optimization:** Quantum Approximate Optimization Algorithm (QAOA) experiments at multiple circuit depths.
- **Classical baselines:** Random Forest, LASSO, recursive feature elimination, minimum-redundancy maximum-relevance, simulated annealing, and random search.
- **IBM Quantum experiments:** Evaluation of QAOA sampling on the `ibm_marrakesh` backend.
- **Validation:** Patient-level nested cross-validation and comparison of candidate gene panels.

## Methodology

The workflow consists of five main stages:

1. **Data preparation:** Clean the expression matrix, resolve gene identifiers, and prepare the classification labels.
2. **Candidate screening:** Identify a manageable set of candidate genes using predictive relevance and selection stability.
3. **QUBO construction:** Encode gene relevance, redundancy, and the four-gene cardinality constraint into an optimization objective.
4. **Optimization:** Compare exact optimization, QAOA, and classical search strategies.
5. **Evaluation:** Assess classification performance, panel consistency, and agreement between simulated and physical quantum experiments.

## Candidate Gene Panels

Two panels are of particular interest in the current experiments.

### Predictive candidate

`FGFRL1`, `CLCA4`, `DPY19L1`, `DNASE1L3`

Selected by the Random Forest and top-four single-gene AUROC approaches in the full-data analysis.

### Quantum-optimization candidate

`CLCA4`, `ACAP2`, `LIMCH1`, `THBS3`

The exact QUBO optimum, also recovered in one recorded IBM Quantum hardware run.

These panels represent different selection objectives. Neither should be considered a clinically validated diagnostic signature without independent external validation.

## Quantum Computing Experiments

Gene42 evaluates QAOA at circuit depths p = 1, 2, and 3 and compares the results with classical optimization methods.

The recorded physical-hardware experiments use IBM Quantum's `ibm_marrakesh` backend, with 1,024 final measurement shots per run.

The experiments investigate:

- Recovery of the exact QUBO optimum.
- Stability across random seeds.
- Valid four-gene bitstring frequency.
- Optimization quality relative to classical methods.
- The effect of finite sampling and hardware execution.

Recovery of a QUBO optimum demonstrates optimization performance on the specified objective. It does not, by itself, establish quantum advantage or superior diagnostic accuracy.

## Validation and Limitations

The current study uses a small LUAD-versus-normal cohort. Nested cross-validation provides a structured evaluation framework, but the reported performance estimates may be uncertain and require independent confirmation.

Important limitations include:

- Small sample size.
- Potential sensitivity to data preprocessing and sample composition.
- Differences between optimization objectives and predictive performance.
- Potential instability of gene selection across folds.
- The need for external validation and more extensive classical baselines.

Gene42 is an experimental research project, not a clinical diagnostic tool.

## Repository Structure

```text
quantum-luad-gene-panel/
├── README.md
├── Gene42_Pipeline.ipynb
├── data/
│   └── README.md
├── seeds/
│   ├── README.md
│   ├── seed_42.txt
│   ├── seed_256.txt
│   └── seed_1024.txt
├── results/
│   └── README.md
└── requirements.txt
```

The directory structure is a suggested organization; update it to match the files actually committed to the repository. Do not commit restricted patient data, credentials, or IBM Quantum API tokens.

## Getting Started

### Requirements

- Python 3.10 or a compatible environment.
- Jupyter Notebook or Google Colab.
- Qiskit and the relevant optimization and machine-learning dependencies.
- IBM Quantum account and appropriate backend access for hardware experiments.

### Run the notebook

1. Clone or download the repository.
2. Install the project's dependencies.
3. Open `Gene42_Pipeline.ipynb` in Jupyter or Google Colab.
4. Configure the dataset paths and experiment settings.
5. Run the preprocessing, selection, optimization, and evaluation stages in order.

Install dependencies, if a complete `requirements.txt` is provided:

```bash
pip install -r requirements.txt
```

Hardware experiments require separate IBM Quantum authentication and backend access. Use environment variables or secure notebook secrets rather than embedding API tokens in source code.

## Reproducibility

For reproducible experiments, record:

- Dataset provenance and preprocessing steps.
- Random seeds and cross-validation splits.
- QUBO coefficients and constraint definitions.
- QAOA circuit depth, optimizer settings, and shot counts.
- IBM backend and job identifiers.
- Software versions and the evaluation metrics used.

Distinguish simulated experiments, saved hardware results, and newly executed hardware jobs in all reports.

## Future Work

- Validate candidate panels on independent LUAD datasets.
- Quantify uncertainty in classification metrics.
- Test performance against repeated random-panel baselines.
- Investigate the biological roles and cell-type origins of selected genes.
- Compare quantum and classical methods under matched computational budgets.
- Evaluate whether the selected panels generalize across cohorts and preprocessing pipelines.


## Team 

Mohamed Irfan · Bogdan Egorov · Jayanth Venkatesan · Hasmik Chilingaryan  — University of Birmingham Dubai

## Disclaimer

This project is intended for research and educational purposes. Its results do not establish clinical validity, clinical utility, or quantum computational advantage.

## License

Choose and add an appropriate open-source license before distributing the repository. Ensure that the code and datasets can legally be shared under the selected terms.
