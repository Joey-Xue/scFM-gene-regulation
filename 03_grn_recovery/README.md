# 03_grn_recovery

Whether gene-pair scores recover known regulatory edges.

- **simulated GRN**: AUROC over TF → gene candidate pairs, for statistics and for models trained from scratch. Two series:
  - the training series;
  - the corpus-size series, with three model sizes, two objectives and three seeds.

  Also an enrichment analysis of the false positives for high Rank-PMI.
- **U2OS ChIP-seq**: per-TF AUROC against the BEELINE non-specific ChIP-seq network on a common gene set, for these scores:
  - the released scFMs (Geneformer V2, scGPT, SCimilarity), zero-shot and fine-tuned on U2OS cells;
  - models trained from scratch on U2OS cells;
  - PCA, co-variation and Rank-PMI of the U2OS cells and of 100,000 scTab cells.

  Paired Wilcoxon tests over TFs.
- **co-occurrence window and residual analyses**: Rank-PMI at several windows, including the 2,048-gene Geneformer sentence, and model similarity after regressing out corpus co-occurrence and co-variation.
- **supervised probe**: an XGBoost predictor of ChIP-Atlas binding scores from two genes' vectors, on random, held-out-TF and held-out-target splits.

*Code to be added.*
