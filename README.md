# CSB2025 - Practical Material for the Computational Systems Biology course, Fall 2025, session 10

This repository contains the practical material for the Computational Systems Biology (CSB 2025) course, session 10, focused on **Constraint-Based Metabolic Modelling (CBM)**. It includes a comprehensive Jupyter notebook used in the hands-on sessions, genome-scale metabolic models, experimental data, and setup instructions to reproduce the analyses.

## Contents

- `CBM_tutorial.ipynb` — Main hands-on notebook used in the practical sessions. It demonstrates model creation from scratch, genome-scale model loading and manipulation, flux balance analysis (FBA), gene knockout studies, and metabolic engineering design.
- `data/` — Contains models and experimental validation data:
  - `iJO1366.xml` the *E. coli* genome-scale model used in the tutorial
  - `iJO1366_anaerobic_wt.json` — Reference data for anaerobic wild-type simulations.
  - `m9_invivo_lethals.json` / `m9_invivo_lethals.csv` — In vivo essential genes under M9 minimal medium conditions.
  - `argonne_invivo_lethals.json` / `argonne_invivo_lethals.csv` — In vivo essential genes under Argonne medium conditions.
  - `argonne_media.json` / `argonne_media.csv` — Argonne medium composition.
- `requirements.txt` — Python package dependencies for the tutorial.
- `INSTALL` — Detailed installation instructions.
- `LICENSE` — BSD 3-Clause license for the repository.

## Citation and references

The material was mainly developed by Miguel Ponce de León (Barcelona Supercomputing Center (BSC)) and adapted by Arnau Montagud (Institute for Integrative Systems Biology (I2SysBio), CSIC-UV).

This material is a hands-on tutorial on constraint-based metabolic modelling using **COBRA** (COnstraint-Based Reconstruction and Analysis). The tutorial is designed to complement systems biology courses.

**Primary reference for COBRApy:**

Ebrahim, A., Lerman, J. A., Palsson, B. O., & Hyduke, D. R. (2013). "COBRApy: Constraints-Based Reconstruction and Analysis for Python". *BMC Systems Biology*, **7**, 74. https://doi.org/10.1186/1752-0509-7-74

**Full COBRApy documentation:** https://cobrapy.readthedocs.io/en/latest/

Additional references for the *E. coli* iJO1366 model and experimental validation data are included in the notebook.

## Quick overview

The notebook walks through:

- **Part 1: Warming up** — Building a toy metabolic model from scratch using COBRApy, learning basic model manipulation, and performing simple flux balance analysis.
- **Part 2: Genome-scale modelling** — Loading and inspecting the *E. coli* iJO1366 model, understanding model structure (reactions, metabolites, genes), examining boundary conditions and exchange fluxes.
- **Part 3: Flux Balance Analysis (FBA)** — Running FBA simulations, interpreting results, and analyzing metabolic flux distributions.
- **Part 4: Knock-out studies** — Performing single gene knockouts and systems-wide knockout analysis to identify essential genes, validating predictions against in vivo experimental data.
- **Part 5: Metabolic engineering** — Designing metabolic engineering strategies for production of metabolites of interest.

## Requirements

This tutorial uses **COBRApy**, the primary Python framework for constraint-based metabolic modelling. Two recommended ways to reproduce the environment:

### 1) Conda environment (recommended for users who prefer a native setup)

- Conda (Anaconda/Miniconda) installed.
- Use the environment already created and install COBRApy and required packages.

Example (PowerShell / WSL / macOS shell / Linux terminal):

```bash
conda activate CSB2025
conda install -c conda-forge glpk cobra
```

Notes:
- The `swiglpk` package (for linear programming) is typically installed automatically with `cobra` but can be installed separately if needed: `conda install -c conda-forge swiglpk`

### 2) Virtual environment with pip

If you prefer using Python's built-in `venv` module:

```bash
python3 -m venv csb2025_env
source csb2025_env/bin/activate  # On Windows: cbm_env\Scripts\activate
pip install -r requirements.txt
```

## How to run the notebook

### Using VS Code (recommended)

1. Open the repository folder in VS Code.
2. Ensure you have the Python extension installed.
3. Select the appropriate conda environment or virtual environment as the Python interpreter:
   - Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on macOS)
   - Search for "Python: Select Interpreter"
   - Choose your `CSB2025` conda environment or virtual environment
4. Open `CBM_tutorial.ipynb`.
5. Run the cells top-to-bottom. The notebook loads models from `./data/`.

### Using Jupyter in the browser

1. Open the repository folder in a terminal and activate the environment:

