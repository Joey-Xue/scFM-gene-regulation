# 05_perturbation_prediction

Whether scFM representations improve the prediction of perturbation responses.

- **reproduction** of the published benchmark (Palla et al. 2026, [royerlab/tfm-perturbation](https://github.com/royerlab/tfm-perturbation)) on its data and frozen splits.
- **prediction across states**: responses 48 h after stimulation are predicted from representations of the perturbed gene measured in non-targeting cells at rest and 8 h after stimulation. Each candidate representation is the predictor's only input, and its gain is measured over the benchmark's mean baseline. The candidates are:
  - static embeddings, hidden states and attention of scFMs;
  - the benchmark's external knowledge features;
  - CRISPRi responses of the same gene in other cell lines, raw or encoded with PCA, scVI, Geneformer or scGPT.
- **predictors**: CatBoost, HistGradientBoosting, TabICL and TabPFN.

*Code to be added.*
