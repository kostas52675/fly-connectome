# Predicting Neuron Cell Types from Whole-Brain Connectivity

Machine learning on the FlyWire connectome of the adult Drosophila melanogaster brain (~139,000 neurons, ~15 million synapses). The goal is to predict a neuron's cell type using only how it is wired into the rest of the brain.

## Research question

> How much of a neuron's identity is written in its connectivity?

Given only features describing each neuron's wiring and size (input/output partners and synapses, the neurotransmitter profile of its outputs, cell size, and synapses per brain region), how accurately can we predict its super-class? We compare a simple baseline (logistic regression) with gradient-boosted trees, evaluate with metrics that account for strong class imbalance, and examine which features drive the predictions. As an extension, we test how performance changes at a finer level of the cell-type hierarchy (class).

## Data

FlyWire connectome, materialization **v783**, downloaded from the
[FlyWire Codex](https://codex.flywire.ai). Data files are not included in this
repository; see [`data/README.md`](data/README.md) for the file list and a description of each
column.

If you use this data, please cite:

- Dorkenwald, S., Matsliah, A., Sterling, A. R., et al. (2024).
  Neuronal wiring diagram of an adult brain. *Nature*, 634, 124–138.
  https://doi.org/10.1038/s41586-024-07558-y
- Schlegel, P., Yin, Y., Bates, A. S., et al. (2024).
  Whole-brain annotation and multi-connectome cell typing of *Drosophila*. *Nature*, 634, 139–152.
  https://doi.org/10.1038/s41586-024-07686-5

## Installation

Requires Python 3.11+. Everything runs on CPU.

```bash
git clone <repo-url>
cd fly-connectome

python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS / Linux
source .venv/bin/activate

pip install -r requirements.txt
```

Then place the FlyWire `.csv.gz` files in `data/` and open the notebooks in `notebooks/`.

## Project structure

```
fly-connectome/
├── data/            # FlyWire data files (not tracked by git)
├── notebooks/       # one notebook per phase (00_data.ipynb, 01_linreg.ipynb, ...)
├── src/             # reusable functions (e.g. features.py)
├── results/         # figures and tables for the final report
└── requirements.txt
```

## Project phases

- [ ] **Phase 0 – Data:** load the FlyWire tables, exploratory analysis, per-neuron connectivity features, train/validation/test split.
- [ ] **Phase 1 – Linear regression:** predict a continuous quantity (e.g. number of output synapses); MSE, R², ridge and lasso.
- [ ] **Phase 4 – Neural networks:** Keras MLP for multi-class cell-type prediction; softmax, early stopping, class imbalance.
- [ ] **Phase 5 – CNN (optional):** classify cell type from 2D images of neuron morphology; compare shape vs. connectivity.