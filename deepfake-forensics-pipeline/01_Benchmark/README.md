# 01_Benchmark — Initial Architecture Benchmark

First phase of the internship: a baseline comparison of three lightweight,
CPU-friendly architectures for facial deepfake detection.

## Models

- **Standard EfficientNet-B0** — plain CNN classification head.
- **Hybrid EfficientNet-B0** — EfficientNet-B0 backbone with a self-attention
  gating module added on top of the convolutional features.
- **DeiT-Tiny** — Vision Transformer variant (`deit_tiny_patch16_224`), included
  to compare a convolutional and an attention-based paradigm at a comparable
  parameter budget.

## Data protocol

- **Training:** FaceForensics++ (FF++) combined with FEI Morph v2.
- **Testing:** Celeb-DF++, used as a held-out dataset to evaluate cross-dataset
  generalization rather than in-distribution performance.

## Structure

```
Model_Benchmark/
├── step1_baseline.ipynb   # workspace/dataset setup, sanity checks, path remapping
├── step2_retrain.ipynb    # dataset augmentation, model definitions, training
└── step3_test.ipynb       # evaluation on the Celeb-DF++ test set
```

## Notes

This benchmark was the starting point for the internship. The models, dataset
protocol, and evaluation were later substantially extended — six model
configurations, a two-step training regime, degradation-robustness testing, and
an ablation study — in
[`02_Extended_Framework`](../02_Extended_Framework), which is the codebase the
final thesis is based on.

Only Jupyter notebooks are version-controlled here; the raw datasets and trained
weights are not included in this repository.
