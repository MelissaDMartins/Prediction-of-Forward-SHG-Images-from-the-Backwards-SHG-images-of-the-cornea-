# Recovering Collagen Structural Information present in the Forward SHG from Backward SHG Images of the Cornea Using Deep Learning 

### Overview

The goal of this project is to achieve accurate, interpretation of collagen structural features—such as fibre orientation, density, and crimp—directly from backward Second Harmonic Generation (SHG) images of the cornea. 

To address this clinical need, a U-Net deep learning architecture was developed to predict forward SHG images from backward SHG scattering data. The model focuses primarily on reconstructing and predicting collagen fibre orientation using the clinically accessible backward SHG signal, eliminating the need for more invasive or complex forward-imaging modalities.

### Dataset Examples
<p align="center">
<img width="716" height="410" alt="image" src="https://github.com/user-attachments/assets/bdf7e0f3-2a45-4381-803a-15d40b9d974c"> </p>

### Dataset & Pre-processing Pipeline

#### 1. Dataset Characteristics

* **Source Material:** 310 paired Second Harmonic Generation (SHG) images.
* **Biological Model:** Acquired from 7 pressurized intact porcine corneas.

#### 2. Image Pre-processing Pipeline

To condition the cross-modal image pairs for deep learning model training, an end-to-end data pipeline was developed: 

* **Global Normalisation:** Patches were dynamically rescaled to a 0–1 range using p1 and p99 intensity percentiles to eliminate extreme sensor noise.
* **Patch Extraction:** Z-slices were tiled into uniform 256 × 256 non-overlapping patches to maximize training sample volume.

#### 3. Forward Image Enhancement (Ground Truth Conditioning)

To optimize the structural visibility of collagen fibres for model supervision, target forward images underwent rigorous enhancement: 

* **CLAHE Application:** Implemented Contrast-Limited Adaptive Histogram Equalisation to maximize local structural contrast.
* **Binarization Thresholding:** Applied a strict 0.7 intensity threshold to segment clean collagen fiber boundaries.
* **Noise Reduction:** Deployed a Median Filter to eliminate lingering background high-frequency noise artifacts.
<p align="center">
<img width="721" height="194" alt="image" src="https://github.com/user-attachments/assets/2630ebec-018c-410b-8cf2-43ab96eb52e4"> </p>

#### 4. Data Partitioning

* **Split Ratio:** Managed an exact **80% Training / 10% Validation / 10% Test** split to ensure rigorous, unbiased model evaluation.

### Results & Evaluation

The trained U-Net model was evaluated on a completely held-out test dataset, demonstrating the clear feasibility of predicting complex, forward-scattering collagen structural features directly from a clinically available backward SHG signal. 

### 1. Quantitative Performance Metrics

The model achieved highly robust, consistent baseline scores across the test set: 

* **Dice Similarity Coefficient:** 0.609 ± 0.0087 (proves consistent structural overlap)
* **Intersection over Union (IoU):** 0.438 ± 0.0090
* **95th Percentile Hausdorff Distance (HD95):** 5.50px ± 0.64px (confirms low boundary error)
* **Block-Averaged Intensity Difference:** 0.250 ± 0.0098

### 2. Qualitative Structural Validation (OrientationJ)

To verify that the model was learning genuine biological structures rather than random noise, **OrientationJ analysis** was executed: 

* **Fiber Alignment:** Validation confirmed broad structural similarities in the dominant collagen fibre orientation between the U-Net's predicted outputs and the true forward-scattering ground truth images.
* **Clinical Significance:** This alignment proves the model successfully mapped hidden structural features from the backward signal, paving the way to make highly interpretable, advanced collagen data accessible in fast-paced clinical settings.
* While the Binary Prediction was evaluated , the Continuous Prediction ( raw model outputs) proved superior at retaining organic structural boundaries and smooth collagen fiber orientation gradients.
<p align="center">
<img width="560" height="246" alt="Screenshot 2026-08-17 115352" src="https://github.com/user-attachments/assets/c688a691-7276-42dd-86d7-81662c78da98"> </p>


