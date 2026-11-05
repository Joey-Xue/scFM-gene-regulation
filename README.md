# scFM-gene-regulation

Code for **"Cells are not sentences: current cell sentence tokenization in single cell foundation model can’t capture gene regulation"**
(Zhengyuan Xue, Weixu Wang, Francesco Paolo Casale, Fabian J. Theis and Daniel Kotlarz).

> **Status:** the repository structure is in place and the analysis code is being cleaned up. Code will be added folder by folder; until then each folder's README describes what it will contain.

## Question

Single-cell foundation models (scFMs) such as Geneformer write each cell as a sequence of gene tokens, often ordered by expression rank. We ask which relation between two genes such a model learns, and whether that relation carries regulatory information. We distinguish two relations computed from the same cells:

- **co-variation**: the Pearson correlation of two genes' log-normalized expression across cells. Gene regulation produces co-variation.
- **co-occurrence**: how often two genes sit close to each other in the cells' rank-ordered gene lists, scored as **Rank-PMI**. This is the positive pointwise mutual information of co-occurrence within a window of *K* positions.

Two genes can sit far apart in every ranked list and still co-vary. Two genes of similar abundance can co-occur without any regulatory link.

A model's gene–gene relation is measured as a **model similarity** from one of three representations:

- **static embedding**: the cosine between rows of the input embedding table;
- **hidden state**: the cosine between final-layer outputs, averaged over cells;
- **attention**: the attention weight between two gene tokens.

Models without gene tokens, such as a VAE, SCimilarity or PCA, give one vector per gene and are compared by the cosine between these vectors.

## Study design

| Step | Question | Data | What is measured | Folder |
|---|---|---|---|---|
| 1 | Which relation does a model's similarity follow during training? | dyngen simulation with a known GRN, U2OS cell cycle | Spearman alignment of model similarity with Rank-PMI and with co-variation over training; data-structure ablations | `02_training_dynamics/` |
| 2 | Do model similarities recover known regulatory edges? | dyngen GRN; U2OS cells with the BEELINE ChIP-seq network; scTab and Genecorpus-30M statistics | AUROC per TF against the reference network; supervised probe on held-out TFs and targets | `03_grn_recovery/` |
| 3 | Do model similarities follow CRISPRi effects within and across T-cell states? | genome-wide CRISPRi Perturb-seq of primary CD4⁺ T cells at rest, 8 h and 48 h after stimulation | correlations of CRISPRi effects, and of their changes between states, with model similarity, co-variation and co-occurrence | `04_crispri_tcell_states/` |
| 4 | Do scFM representations help predict perturbation responses? | a published CD4⁺ T-cell perturbation-response benchmark; CRISPRi screens in K562, RPE1, Jurkat and HepG2 | gain in cosine similarity of predicted responses over the benchmark's mean baseline, across four predictors | `05_perturbation_prediction/` |

Models compared:

- **from scratch**:
  - rank-only transformers, which read genes ordered by expression, trained with masked or next-gene-token objectives at three model sizes;
  - a value-aware transformer, which reads expression values through the scGPT value encoder;
  - a variational autoencoder.
- **released**: Geneformer V2, scGPT whole-human and SCimilarity v1.1, zero-shot and fine-tuned on U2OS cells.
- **baselines**: co-variation, Rank-PMI and PCA of the same cells and of a 100,000-cell scTab panel.

## Repository layout

```
common/                      shared code: Rank-PMI, co-variation, model similarities, alignment, plotting style
01_simulation/               dyngen simulations, nested corpora (10k–100k cells), data-structure ablations
02_training_dynamics/        rank-only and value-aware transformers and VAE; alignment over training
03_grn_recovery/             GRN and ChIP-seq recovery: simulated GRN, U2OS cells, released scFMs, supervised probe
04_crispri_tcell_states/     CD4⁺ T-cell Perturb-seq: model similarity extraction, within-state and across-state analyses
05_perturbation_prediction/  benchmark reproduction and prediction of 48 h responses from rest and 8 h representations
figures/                     scripts that assemble the main and supplementary figures from the outputs above
data/                        download instructions for every external dataset (no data are stored here)
envs/                        conda environment files
```

## Data

All datasets are public. Download instructions will be in [`data/README.md`](data/README.md).

- CD4⁺ T-cell CRISPRi Perturb-seq: Zhu et al. 2026, GEO [GSE314342](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE314342).
- U2OS cell cycle: Mahdessian et al. 2021, GEO [GSE146773](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE146773).
- scTab corpus and partitions: Fischer et al. 2024; DenAdel et al. 2026, [Zenodo 19173545](https://doi.org/10.5281/zenodo.19173545).
- Genecorpus-30M: Theodoris et al. 2023, [Hugging Face](https://huggingface.co/datasets/ctheodoris/Genecorpus-30M).
- K562 and RPE1 Perturb-seq: Replogle et al. 2022, [Zenodo 7041849](https://doi.org/10.5281/zenodo.7041849).
- Jurkat and HepG2 Perturb-seq: Nadig et al. 2025, GEO [GSE264667](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE264667).
- BEELINE reference networks: Pratapa et al. 2020, [Zenodo 3701939](https://doi.org/10.5281/zenodo.3701939).
- ChIP-Atlas target-gene scores: [chip-atlas.org](https://chip-atlas.org).
- Perturbation-response benchmark and external knowledge features: Palla et al. 2026, [royerlab/tfm-perturbation](https://github.com/royerlab/tfm-perturbation) and [Zenodo 15587986](https://doi.org/10.5281/zenodo.15587986).

The simulated data and derived matrices will be deposited in a public repository on publication.

## Software

We used the following models and tools:

- Geneformer: [Hugging Face](https://huggingface.co/ctheodoris/Geneformer).
- scGPT: [bowang-lab/scGPT](https://github.com/bowang-lab/scGPT), release 0.2.4.
- SCimilarity: [Genentech/scimilarity](https://github.com/Genentech/scimilarity), model v1.1.
- scvi-tools 1.1.2.
- CatBoost 1.2.10, TabICL 2.0.1 and TabPFN 9.0.0.
- dyngen 1.1.1 (R).

Environment files will be in `envs/`.

## Citation

The citation will be added on publication.

## License

[MIT](LICENSE)
