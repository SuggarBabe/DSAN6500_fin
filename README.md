# Robust Drivable Road Segmentation under Image Degradation

This repository contains a computer vision project on road segmentation under degraded image conditions.

The goal is to evaluate how different models perform when input images are affected by real-world factors such as blur, noise, brightness changes, and compression artifacts.

---

## Dataset

This project uses the **KITTI Road Benchmark** dataset.

Download from:

https://www.cvlibs.net/datasets/kitti/eval_road.php

The dataset is not included in this repository due to size.

After downloading, place the data as:

```
data/
├── training/
│   ├── image_2/
│   └── gt_image_2/
└── testing/
    └── image_2/
```

---

## Methods

The project compares three approaches:

* Classical baseline (Canny edge + morphology)
* U-Net (CNN-based segmentation)
* Vision Transformer (ViT-based segmentation)

---

## Results

| Model     | Dice Score |
| --------- | ---------- |
| Classical | 0.1883     |
| U-Net     | ~0.75      |
| ViT       | **0.9217** |

Key observations:

* Classical methods fail due to lack of semantic understanding
* U-Net improves segmentation quality significantly
* ViT achieves the best performance by capturing global context

---

## Repository Structure

```

DSAN6500_FIN/
├── README.md
├── final.md
├── check-in-1.md
├── check-in-2.md
├── check-in-3.md

├── notebooks/
│   ├── eda.ipynb
│   ├── baseline.ipynb
│   ├── unet.ipynb
│   ├── vit_segmentation.ipynb
│   └── robustness.ipynb

├── results/
│   ├── threshold_sweep.csv
│   └── figures/
│       ├── qualitative_examples.png
│       └── failure_cases.png

└── data/
    └── KITTI dataset (not included)
    
```

---

## Run Instructions

Install dependencies:

```
pip install -r requirements.txt
```

Run notebooks:

```
jupyter notebook notebooks/eda.ipynb
jupyter notebook notebooks/baseline.ipynb
jupyter notebook notebooks/unet.ipynb
jupyter notebook notebooks/vit_segmentation.ipynb
jupyter notebook notebooks/robustness.ipynb
```

---

## Results Artifacts

Qualitative outputs and failure cases are stored in:

```
results/figures/
```

---

## Project Reports

* `check-in-1.md` → problem framing and dataset
* `check-in-2.md` → baseline models
* `check-in-3.md` → transformer model
* `final.md` → final analysis and conclusions

---

## Notes

* This project focuses on evaluating robustness under degraded conditions
* Performance may vary depending on threshold selection and training setup
