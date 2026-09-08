# 02_Extended_Framework — Extended Deepfake Detection Pipeline

Extended framework developed in the second phase of the internship, and the
codebase underlying the final thesis. It expands the initial benchmark
(see [`01_Benchmark`](../01_Benchmark)) to six model configurations, a two-step
training regime, a systematic robustness evaluation under degradation, and an
ablation study isolating the contribution of each architectural component.
Unlike the first phase, models here are trained and tested only on Celeb-DF++
and FEI Morph v2 (no FaceForensics++).

## Models

| # | Model | Description |
|---|-------|-------------|
| 1 | Standard EfficientNet-B0 | CNN backbone, plain classification head |
| 2 | Hybrid EfficientNet-B0 | CNN backbone + self-attention gating module |
| 3 | DeiT-Tiny | Vision Transformer (`deit_tiny_patch16_224`), non-distilled |
| 4 | DINOv3 ConvNeXt-S | Frozen DINOv3 ConvNeXt-S backbone |
| 5 | Dual-Branch Standard | Standard EfficientNet-B0 branch fused with a frozen DINOv3 ViT-Small branch via cross-attention |
| 6 | Dual-Branch Hybrid | Hybrid EfficientNet-B0 branch fused with a frozen DINOv3 ViT-Small branch via cross-attention |

## Data

- **Datasets:** Celeb-DF++ and FEI Morph v2, merged into a single master
  dataset with an identity-disjoint train/val/test split (no identity leakage
  across splits).
- **Face detection & preprocessing:** SSD-based face detector, with a
  center-crop fallback for frames where no face is confidently detected.

## Training

Each model is trained in two steps:

- **Step 1** — training on clean (non-degraded) data.
- **Step 2** — fine-tuning with advanced, degradation-aware augmentation
  (downscaling, JPEG recompression), to improve robustness to the kind of
  degradation typical of real-world image/video sharing.

## Evaluation

- Confusion matrices, ROC/AUC on the clean test set.
- Robustness test under controlled degradation (random downscale + repeated
  JPEG recompression).
- CPU vs GPU inference benchmark across all six models.
- Disaggregated evaluation by data source (FEI vs Celeb-DF++).
- Ablation studies isolating the effect of the self-attention gating module,
  the DINOv3 fusion branch, and the Step 2 augmentation.

## Structure

```
Datasets/                       # dataset exploration, split & preprocessing notebooks
Model_Benchmark/
├── CNN_ViT_Hybrid/              # Standard/Hybrid EfficientNet-B0 + DeiT-Tiny
├── DINOv3_ConvNeXt/             # DINOv3 ConvNeXt-S
├── DualBranch/                  # Dual-Branch Standard/Hybrid
├── Robustness_Test/             # degradation-based robustness evaluation
├── all_models_cpu_gpu_benchmark.ipynb
└── fei_vs_celeb_disaggregated_all_models.ipynb
deepfake_models_final/          # trained model checkpoints (not tracked in git)
```

Each model directory follows the same `step1_baseline` → `step2_retrain` →
`step3_test` structure used in `01_Benchmark`.

## Notes

Only Jupyter notebooks are version-controlled; raw datasets, extracted frames,
and trained model checkpoints are excluded from this repository due to their
size.

This codebase is the basis for the thesis *"DeepFake Detection Efficiente: un
percorso architetturale incrementale, da CNN efficienti a modelli ibridi con
fusione DINOv3"* ("Efficient DeepFake Detection: An Incremental Architectural
Path, from Efficient CNNs to Hybrid Models with DINOv3 Fusion"), University of
Bologna.
