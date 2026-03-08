# CHECK-IN 1: PROBLEM FRAMING AND DATA AUDIT  
**Project Title:** Robust Drivable Road Segmentation under Image Degradation  
**Modality:** Vision (Image Segmentation)

---

## 1. PROBLEM FRAMING AND SCOPE

### TASK DEFINITION

This project investigates the robustness of road segmentation models under image degradation conditions relevant to autonomous driving.

**Input:** Front-facing driving scene image  
**Output:** Pixel-wise binary segmentation mask (Road vs Background)

---

### MOTIVATION

Autonomous driving systems operate in non-ideal conditions, including:

- Motion blur  
- Sensor noise  
- Low-light environments  
- Image compression artifacts  

Most segmentation models are trained on clean datasets. However, real-world deployment involves degraded inputs. Understanding model robustness under such conditions is critical for safety and reliability.

---

### SCOPE

To ensure feasibility within one semester, the project is scoped as follows:

- Binary segmentation only (drivable road vs non-road)  
- Use a lightweight dataset (KITTI Road)  
- Implement a baseline CNN model (U-Net) in Check-In 2  
- Evaluate robustness via controlled image corruption  

This scope ensures the project remains measurable and achievable.


### SUCCESS CRITERIA

The project will be considered successful if:

- A baseline road segmentation model can be trained on the dataset.
- The model achieves stable segmentation performance on clean validation data.
- Performance degradation can be measured under different image corruption levels（blur, noise, brightness）

## 2. DATASET ACCESS AND DOCUMENTATION

### DATASET

Dataset: KITTI Road Benchmark  
Source: https://www.cvlibs.net/datasets/kitti/eval_road.php  

### DATASET SIZE

- ~289 training images  
- ~290 test images  
- Image resolution ≈ 1242 × 375  


### LICENSE / USAGE
The dataset is available for academic and research use.

### DOWNLOAD INSTRUCTIONS

1. Download the dataset from the official KITTI website.
2. Extract it into the project directory
---

## 3. DATA AUDIT / EXPLORATORY DATA ANALYSIS (EDA)

### REPRESENTATIVE SAMPLES

The dataset was inspected by visualizing:

- Original driving scene images  
- Ground truth road masks  
- Overlay of image and mask  


**Initial observations:**

- Road width varies significantly due to perspective effects.  
- Distant road regions appear thinner and more difficult to segment.  
- Shadows and lighting variation affect boundary clarity.  
- Road edges sometimes blend with sidewalks or surrounding structures.  

---

### BASIC DATASET CHARACTERISTICS

- Binary segmentation task (Road vs Background)  
- ~240 training images  
- ~240 test images  
- Image resolution ≈ 1242 × 375  
- Road pixels occupy approximately **XX–XX%** of the image area

---

### POTENTIAL ARTIFACTS / BIASES

- Most images are captured in daylight conditions.  
- Limited variation in extreme weather or nighttime scenarios.  
- Strong shadows appear in several scenes.  
- Perspective distortion makes distant road regions smaller and harder to segment.  

These characteristics may influence model robustness.

---

## 3. EVALUATION PLAN

### METRICS

The following metrics will be used:

- Dice Score  
- Mean Intersection over Union (mIoU)  

Both metrics measure overlap quality between predicted masks and ground truth.

---

### TRAIN / VALIDATION / TEST SPLIT

Since the dataset does not provide a validation split:

- 80% training  
- 20% validation  
- Test set reserved for final evaluation  

Random splitting will be used while preserving road coverage distribution.

---

### ROBUSTNESS EVALUATION STRATEGY

To simulate real-world degradation, the following corruptions will be applied:

- Gaussian Blur (multiple sigma levels)  
- Gaussian Noise (increasing variance)  
- Brightness reduction  
- JPEG compression  

Performance will be evaluated using curves such as:

- Dice vs Blur Level  
- Dice vs Noise Level  
- Dice vs Brightness Factor  
- Dice vs Compression Quality  

---

## 4. INITIAL BASELINE / REPRESENTATION PLAN

### CLASSICAL BASELINE

- Convert image to grayscale  
- Apply Canny edge detection  
- Perform morphological operations  
- Generate binary road mask  

This provides a non-deep-learning reference baseline.

---

### CNN BASELINE

- U-Net architecture  
- Binary Cross Entropy + Dice Loss  
- Adam optimizer  

This model will serve as the primary segmentation baseline.