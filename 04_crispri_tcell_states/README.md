# 04_crispri_tcell_states

Whether model similarities follow CRISPRi effects in primary CD4⁺ T cells: genome-wide CRISPRi Perturb-seq, at rest and 8 h and 48 h after stimulation.

- **extraction**: Geneformer V2-104M and scGPT hidden states and attention from non-targeting control cells of each state; co-variation and Rank-PMI (K = 1,000) of the same cells.
- **within one state**: the correlation of the size of the CRISPRi effect with each relation.
- **across states**: changes between states, after removing gene-wide changes.
  - Changes in model similarity are related to changes in co-occurrence and in co-variation.
  - Changes in each relation are related to changes in the CRISPRi effect.
  - Confidence intervals come from bootstrap resamples of knocked-down genes.

*Code to be added.*
