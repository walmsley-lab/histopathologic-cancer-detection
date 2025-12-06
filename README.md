# Histopathologic Cancer Detection

This repository contains a deep learning project for binary classification of
histopathologic image patches (tumor vs. healthy tissue) using convolutional
neural networks. The work was developed and evaluated using the
PCam (PatchCamelyon) dataset and executed primarily in a Kaggle environment.

## Problem Overview

The task is to classify small histopathologic image patches as either containing
tumor tissue or healthy tissue. This is a supervised computer vision problem that
requires extracting meaningful spatial features from high-resolution medical
images while handling class imbalance and subtle visual differences.

## Repository Structure

histopathologic-cancer-detection/
├── notebook/ # Kaggle-compatible experiment notebook
├── results/
│ ├── model_comparison.csv # Aggregated evaluation results
│ ├── plots/ # Saved EDA and performance figures
│ └── summary.md # Short experiment summary
├── models/ # Trained model checkpoints (.pth)
├── README.md
└── requirements.txt

ruby
Copy code

## Models Evaluated

Multiple architectures were implemented and compared:

- **SimpleCNN** – baseline convolutional network
- **ImprovedCNN** – deeper CNN with batch normalization and dropout
- **MultiScaleCNN** – parallel multi-kernel architecture for spatial scale analysis
- **Pretrained ResNet18** – transfer learning from ImageNet

Balanced batch sampling, weighted loss functions, early stopping, and data
augmentation were applied across all models.

## Key Results

| Model        | Best Validation AUC | Validation Accuracy | Average Precision | Epochs |
|:-------------|:--------------------|:--------------------|:------------------|:--------|
| Pretrained (ResNet18) | 0.9076 | 0.8400 | 0.8770 | 3 |
| ImprovedCNN | 0.8958 | 0.7715 | 0.8480 | 3 |
| MultiScaleCNN | 0.8854 | 0.8065 | 0.8428 | 3 |
| SimpleCNN | 0.8230 | 0.7330 | 0.7132 | 3 |

The pretrained ResNet18 model achieved the best overall discrimination
performance, while the custom CNN variants demonstrated competitive accuracy
with significantly reduced training time.

## Results and Visualizations

All plots and evaluation artifacts generated during training are saved under results/plots/ with samples given in results/benchmark_plots.

These include:
- ROC curves
- Precision–Recall curves
- Loss and AUC training trajectories
- Exploratory data analysis figures

## How to Run

The primary workflow is designed to run inside Kaggle.

1. Upload the repository notebook to Kaggle
2. Attach the PCam dataset
3. Run all cells sequentially
4. Download outputs from `/kaggle/working/results`

Local execution is also possible with a compatible GPU setup.

## Notes

- All evaluation metrics are computed on a held-out validation split
- Early stopping was used to prevent overfitting
- Training time was intentionally minimized to allow rapid iteration