```bash
# if using conda environment
conda activate CSB2025

# if using virtual environment
source cbm_env/bin/activate  # On Windows: cbm_env\Scripts\activate

# start jupyter notebook
jupyter notebook
```

2. Navigate to `CBM_tutorial.ipynb` and open it.
3. Run the cells sequentially.

## Important notes and tips

- **First-time setup**: The first time you run the notebook, imports may take a while as packages initialize.
- **Linear programming solver**: COBRApy uses `swiglpk` (GLPK via SWIG) by default for linear programming. Alternatively, you can install commercial solvers like Gurobi or CPLEX if available.
- **Output directory**: Some cells write results to an `out/` directory. This will be created automatically when needed.
- **Gene knockout analysis**: The systems-wide knockout analysis in Part 4 may take several minutes to complete, as it performs FBA for every gene in the model (~4,400 genes for iJO1366).

## Models and data included

### iJO1366 model

The *E. coli* iJO1366 genome-scale metabolic model is used throughout the tutorial. This is one of the most comprehensive *E. coli* models available.

**Reference:**
- Orth, J. D., Conrad, T. M., Na, J., Lerman, J. A., Nam, H., Feist, A. M., & Palsson, B. Ø. (2011). "A comprehensive genome-scale reconstruction of *Escherichia coli* metabolism – 2011". *Molecular Systems Biology*, **7**, 535. https://doi.org/10.1038/msb.2011.65

**Access:** Available at the [BiGG Models database](http://bigg.ucsd.edu/models/iJO1366)

### Experimental validation data

- **M9 minimal medium lethals**: Essential genes under M9 (glucose + minimal salts) aerobic conditions.
- **Argonne medium lethals**: Essential genes under rich medium (Argonne) conditions, used for comparison.

These datasets allow students to validate FBA predictions against in vivo experimental results, calculating sensitivity, specificity, precision, and accuracy metrics.

## Notebook tasks and exercises

The notebook contains multiple hands-on exercises and evaluated assignments. Highlights:

- **Exercise 1.1–1.3**: Build a toy metabolic model, practice model manipulation, and perform basic FBA.
- **Exercise 2.1–2.4**: Inspect the iJO1366 model structure, query genes and reactions, and understand objective functions and exchange fluxes.
- **Exercise 3.1–3.2**: Perform single gene knockouts and conduct a genome-wide knockout analysis. Compare in silico predictions with in vivo experimental data.
- **Exercise 4.1**: Design a metabolic engineering project: select an organism and metabolite of interest, identify required reactions and enzymes, and design modifications.

### Evaluated exercises (graded assignments)

- **E1 (30%)**: Build a confusion matrix comparing in silico and in vivo knockout predictions.
- **E2 (30%)**: Calculate sensitivity, specificity, precision, and accuracy from the confusion matrix.
- **E3 (30%)**: Comment on the model's predictive capacity and discuss sources of errors.
- **E4 (10%)**: Design a metabolic engineering project with detailed justification.

## Getting started

1. **Clone or download this repository**:
   ```bash
   git clone https://github.com/ArnauMontagud/CSB2025_session10.git
   cd CSB2025_session10
   ```

2. **Set up your environment** (choose one of the methods above).

3. **Open the notebook** and run cells sequentially.

## Troubleshooting

- **Import errors**: Ensure all packages are installed in the active environment. Verify with `pip list` or `conda list`.
- **Model loading errors**: Check that the `data/iJO1366.xml` file exists and the path is correct (relative to the notebook directory).
- **Solver issues**: If you get a "No available solver" error, install `swiglpk` explicitly: `pip install swiglpk` or `conda install -c conda-forge swiglpk`.
- **Performance**: The genome-wide knockout analysis is computationally intensive and may take 5–10 minutes depending on your system.

## License

This repository is released under the BSD 3-Clause License. See `LICENSE` for details.

## Contact and support

For questions, issues, or feedback regarding this tutorial:
- Open an issue in the repository.
- Contact the course instructor.

**Authors:** Miguel Ponce de León (Barcelona Supercomputing Center) and Arnau Montagud (Institute of Integrative Systems Biology, I2SysBio, CSIC-UV)

## Launch in Binder

Click the badge below to launch the notebook in a free, cloud-based Binder environment (no installation needed, but with limited resources and a 10-minute inactivity timeout):

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/ArnauMontagud/CSB2025_session10/HEAD?urlpath=%2Fdoc%2Ftree%2FCBM_tutorial.ipynb)

**Note on Binder (as of November 2025):** Binder sessions have access to up to 2 GB of RAM. Sessions shut down after 10 minutes of inactivity but can run for up to 6 hours. See [Binder usage guidelines](https://mybinder.readthedocs.io/en/latest/user-guidelines.html) for details.
