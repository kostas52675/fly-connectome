# Predicting Neuron Cell Types from Whole-Brain Connectivity

Machine learning on the **FlyWire connectome** of the adult *Drosophila melanogaster* brain
(~139,000 neurons, ~15 million synapses). The goal is to predict a neuron's **cell type** and
**neurotransmitter** using only how it is wired into the rest of the brain.

## Research question

> How much of a neuron's identity is written in its connectivity?

Given only connectivity-derived features for each neuron (input/output degree, synapse counts
per brain region, fraction of inhibitory inputs, etc.), how accurately can we predict its cell
type and neurotransmitter? Which models work best, and do unsupervised clusters in connectivity
space line up with the annotated cell types?

## Data

FlyWire connectome, materialization **v783**, downloaded from the
[FlyWire Codex](https://codex.flywire.ai/api/download). Data files are not included in this
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
- [ ] **Phase 2 – Logistic regression:** excitatory vs. inhibitory neurons; cross-entropy, decision threshold, confusion matrix, precision/recall/F1.
- [ ] **Phase 3 – SVM:** linear, polynomial and RBF kernels; tuning C and γ; one-vs-one / one-vs-rest for multiple neurotransmitters.
- [ ] **Phase 4 – Neural networks:** Keras MLP for multi-class cell-type prediction; softmax, early stopping, class imbalance.
- [ ] **Phase 5 – CNN (optional):** classify cell type from 2D images of neuron morphology; compare shape vs. connectivity.
- [ ] **Phase 6 – Unsupervised learning:** PCA, t-SNE, k-means; do the clusters match the annotated cell types?
