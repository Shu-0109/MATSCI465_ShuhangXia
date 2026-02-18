# MATSCI465_ShuhangXia
This was created in 2026.1.7. for MATSCI465 course. ^-^
This environment requires Python NumPy, SciPy, Matplotlib, HyperSpy and py4DSTEM.

### Project Structure Directory



# Assignment02：
Virtual Detectors allow you to "re-image" your sample after the experiment is finished, just as if you were still sitting at the microscope.

Data Foundation: 4D-STEM records a complete 2D diffraction pattern for every single pixel in the scanned area (creating a 4D dataset).

Post-Masking: Using computer algorithms, you generate a "virtual" shape (for example, a small circle for Bright Field or a ring for Dark Field).

Pixel Integration: The intensity of the electrons falling within that virtual shape is summed up for every diffraction frame to determine the brightness of the corresponding pixel in the final image.

Because the raw data contains information about all electrons, you can freely adjust the detector's size, shape, or position after the experiment. This allows you to extract Bright Field (BF), Annular Dark Field (ADF), or any specific angular image from the same data without needing to re-run the experiment.


# Assignment03&04：
# Particle Analysis Pipeline: Classical, Machine Learning, and Deep Learning

This repository documents a comprehensive workflow for particle segmentation and classification, developed for the **MATSCI 465** course. The project transitions from geometric algorithms to state-of-the-art neural networks to analyze microscopy data.

---

## 1. Methodology

The project explores four distinct paradigms for image analysis:

* **Classical Computer Vision**: Utilizes **Otsu's Thresholding** for binarization and the **Watershed algorithm** to separate overlapping particles based on distance transforms.
* **Machine Learning (ML)**: Extracts morphological descriptors to train **Random Forest** and **SVM** classifiers to distinguish between particle size categories.
* **CNN Classification**: Implements a lightweight **Convolutional Neural Network** with `GlobalAveragePooling2D` for binary classification (Small vs. Large particles).
* **U-Net Segmentation**: Employs a **U-Net** architecture with an encoder-decoder structure and skip connections to achieve precise pixel-wise binary segmentation.



---

## 2. Quantitative Comparison

The following table summarizes the performance metrics based on the experimental results recorded in the notebook:

| Method | Evaluation Metric | Result | Runtime | Data Requirement |
| :--- | :--- | :--- | :--- | :--- |
| **Watershed** | Segmentation Quality | N/A | **Instant** | Unsupervised |
| **SVM** | Classification F1-Score | **0.9630** | Fast | High (Class Labels) |
| **Random Forest** | Classification F1-Score | **1.0000** | Fast | High (Class Labels) |
| **CNN** | Classification F1-Score | **0.8889** | Moderate | High (Class Labels) |
| **U-Net** | Segmentation IoU | **0.8795** | Slow (GPU) | Highest (Pixel Masks) |

*Note: The U-Net model additionally achieved a **Dice Coefficient of 0.9359**.*

---

## 3. Key Findings & Interpretability

* **Feature Importance**: In the Random Forest model, **Solidity** and **Circularity** were identified as critical descriptors, suggesting that shape characteristics are primary differentiators for particle classification.
* **Deep Learning Visualization**: 
    * **CNN**: The model successfully learned to classify particles with an F1-score of ~0.89 using basic convolutional blocks.
    * **U-Net**: Feature maps confirm that early layers (`conv2d_3`) capture edge gradients, while skip connections (`concatenate_2`) restore spatial resolution during upsampling.
* **Model Trade-offs**: While traditional Watershed is efficient, deep learning methods (CNN/U-Net) offer superior robustness against noisy backgrounds and complex particle overlaps.



---

## 4. Recommended Use-Cases

* **Classical (Watershed)**: Recommended for high-contrast images where particles are clearly separated and real-time processing is required.
* **Machine Learning (RF/SVM)**: Ideal when interpretability is needed to understand the physical and geometric factors driving the classification.
* **Deep Learning (CNN/U-Net)**: Mandatory for complex datasets with low signal-to-noise ratios or significant particle overlap where automated feature extraction is necessary.



---

## 5. How to Run
1. Ensure all dependencies are installed: `pip install -r requirements.txt`.
2. Update the `IMAGE_DIR` path in the notebook to match your local dataset location.
3. Execute the cells in `assignment_04_combined.ipynb` sequentially to reproduce the pipeline and plots.
