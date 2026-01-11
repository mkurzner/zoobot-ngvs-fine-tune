# ZooBot Fine-Tuning on NGVS Morphology Labels (Curated Evaluation Example)
This repository contains a curated example of transfer learning and model evaluation using a pretrained ZooBot convolutional neural network (CNN) applied to galaxy cutouts from the Next Generation Virgo Cluster Survey (NGVS).

The goal of this project is to demonstrate an empirical evaluation workflow for image classifiers operating under:

- Domain shift between pretraining and target data
- Limited and noisy supervision, and
- Heterogeneous real-world image quality.

Emphasis is placed on failure-mode discovery, subgroup behavior, and confidence-aware diagnostics, rather than on optimizing benchmark performance.

## What is included
This repository demonstrates the following components of the workflow:

- Building a ZooBot-compatible `catalog` (`id_str`, `file_loc`, label columns)
- Fine-tuning a pretrained CNN under domain shift and heterogeneous image quality
- Saving probabilistic predictions for reproducible downstream analysis
- Qualitative failure inspection, including:
   - High-confidence errors
   - Top-confidence predictions (as a sanity check)
   - Low-confidence and decision-boundary cases
   - Subgroup slicing by morphological class

All evaluation figures and tables are generated from committed prediction artifacts to ensure reproducibility.   

## Repository Contents
- `notebooks/ZooBotNGVS_Curated_Example.ipynb` — main workflow (end-to-end)
- `outputs/figures/` — curated qualitative inspection figures
- `outputs/tables/` — saved prediction CSV and lightweight quantitative summary

Training and inference are not re-run in this notebook; however, a sketch of the training workflow is included for transparency

## How I ran this notebook
1. Created an environment with PyTorch + ZooBot dependencies.
2. In the notebook, set:
   - `DATA_DIR` (image directory)
   - `CATALOG_CSV` (metadata + labels)
   - `CHECKPOINT_LOC` (pretrained ZooBot checkpoint)
3. Run cells top-to-bottom. Predictions will be written to:
   - `outputs/finetuned_predictions.csv`
   - `outputs/figures/top_confidence.png`
   - `outputs/figures/bottom_confidence.png`

## Notes
- Image data are not included in this repository. 
- This is research code intended to highlight transparent evaluation and failure analysis rather than production deployment.

## Why this matters for AI safety
Although this project was conducted in an astronomical setting, the evaluation challenges closely mirror those faced in real-world ML deployments, e.g., limited labels, dataset shift, and the risk of confident but incorrect predictions. The diagnostic techniques demonstrated here are directly applicable to safety-critical ML systems where subgroup failures and miscalibration can lead to harmful downstream decisions.
