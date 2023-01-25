# Finetuning Methods

This repo includes an implementation of some recent finetuning methods. Methods include:
- LP-FT
- Surgical Finetuning
- Disciriminitive Finetuning
- Feature Extraction

## LP-FT
LP-FT is a method discussed in the paper [Fine-Tuning can Distort Pretrained Features and Underperform Out-of-Distribution](https://arxiv.org/pdf/2202.10054.pdf) where the authors argue for finetuning the entire network only after having a trained linear probe. This theory follows from the idea that the pre-trained model already has a good feature extractor and we should strive for minimally disturbed extractors after finetuning. We can achieve this by the proposed method.

## Surgical Finetuning
Surgical finetuning methods are region specific finetuning methods. These methods were discussed in the paper [Surgical Fine-Tuning Improves Adaptation to Distribution Shifts](https://arxiv.org/pdf/2210.11466.pdf). These methods were mainly used for domain adaptation. The two implemented methods found in `Finetuning.ipynb` are:
- Layer Specific finetuning
  - This method requires specifying the first and last layer from a list of available layers to finetune.
- AutoRGN
  - Automatically adjust the learning rate for each layer to be finetuned by its relative gradient norm with respect to all layers

## Discriminitive Finetuning
Inspired by [ULMFiT](https://arxiv.org/pdf/1801.06146v5.pdf) and a recent [post](https://towardsdatascience.com/advanced-techniques-for-fine-tuning-transformers-82e4e61e16e) on medium discussing layer specific learning rate decay and warm-up steps, we implement these methods in the `Finetuning.ipynb` notebook. The methods:
- Ramp up the learning rate from 0 to the initial learning rate specified in `n` epochs
- The learning rate is highest for the last layers and drops by %10 for each preceeding layer

## Feature Extraction
In the `Data_Visualization.ipynb` notebook, we use the pre-trained model as a feature extractor and plot the features in a 2D space using [UMAP](https://umap-learn.readthedocs.io/en/latest/index.html). We additionally compute the representation similarity of different resizing methods (using different interpolations) using [Centered Kernel Alignment (CKA)](https://arxiv.org/pdf/1905.00414.pdf).
