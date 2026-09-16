# Predictor vs Predictor-Corrector Sampling for Score-Based SDEs

This project investigates **score-based generative modeling using Stochastic Differential Equations (SDEs)** on the MNIST dataset.

The main objective is to compare two reverse-time sampling methods:

* **Predictor-only sampling**
* **Predictor-Corrector (PC) sampling**

A **Variance-Exploding (VE) SDE** and a **time-conditioned U-Net** are used to learn the score function and generate MNIST images.

## Research Question

**Can Predictor-Corrector sampling improve generated image quality compared with Predictor-only sampling, and what is the computational cost?**

## Methodology

```text
MNIST Images
     ↓
Forward VE-SDE (Add Noise)
     ↓
Time-Conditioned U-Net
     ↓
Learn Score Function
     ↓
Reverse-Time Sampling
     ├── Predictor
     └── Predictor-Corrector
     ↓
Generated Images
     ↓
Evaluation
```

## Experimental Setup

* **Dataset:** MNIST
* **Model:** Time-Conditioned U-Net
* **SDE:** Variance-Exploding (VE-SDE)
* **Sampling Steps:** 50, 100, 250, 500, 1000
* **Predictor-Corrector:** Langevin Corrector
* **Framework:** PyTorch
* **Environment:** Google Colab

## Results

| Method    |   Steps |       FID ↓ |
| --------- | ------: | ----------: |
| Predictor |      50 |     48.1189 |
| Predictor |     250 |     45.1138 |
| PC        |      50 |     40.4739 |
| **PC**    | **250** | **35.8669** |

The **Predictor-Corrector sampler achieved lower FID scores** in the reported experiments, but required higher computational cost due to additional score-network evaluations.

## Key Finding

The results show an important trade-off:

> **Better sample quality can require higher computational cost.**

Increasing the number of sampling steps also did not always improve the generated results.

## Repository Structure

```text
├── notebooks/       # Google Colab notebooks
├── results/         # Generated samples and results
├── paper/           # Project paper
├── README.md
└── requirements.txt
```

## Reference

Song, Y., et al. (2021). **Score-Based Generative Modeling through Stochastic Differential Equations.** ICLR 2021.

## Authors

**Sumaiya Azad Isha**
**Tasnia Mahjabin Maliha**

Department of Computer Science and Engineering
BRAC University
