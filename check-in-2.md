# CHECK-IN 2: FUNDAMENTALS BASELINES

**Project Title:**  Robust Drivable Road Segmentation under Image Degradation  
**Modality:** Vision (Image Segmentation)

---

## 1. CLASSICAL BASELINE

### Method

A classical computer vision baseline was implemented using edge-based image processing techniques:

- Convert image to grayscale  
- Apply Canny edge detection  
- Apply morphological operations
- Generate a binary segmentation mask  

This approach relies purely on low-level features such as edges and intensity gradients, without any learning-based components.

---

### Results

The classical baseline was evaluated on the full KITTI Road training dataset (289 images).

- **Mean Dice Score:** 0.1883  

Example outputs show that the predictions are highly fragmented and noisy.

---

### Observations

- The method captures strong edges but fails to form coherent regions  
- Predictions contain many false positives in non-road areas  
- The output is highly sensitive to lighting and texture  

---

## 2. CNN BASELINE (U-NET)

### Model

A U-Net architecture was implemented as the CNN baseline.

- Input size: 256 × 256  
- Loss function: Binary Cross Entropy  
- Optimizer: Adam (learning rate = 1e-3)  
- Training epochs: 3  

The model learns pixel-wise segmentation from labeled data.

---

### Results

The U-Net model was trained on the training split and evaluated on a validation set.

- **Validation Dice Score:** ~0.75  

Compared to the classical baseline, the U-Net produces significantly smoother and more accurate segmentation masks.

---

### Observations

- The model successfully captures the general shape of the road  
- Predictions are more continuous and less noisy  
- The model demonstrates clear semantic understanding of the scene  

---

## 3. RESULTS AND COMPARISON

| Model | Dice Score |
|------|------------|
| Classical baseline | 0.1883 |
| U-Net baseline | ~0.75 |

---

### Analysis

The U-Net model significantly outperforms the classical baseline.

- The classical approach relies on low-level features and fails to distinguish road from background  
- The CNN model learns high-level semantic representations and produces much more accurate segmentation  

This demonstrates the advantage of deep learning methods for structured vision tasks.

---

## 4. FAILURE ANALYSIS

### Classical Baseline

The classical method fails in multiple ways:

- Produces noisy and fragmented predictions  
- Confuses background edges (trees, buildings, shadows) with road  
- Lacks semantic understanding of the scene  
- Performs poorly under varying lighting conditions  

The worst example achieved a Dice score of 0.0221, indicating near-total failure.

---

### CNN Baseline (U-Net)

Although significantly better, the CNN model still exhibits limitations:

- Road boundaries are sometimes imprecise (over-segmentation)  
- Distant thin road regions are often missed  
- Small noisy predictions appear in non-road regions  
- Performance can degrade under strong lighting variation  

---

### Dataset Limitations

The KITTI annotations introduce additional challenges:

- Some drivable regions are not fully labeled  
- Ground truth masks may not cover the entire visible road  
- This introduces ambiguity during evaluation  

---

## 5. SUMMARY

This milestone demonstrates that:

- Classical methods are insufficient for road segmentation tasks  
- CNN-based models provide substantial improvements  
- U-Net is able to learn meaningful semantic representations  
