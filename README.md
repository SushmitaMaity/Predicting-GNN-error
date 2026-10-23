# Reliability of GNN property predictors under compositional distribution shift

I study how GNN property predictors fail under compositional distribution shift. I trained a graph attention network on heteroatom-rich molecules and tested it on heteroatom-poor ones (ESOL, FreeSolv, Lipophilicity), then profiled per-molecule errors with corrected statistics and a cross-validated meta-model. In every model I fit, error was higher for molecules with fewer heteroatoms (weakly in one case) and for molecules with more extreme property values, and structural novelty mattered in most fits; associations with TPSA and LogP depended on the model and dataset. A graph-only ablation showed no detectable RMSE difference from the descriptor-augmented model. A workshop submission drew detailed reviewer feedback and I'm revising it; I'm also extending the work to explanation faithfulness.

## Status
Research code and working notebooks, not a cleaned pipeline. The work was submitted to the NeurIPS 2026 AI4DD workshop and is being revised after reviewer feedback. Results are exploratory.

## What's here
- Notebooks for ESOL, Lipophilicity and FreeSolv, each with random, scaffold and heteroatom-based splits
- A hybrid GAT (five global RDKit descriptors: LogP, MW, TPSA, HBD, HBA), a graph-only ablation, and GCN and AttentiveFP comparisons
- Per-molecule error analysis: Mann-Whitney tests, OLS with nearest-neighbour novelty controls, Bonferroni and Benjamini-Hochberg correction, and a cross-validated random-forest meta-model with SHAP
- GCN and AttentiveFP comparisons (ESOL, scaffold split only)
- GNNExplainer faithfulness analysis (in progress)

## The compositional split
Training uses molecules with more than 2 heteroatoms; testing uses molecules with 2 or fewer. Some notebooks call it "LoHi". It is unrelated to the Lo-Hi benchmark of Steshin (2023).

## Findings so far
- Relative to a random split, RMSE rose for ESOL and FreeSolv and fell for Lipophilicity. Test sets differ across splits, so these RMSEs are not like-for-like.
- In ESOL and FreeSolv, fewer heteroatoms and more extreme property values were associated with higher error in both model variants. TPSA and LogP associations varied by model and dataset.
- A graph-only ablation (seeds 42-44) showed no detectable RMSE benefit from the descriptors.
- Faithfulness showed no significant correlation with prediction error after correction.

## Limitations
- Seed-to-seed and run-to-run variability is substantial, especially for FreeSolv; GPU runs are not bitwise reproducible.
- The analyzed descriptors overlap with model inputs, so some associations may reflect descriptor-space extrapolation.
- The compositional-split analyses use one architecture family (a GAT with and without descriptor inputs); GCN and AttentiveFP were run only on ESOL with the scaffold split.
- Mostly one architecture; three small benchmark datasets; p-values are uncorrected in some robustness checks.

## Running
Notebooks were run on Google Colab (PyTorch Geometric, RDKit, DeepChem, scikit-learn, statsmodels, SHAP).

## Notebook guide
- [Esol_experiments.ipynb](https://github.com/SushmitaMaity/Predicting-GNN-error/blob/main/Esol_experiments.ipynb): compositional-split analyses (sections 1-3), hybrid vs graph-only ablation (section 2), faithfulness (section 4)
- [ESOL_GCN+AttentiveFp_ScaffoldSplit.ipynb](https://github.com/SushmitaMaity/Predicting-GNN-error/blob/main/ESOL_GCN%2BAttentiveFp_ScaffoldSplit.ipynb): GCN and AttentiveFP comparisons (ESOL, scaffold split only).
- [Freesolv_experiments.ipynb](https://github.com/SushmitaMaity/Predicting-GNN-error/blob/main/Freesolv_experiments.ipynb): same structure.
- [Lipophilicity_experiments.ipynb](https://github.com/SushmitaMaity/Predicting-GNN-error/blob/main/Lipophilicity_experiments.ipynb): same structure.

