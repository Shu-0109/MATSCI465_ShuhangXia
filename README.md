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

## 1. Methodology (方法论)

The project explores three distinct paradigms for image analysis:

* **Classical Computer Vision**: Utilizes **Otsu's Thresholding** for binarization and the **Watershed algorithm** to separate overlapping particles based on distance transforms.
* **Machine Learning (ML)**: Extracts 10+ morphological descriptors (such as **Solidity**, **Circularity**, and **Eccentricity**) to train **Random Forest** and **SVM** classifiers.
* **Deep Learning (DL)**: Implements a **U-Net** architecture. This encoder-decoder model uses skip connections to preserve high-resolution spatial details, enabling precise pixel-wise segmentation.



---

## 2. Quantitative Comparison 

The following table summarizes the performance based on our experimental results:

| Method | Evaluation Metric | Result | Runtime | Data Requirement |
| :--- | :--- | :--- | :--- | :--- |
| **Watershed** | Segmentation Quality | N/A | **Instant** | None (Unsupervised) |
| **SVM** | Classification F1-Score | **0.9630** | Fast | High (Class Labels) |
| **Random Forest** | Classification F1-Score | **1.0000** | Fast | High (Class Labels) |
| **U-Net** | Segmentation IoU | **0.8795** | Slow (GPU) | Highest (Pixel Masks) |

*Note: The U-Net model also achieved a **Dice Coefficient of 0.9359**, indicating excellent overlap with ground truth masks.*

---

## 3. Key Findings & Interpretability 

* **Feature Importance**: In the Random Forest model, **Solidity** was identified as a critical feature, suggesting that the "fullness" of a particle is a primary differentiator between size classes.
* **Feature Maps**: Visualizing U-Net intermediate layers confirms that the encoder captures edge gradients in early stages (`conv2d_3`), while the skip connections (`concatenate_2`) successfully restore boundary details during upsampling.
* **Model Robustness**: While traditional Watershed is efficient, **U-Net** is significantly more robust against noisy backgrounds and low-contrast boundaries common in real-world microscopy.



---

## 4. Recommended Use-Cases 

* **Classical (Watershed)**: Best for high-contrast images where particles are clearly defined and separated.
* **Machine Learning (RF/SVM)**: Ideal when interpretability is needed to understand the physical/geometric factors driving classification.
* **Deep Learning (U-Net)**: Mandatory for complex datasets with low SNR (Signal-to-Noise Ratio) or significant particle overlap.



---

## 5. How to Run
1.  Ensure all dependencies are installed: `pip install -r requirements.txt`.
2.  Update the `IMAGE_DIR` path in the notebook to point to your `raw_data` folder.
3.  Run the cells in `assignment_04_combined.ipynb` sequentially to reproduce the pipeline and plots.
