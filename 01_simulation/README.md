# 01_simulation

Simulated single-cell data with a known GRN:

- **dyngen simulation**: a bifurcating backbone with 31 TFs, 264 target genes and 100 housekeeping genes, 100,000 cells (R, dyngen 1.1.1).
- **nested corpora**: 10,000, 25,000, 50,000 and 100,000 cells, drawn by stratified sampling so that each smaller corpus is contained in each larger one, with training and validation splits.
- **data-structure ablations** of the 10,000-cell corpus:
  - each gene permuted across cells, which removes co-variation and keeps abundance-driven co-occurrence;
  - counts dequantized and replaced per gene by a rank-inverse-normal transform, which gives every gene the same distribution across cells: abundance-driven co-occurrence disappears and co-variation is kept.
- **simulations with more branch modifications**, used to test whether the difference between the two relations depends on trajectory complexity.

*Code to be added.*
