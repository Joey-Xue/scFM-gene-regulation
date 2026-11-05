# common

Shared code used by every analysis:

- **reference statistics**: co-variation, the Pearson correlation of log-normalized expression; Rank-PMI, the positive PMI of co-occurrence within a window of *K* positions of each cell's rank-ordered gene list, or within the top-*K* genes of a cell.
- **model similarities**: static embedding, hidden state and attention for gene-token models, and the cosine between gene vectors for VAE, SCimilarity and PCA.
- **alignment**: the Spearman correlation of a model similarity with a reference statistic over gene pairs.
- **figure style**: the shared figure style.

*Code to be added.*
