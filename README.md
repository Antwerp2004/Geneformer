> **Note:** I'm working over an SSH remote connection, so downloading large folders locally can be slow and difficult. I will just upload and update some of the code files where I'm implementing the training and testing on Geneformer.

# Geneformer Project

## Overview

**Geneformer** is a context-aware, attention-based deep learning model pretrained on over **29.9 million** human single-cell transcriptomes (Genecorpus-30M) to enable accurate, data-efficient predictions in network biology. By leveraging a self-supervised **masked learning** objective during pretraining and fine-tuning on limited downstream datasets, Geneformer:  

- Learns fundamental gene network dynamics and context-specific embeddings.  
- Excels at diverse tasks including **cell type annotation**, **gene dosage sensitivity**, **chromatin state prediction**, and **in silico perturbation** for therapeutic target discovery.  
- Demonstrates strong performance on rare diseases and clinically challenging tissues by transferring knowledge from large-scale unlabeled data.

## Key Features

- **Self-Supervised Pretraining**: 15% masked gene prediction across 30M single-cell profiles.  
- **Transfer Learning**: Fine-tune on as few as hundreds of task-specific examples.  
- **Attention Visualization**: Identify network hierarchies and key regulatory genes via model attention weights.  
- **In Silico Perturbation**: Model gene deletion and activation effects on cell and gene embeddings for discovery of candidate therapeutic targets.

## Repository Structure

```
├── anaconda3/                                # Environment
├── geneformer_real/                          # The main folder, updated only when achieved something new
├── geneformer_test/                          # Training, evaluation, and preprocessing scripts
│   ├── data/                                     # Contains datasets
│   ├── Geneformer                                # The model, we can choose different versions (6L-30M means 6 layers, pretrained on 30 million cells)
│   ├── outputs                                   # Contains output data or files
│   ├── wandb                                     # Train and test data using wandb
│   ├── cell_classification.ipynb                 # Train and test Geneformer on different cell datasets
│   ├── gene_classification.ipynb                 # Train and test Geneformer on different gene datasets
│   ├── download_and_prepare_datasets.ipynb       # Train and test Geneformer on different gene datasets
└── README.md                                 # This file
```

> **Note:** I exclude environment folders (e.g. anaconda3/), VS Code settings (e.g. .vscode/), and other hidden config dirs (.ssh/, .ipython/) via .gitignore to keep the repo lightweight.

## Getting Started

This project uses **Anaconda** for environment management and includes a preconfigured `geneformer_env` environment.

1. **Select the kernel in VS Code**
  - Open any Jupyter notebook in the notebooks/ folder.
  - Click the kernel selector (top-right).
  - Choose Python (geneformer_env) as the active interpreter.

2. **Prepare data**  
   - Tokenize raw `.loom` or `.h5ad` files with `tokenize_data.py`.  
   - Use `prepare_data()` to generate labeled `.dataset` for training/testing.

3. **Train & Validate**  
   ```bash
   python geneformer_test/cell_classification.ipynb \
     --input data/cell_type_train_data.dataset \
     -- model data/pancreas_model \
   ```

4. **Evaluate**  
   ```bash
   python scripts/evaluate_model.py \
     --model data/pancreas_model \
     --test data/pancreas_scib_labeled_test.dataset
     --test data/pancreas_scib_filtered.dataset
   ```

## Notes for Recruiters

- This project demonstrates **advanced skills** in:  
  - **Deep Learning**: Transformers, masked modeling, transfer learning.  
  - **Single-Cell Analysis**: Tokenization of transcriptomes, Scanpy & Loom integration.  
  - **Software Engineering**: Python package development, Hugging Face Datasets, reproducible environments.  
  - **Data Visualization**: Embedding and attention weight UMAPs, confusion matrices, performance dashboards.  

- **Impact**: Geneformer’s ability to leverage large unlabeled corpora to boost predictive accuracy on limited data opens avenues in rare disease research, target discovery, and precision cardiology.

---

## Reference

- 🔗 **Original Geneformer Model**: [Hugging Face – ctheodoris/Geneformer](https://huggingface.co/ctheodoris/Geneformer)  
- 📄 **Paper**: *Transfer learning enables predictions in network biology*  
  [Nature (2023)](https://www.nature.com/articles/s41586-023-06139-9.epdf?sharing_token=u_5LUGVkd3A8zR-f73lU59RgN0jAjWel9jnR3ZoTv0N2UB4yyXENUK50s6uqjXH69sDxh4Z3J4plYCKlVME-W2WSuRiS96vx6t5ex2-krVDS46JkoVvAvJyWtYXIyj74pDWn_DutZq1oAlDaxfvBpUfSKDdBPJ8SKlTId8uT47M%3D)

_Repository maintained by Đỗ Hoàng Quân, Research Student in BioTuring._

