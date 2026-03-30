# Stable Prototypical Networks for Hyperspectral Few-Shot Classification

This repository contains our end-to-end major project work on few-shot hyperspectral image classification using Stable Prototypical Networks (SPN), including baseline implementations, architecture trials, ablation studies, and experiment reports.

The work is organized in two phases:

- Batch 2023: baseline SPN implementation, original study artifacts, and supporting documents.
- Batch 2024: improved experimentation pipeline, encoder variants, tuning/testing notebooks, and large ablation outputs.

## What This Project Solves

Hyperspectral image (HSI) classification typically requires many labeled samples, which are expensive to collect. This project studies how SPN-style few-shot learning can improve classification when only a small number of labeled examples per class are available.

Core ideas explored in this repository:

- Episodic training for N-way K-shot classification.
- Stable embedding learning with SPN-style regularization ideas.
- Temperature scaling (`tau`) analysis.
- Encoder variants with and without self-attention.
- Ablation studies across train/tune epoch schedules and shot settings.

## Repository Layout

- [Major Project Batch 2023](Major%20Project%20Batch%202023/)
- [Major Project Batch 2024](Major%20Project%20Batch%202024/)

Important subfolders:

- [Major Project Batch 2023/Code/SPN-main](Major%20Project%20Batch%202023/Code/SPN-main/): original SPN reference implementation and paper-linked README.
- [Major Project Batch 2023/Dataset](Major%20Project%20Batch%202023/Dataset/): benchmark HSI `.mat` datasets used in early phase experiments.
- [Major Project Batch 2024/encoders](Major%20Project%20Batch%202024/encoders/): encoder architecture variants (`conv_gan`, `conv_sa`, `conv_no_sa`, etc.).
- [Major Project Batch 2024/lib](Major%20Project%20Batch%202024/lib/): reusable training, data, prediction, and metrics utilities.
- [Major Project Batch 2024/ablation](Major%20Project%20Batch%202024/ablation/), [ablation_fresh](Major%20Project%20Batch%202024/ablation_fresh/), [ablation_review](Major%20Project%20Batch%202024/ablation_review/): experiment sweeps and organized outputs.
- [Major Project Batch 2024/Reports](Major%20Project%20Batch%202024/Reports/): timestamped evaluation reports (accuracy, kappa, per-class metrics).

## Main Notebooks (Batch 2024)

- [SPN_5Shot_MT.ipynb](Major%20Project%20Batch%202024/SPN_5Shot_MT.ipynb): multi-train workflow.
- [SPN_5Shot_Tune.ipynb](Major%20Project%20Batch%202024/SPN_5Shot_Tune.ipynb): training plus tuning workflow.
- [SPN_5Shot_TEST.ipynb](Major%20Project%20Batch%202024/SPN_5Shot_TEST.ipynb): testing/evaluation-focused run.
- [SPN_5Shot_TAU.ipynb](Major%20Project%20Batch%202024/SPN_5Shot_TAU.ipynb): temperature (`tau`) sensitivity experiments.
- [SPN_5Shot_OG.ipynb](Major%20Project%20Batch%202024/SPN_5Shot_OG.ipynb): baseline comparison notebook.

## Typical Experiment Flow

1. Load and preprocess HSI dataset (`.mat`) with PCA and patch extraction.
2. Select encoder variant from [encoders](Major%20Project%20Batch%202024/encoders/).
3. Run episodic training (few-shot episodes).
4. Run tuning/fine-tuning for target classes (if enabled).
5. Evaluate on test episodes and generate reports.

Common hyperparameter knobs in notebooks:

- Patch/window size
- PCA components
- Train/tune/test way-shot-query configuration
- Train/tune/test epochs
- Learning rate
- Temperature scaling (`tau`)

## Quick Start

### 1) Create environment

Recommended: Python 3.10 with TensorFlow 2.10 (as used in the notebooks).

```bash
cd "Major Project Batch 2024"
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

### 2) Launch Jupyter

```bash
jupyter notebook
```

Open one of:

- `SPN_5Shot_MT.ipynb`
- `SPN_5Shot_Tune.ipynb`
- `SPN_5Shot_TEST.ipynb`
- `SPN_5Shot_TAU.ipynb`

### 3) Configure data paths and settings

Inside the selected notebook, verify:

- Dataset file locations (`.mat` files)
- Encoder choice import
- Train/tune/test configuration values
- Save flags for model and report artifacts

## Datasets

This work uses standard hyperspectral benchmarks such as:

- Indian Pines
- Salinas / SalinasA
- Pavia University (in experiment configurations)
- Houston (as referenced by SPN baseline materials)

Public dataset sources referenced by the baseline SPN repository:

- http://www.ehu.eus/ccwintco/index.php/Hyperspectral_Remote_Sensing_Scenes
- https://hyperspectral.ee.uh.edu/?page_id=459

If you do not store datasets in the same local paths used during development, update notebook path variables before execution.

## Example Outputs

Generated artifacts include:

- Overall Accuracy (OA), Average Accuracy (AA), and Kappa score
- Per-class precision/recall/F1 classification reports
- Confusion matrices
- Optional saved model checkpoints
- Timestamped text reports in [Major Project Batch 2024/Reports](Major%20Project%20Batch%202024/Reports/)

## Reproducibility Notes

- Notebooks contain the canonical experiment logic used in this project.
- Many experiments are configured through top-level notebook variables.
- To compare encoder variants fairly, keep data split and episode settings fixed.
- Ablation folders contain runs with different epoch schedules and train/tune settings.

## Project Background

This repository consolidates academic major project work from two consecutive batches:

- Baseline and foundational work from Batch 2023
- Extended experimentation and ablation-focused work from Batch 2024

Original SPN reference implementation and paper context are available in:

- [Major Project Batch 2023/Code/SPN-main](Major%20Project%20Batch%202023/Code/SPN-main/)

## Citation

If you use the SPN baseline ideas/code, cite the original paper:

```bibtex
@ARTICLE{9455864,
  author  = {Pal, Debabrata and Bundele, Valay and Banerjee, Biplab and Jeppu, Yogananda},
  journal = {IEEE Geoscience and Remote Sensing Letters},
  title   = {SPN: Stable Prototypical Network for Few-Shot Learning-Based Hyperspectral Image Classification},
  year    = {2022},
  volume  = {19},
  pages   = {1-5},
  doi     = {10.1109/LGRS.2021.3085522}
}
```

## License and Academic Use

This repository is currently intended for academic/research use.

Before public redistribution, verify:

- Dataset redistribution permissions
- Third-party code licensing compatibility
- Report/document sharing constraints

---

If you want, I can also create:

- A polished `.gitignore` at repository root.
- A `CONTRIBUTING.md` for collaborators.
- A shorter one-page README variant optimized for recruiters and portfolio viewing.
