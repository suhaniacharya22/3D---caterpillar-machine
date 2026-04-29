# 3D Gaussian Splatting — Caterpillar 950F Reconstruction
### STA306 Project | BSc Computer Science | April 2026 | Suhani Acharya

## Project Overview

This project implements **3D Gaussian Splatting (3DGS)** for photorealistic 
reconstruction of a Caterpillar 950F wheel loader — a subject chosen for its 
rich anisotropic spatial correlations (hydraulic arms, tyre treads, flat 
painted panels, structural edges).

Based on: [Kerbl et al., 2023 — 3D Gaussian Splatting for Real-Time Radiance Field Rendering](https://arxiv.org/pdf/2308.04079)

---

## Repository Structure
```
3D---caterpillar-machine/
├── README.md
├── CITATION.cff
├── notebook/
│   └── suhani-acharya-AU2220106-sta306-project.ipynb
├── report/
│   └── Suhani Acharya_AU2220106_Report.pdf
├── results/
│   └── renders/
│       ├── front view (a).png
│       ├── front view (b).png
│       ├── back view (a).png
│       ├── back view (b).png
│       ├── side view (a).png
│       └── side view (b).png
└── colmap_output/
    └── cameras.json
```

## Results

| Metric | Value |
|--------|-------|
| Images Used | 150 |
| COLMAP Registration | 150/150 (100%) |
| Sparse 3D Points | 93,611 |
| Reprojection Error | 0.454 px |
| PSNR @ 7,000 iterations | 27.85 dB |
| PSNR @ 30,000 iterations | **31.53 dB** |
| Training Time | ~1h 27min (2x Tesla T4) |

---

## How to Reproduce

### 1. Dataset
Images available on Kaggle:  
[suhanimanishacharya/caterpillar-images](https://www.kaggle.com/datasets/suhanimanishacharya/caterpillar-images)

### 2. Run the Notebook
Open [Kaggle notebook](https://www.kaggle.com/code/suhanimanishacharya/suhani-acharya-au2220106-sta306-project) in Kaggle with **GPU T4 x2** enabled.  
Run all cells sequentially.

### 3. View the 3D Model
Download `point_cloud.ply` from the Google Drive link below (Full Model) and open in:

[SuperSplat Viewer](https://playcanvas.com/supersplat/editor)

---

## Key Findings on Anisotropic Correlation

| Surface | Anisotropy Type | Captured status|
|---------|----------------|-----------|
| Painted body panels | Planar (flat) | Excellent |
| Rubber tyres | Periodic directional | Excellent |
| Hydraulic arms | Linear (elongated) | Moderate |
| Sky/background | Linear (needle) | Poor |
| Glass windows | Transparent planar | Poor |
| Top View | View-dependent | Poor |

---

## Gaussian Update Strategies

Five novel modifications proposed for better anisotropic capture:

1. **Normal-Guided Covariance Initialisation** — align Gaussian orientation with SfM surface normals before training
2. **Surface-Tangent Spherical Harmonics** — express SH in local Gaussian frame instead of world frame
3. **Anisotropy Regularisation Loss** — penalise pathological aspect ratios in background regions
4. **2D Planar Gaussian Splatting** — replace volumetric Gaussians with surface discs (Chen et al., 2024)
5. **Depth-Consistent Covariance Pruning** — remove geometrically inconsistent Gaussians at specular joints

---

## Environment

- Platform: Kaggle Free Tier (GPU T4 x2)
- PyTorch 2.10.0 + CUDA 12.8
- COLMAP (CPU mode)
- Official 3DGS repo: [graphdeco-inria/gaussian-splatting](https://github.com/graphdeco-inria/gaussian-splatting)

---

## Report

Full technical report (including theory, pipeline, anisotropy analysis, and bonus proposals):

[View Report](#report)

---

## Download Full Model

The complete trained model and outputs (508 MB) are available here:

[Download caterpillar_3dgs.zip (Google Drive)](https://drive.google.com/file/d/1aRzDdof2WZ5cUc73bknu4r1JsjkK8PXf/view?usp=drive_link)

Contents:
- point_cloud/iteration_30000/point_cloud.ply — Best quality model
- point_cloud/iteration_7000/point_cloud.ply
- cameras.json
- cfg_args

## References

- Kerbl et al. (2023). 3D Gaussian Splatting for Real-Time Radiance Field Rendering. *ACM TOG*
- Chen et al. (2024). 2D Gaussian Splatting. *SIGGRAPH 2024*
- Schönberger & Frahm (2016). Structure-from-Motion Revisited. *CVPR 2016*
---
