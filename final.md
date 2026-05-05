# Final Analysis: Robust Drivable Road Segmentation under Image Degradation

## 1. Project Summary

This project investigates the robustness of road segmentation models under image degradation conditions using the KITTI Road dataset.

The task is binary semantic segmentation:

- Input: front-facing driving scene image  
- Output: pixel-wise binary mask (road vs background)  

The project compares three approaches:

- Classical computer vision baseline  
- CNN-based segmentation (U-Net)  
- Transformer-based segmentation (Vision Transformer, ViT)  

---

## 2. Model Comparison

| Model | Dice Score | IoU |
|------|------------|-----|
| Classical (Edge + Morphology) | 0.1883 | Low |
| U-Net | ~0.75 | ~0.62 |
| ViT-based Segmentation | **0.9217** | **0.8577** |

---

## 3. Key Findings

### 3.1 Classical vs Deep Learning

- The classical baseline performs poorly (Dice ≈ 0.18)  
- It relies on low-level edges and cannot distinguish road from background  
- Predictions are fragmented and highly noisy  

### 3.2 CNN (U-Net)

- U-Net significantly improves performance (Dice ≈ 0.75)  
- It captures semantic structure of the road  
- Produces smoother and more continuous masks  

However:

- Misses thin or distant road regions  
- Boundary precision is limited  

### 3.3 Transformer (ViT)

- The ViT-based model achieves the best performance (Dice = 0.9217) :contentReference[oaicite:1]{index=1}  
- It captures global context using self-attention  
- Produces more complete and coherent road regions  

Key advantage:

- Maintains road continuity across the image  
- More robust to structural variation  

---

## 4. Robustness Analysis

The models were evaluated under different image degradations:

- Noise  
- Blur  
- Low-light  
- Compression  

### Observations

- **Blur** has the largest negative impact  
  - Removes edge information  
  - Makes road boundaries unclear  

- **Low-light** significantly reduces contrast  
  - Model struggles to detect road region  

- **Noise** introduces false positives  

- Classical baseline is extremely sensitive to all degradations  

- Deep learning models are more robust but still degrade in performance  

---

## 5. Threshold Sensitivity

A threshold sweep was performed on the ViT model outputs:

| Threshold | Dice | IoU |
|----------|------|------|
| 0.3 | 0.9098 | 0.8377 |
| 0.5 | **0.9217** | **0.8577** |
| 0.7 | 0.9174 | 0.8501 |

### Insights

- Threshold = 0.5 gives the best performance  
- Lower threshold increases recall but introduces false positives  
- Higher threshold reduces noise but misses road pixels  

This shows the model produces well-calibrated probabilities.

---

## 6. Failure Cases

Despite strong performance, several failure modes remain:

### 6.1 Under-segmentation
- Predicted road is narrower than ground truth  
- Conservative predictions near boundaries  

### 6.2 Boundary Inaccuracy
- Edges are not perfectly aligned  
- Fine-grained details are lost  

### 6.3 Difficult Visual Conditions
- Shadows  
- Blur  
- Low contrast  
- Distant road regions  

---

## 7. Limitations

- Dataset is limited to KITTI (mostly daylight scenes)  
- Limited diversity (weather, night, urban variation)  
- Small dataset size (~289 images)  
- Threshold must be manually selected  
- Model processes single images (no temporal information)  

---

## 8. Future Work

- Adaptive thresholding instead of fixed threshold  
- Video-based segmentation (temporal smoothing)  
- Training on larger and more diverse datasets  
- Improve boundary precision (e.g., hybrid CNN + transformer)  
- Real-time inference optimization  

---

## 9. Conclusion

This project demonstrates that:

- Classical methods are insufficient for semantic segmentation tasks  
- CNN models significantly improve performance by learning spatial features  
- Transformer-based models further improve performance by capturing global context  

The ViT-based model achieves the best results, showing that global attention is highly effective for road segmentation.

However, robustness under degraded conditions and boundary precision remain key challenges for real-world deployment.