# 02_training_dynamics

Which relation a model's gene–gene similarity follows during training.

- **rank-only transformer**: reads each cell as its genes sorted by decreasing count; masked gene-token objective, with a next-gene-token variant.
- **value-aware transformer**: the same transformer stack in a fixed gene order, with expression read through the scGPT value encoder (50 bins) and a masked value objective.
- **variational autoencoder**: gene similarity is the cosine between decoder rows.
- **alignment over training**: the alignment of the static embedding, hidden state and attention with Rank-PMI and with co-variation, at checkpoints over training, on the simulated corpora, the ablated corpora and U2OS cells.

*Code to be added.*
