# Data-Driven-Quantification-of-Quantum-k--Entanglement-via-Machine-Learning
A machine learning framework that rapidly estimates multipartite k-entanglement—bypassing exponential optimization—for real-time quantum analysis.
# Fast ML Surrogates for Multipartite $k$-Entanglement $E_w^{(k,n)}$

## Overview
Quantifying multipartite $k$-entanglement is a central yet computationally demanding task in quantum information. Exact evaluation of $k$-entanglement measures typically requires high-dimensional optimization over subsystem partitions, with computational complexity that grows exponentially with the system size. This makes real-time monitoring, online feedback, and large-scale parameter sweeps impractical for many experimental settings.

This repository provides datasets and pretrained models for a general-purpose machine learning framework that approximates the multipartite $k$-entanglement measure $E_w^{(k,n)}$ proposed in [GYHQH25] by reformulating its computation as a supervised regression problem. The framework integrates MLP, CNN, and LightGBM via a stacking ensemble to combine accuracy and inference efficiency. The released checkpoints enable millisecond-level inference per state, serving as a practical tool for rapid $k$-entanglement quantification and experimental feedback control.

---

## What is released
- **Datasets**: density matrices $\rho_i$ stored in `rho_data.npz` together with corresponding labels $E_w^{(k,n)}(\rho_i)$ stored in `results.csv`.
- **Pretrained models**: trained `.pth` checkpoints for fast inference (per dataset / per setting).

---

## Datasets

### Dataset definition
For each setting, we provide a dataset of the form
\[
\mathcal{D}_{\boldsymbol{\delta}_k} = \{(\rho_i,\; E_w^{(k,n)}(\rho_i))\}_{i=1}^{N},
\qquad N=30000,
\]
with an **80% / 20% split** between the training and test sets.

### Directory naming convention
Each dataset is stored under a directory named as:

- `K_a-b-c-...`

where `a-b-c-...` denotes the local Hilbert space dimensions of the multipartite system, i.e. the setting
\[
\boldsymbol{\delta} = (a, b, c, \ldots).
\]
For example, a directory named `K_2-4-2` corresponds to a tripartite system with local dimensions $(2,4,2)$.

> Note: The value of $k$ (e.g., $k=2,3,4$) is specified in the corresponding dataset directory description / release notes and matches the pretrained checkpoint provided for that dataset.

### Systems covered in this release
The datasets in this repository cover the following settings (local dimensions) and $k$ values used in our experiments:

- $(2,2,2)_{k=2}$, $(2,2,2)_{k=3}$
- $(2,4)_{k=2}$
- $(2,2,2,2)_{k=2}$, $(2,2,2,2)_{k=3}$, $(2,2,2,2)_{k=4}$
- $(2,4,2)_{k=2}$, $(2,4,2)_{k=3}$
- $(2,8)_{k=2}$

### File formats
Each dataset directory contains exactly two files:

- `rho_data.npz`  
  Stores the quantum states $\{\rho_i\}_{i=1}^N$.

- `results.csv`  
  Stores the target labels $\{E_w^{(k,n)}(\rho_i)\}_{i=1}^N$ aligned with the state ordering in `rho_data.npz`.

> Alignment rule: the $i$-th label in `results.csv` corresponds to the $i$-th state $\rho_i$ in `rho_data.npz`.

### Train/test split
All datasets use a fixed **80% / 20%** split between training and test sets. The split is consistent with the ordering (or split metadata) provided together with each dataset.

---

## Pretrained models (`.pth`)

We provide pretrained PyTorch checkpoints for fast inference for the released settings.

### Where to find checkpoints
Pretrained weights are stored under:
- `checkpoints/` (or provided via GitHub Releases, depending on repository setup)

### Naming convention
Each checkpoint name encodes the dataset setting and the corresponding $k$ value, for example:
- K_2-2-2_cnn_quantum_model_1.pth`
- `K_2-2-2_mlp_quantum_model_1.pth`

(Exact filenames may vary; please refer to the directory listing or the release page.)

---

## Intended usage
The released datasets and pretrained weights are intended for:
- fast approximation of multipartite $k$-entanglement $E_w^{(k,n)}$,
- rapid parameter scans and state monitoring,
- experimental feedback control loops where exact optimization is too costly.

---

## Citation
If you use the datasets or pretrained models in this repository, please cite:

```bibtex
@article{GYHQH25,
  title   = {Data-Driven Quantification of Quantum $k$-Entanglement via Machine Learning},
  author  = {Jie Guo, Jinchuan Hou, Xiaofei Qi, and Kan He.},
  journal = {<JOURNAL>},
  year    = {2026},
  volume  = {<VOLUME>},
  number  = {<NUMBER>},
  pages   = {<PAGES>},
  doi     = {<DOI>}
}

\bibitem{GYHQH25} J. Guo, S.-Y. Yan, J.-C. Hou, X.-F. Qi, and K. He, $k$-entanglement measures without convex roof extension and its evaluation, arXiv:2512.12588 [quant-ph].
