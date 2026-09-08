# CPU-Friendly Deepfake Detection

Curricular internship project on facial deepfake detection, focused on building
lightweight, CPU-friendly neural architectures that balance accuracy with low
computational cost (parameter counts in the few-million range, no dedicated
hardware acceleration required for inference).

The work is organized in two phases, each in its own sub-project:

- **[`deepfake-forensics-pipeline/01_Benchmark`](deepfake-forensics-pipeline/01_Benchmark)**
  — first phase of the internship: a baseline benchmark of three lightweight
  architectures (Standard EfficientNet-B0, Hybrid EfficientNet-B0, DeiT-Tiny),
  trained on FaceForensics++ and FEI Morph v2 and evaluated cross-dataset on
  Celeb-DF++.
- **[`deepfake-forensics-pipeline/02_Extended_Framework`](deepfake-forensics-pipeline/02_Extended_Framework)**
  — extended framework developed in the second phase, expanding the model pool
  to six configurations (adding DINOv3 ConvNeXt-S and two Dual-Branch
  CNN+DINOv3 fusion architectures), with a two-step training regime, a
  systematic robustness evaluation under degradation, and an ablation study.
  Unlike the first phase, models here are trained and tested only on Celeb-DF++
  and FEI Morph v2 (no FaceForensics++). This is the codebase underlying the
  final thesis.

## Repository structure

Only Jupyter notebooks (`*.ipynb`) are version-controlled; raw datasets, extracted
frames, and trained model checkpoints are excluded (see `.gitignore`) due to their
size and are not included in this repository.

## Thesis

The `02_Extended_Framework` codebase is the basis for the thesis *"DeepFake
Detection Efficiente: un percorso architetturale incrementale, da CNN
efficienti a modelli ibridi con fusione DINOv3"* ("Efficient DeepFake
Detection: An Incremental Architectural Path, from Efficient CNNs to Hybrid
Models with DINOv3 Fusion"), University of Bologna.

## Author

Lucia Pola — internship carried out at IdentifaAI Labs, Cesena, as part of a
curricular internship for the University of Bologna.
