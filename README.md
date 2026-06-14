# Molecular GNN Error Analysis Study

An investigation into the chemical drivers of prediction error in Graph Neural Networks using the ESOL dataset.

## 🔬 Overview
This repository provides a systematic characterization of structural predictors of GNN prediction error under distribution shift. We focus on the difference between random and scaffold splits to understand how structural novelty and molecular descriptors (MW, LogP, TPSA) influence the reliability of log-solubility predictions.

## 🛠️ Features
- **Hybrid GAT Model**: Combines graph-level features with atomic-scale attention.
- **Scaffold Novelty Metric**: Implements Tanimoto Nearest Neighbor distance to quantify out-of-distribution molecules.
- **Statistical Validation**: Multivariate regression and Mann-Whitney U testing to isolate structural predictors of error.
