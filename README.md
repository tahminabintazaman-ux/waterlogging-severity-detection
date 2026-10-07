# Automated Waterlogging Severity Detection from Ground-Level Street Imagery

## Project Overview

This project focuses on **automated waterlogging severity detection from ground-level street images using deep learning**.

The objective is to classify roadway waterlogging into three severity levels:

* **Low**
* **Medium**
* **High**

The project uses roadway images and corresponding segmentation masks to calculate water coverage and define the severity classes. Three deep learning models were developed and compared: **Custom CNN, VGG16, and EfficientNetB0**.

## Dataset

The project uses the **Roadway Flooding Image Dataset** obtained from Kaggle.

After checking the dataset, **440 valid and unique roadway images** were used.

The severity classes were defined using water coverage percentage:

| Severity | Water Coverage |
| -------- | -------------- |
| Low      | < 15%          |
| Medium   | 15% – 35%      |
| High     | > 35%          |

These thresholds are project-defined operational thresholds.

## Data Preprocessing

The following preprocessing steps were performed:

* Converted images to RGB format
* Resized images to **224 × 224**
* Normalized pixel values from **0–255 to 0–1**
* Extracted image features such as brightness, contrast, RGB values, and water coverage
* Used a **70/15/15 stratified split** for training, validation, and testing
* Performed a data leakage check

## Exploratory Data Analysis

The final dataset contains:

* **Low:** 23 images
* **Medium:** 127 images
* **High:** 290 images

The dataset is therefore highly imbalanced, with High-severity images being the majority class.

## Models

Three deep learning models were developed and compared:

1. **Custom CNN** – used as the baseline model
2. **VGG16** – transfer learning-based CNN architecture
3. **EfficientNetB0** – efficient modern CNN architecture

Class weighting was used during training to reduce the effect of class imbalance.

## Evaluation

The models were evaluated using:

* Accuracy
* Precision
* Recall
* Macro F1-score
* Confusion Matrix

**Macro F1-score** was considered the main metric because the dataset contains a significant class imbalance.

### Final Results

| Model          | Accuracy | Precision | Recall |   Macro F1 |
| -------------- | -------: | --------: | -----: | ---------: |
| Custom CNN     |   72.73% |    56.70% | 53.69% | **54.24%** |
| EfficientNetB0 |   71.21% |    47.12% | 48.56% |     47.46% |
| VGG16          |   65.15% |    42.20% | 40.55% |     41.33% |

Based on Macro F1-score, the **Custom CNN** achieved the best overall class-balanced performance among the three models.

## Ablation Study

An ablation study was performed to investigate the effect of class weighting.

| Model                     | Accuracy |   Macro F1 |
| ------------------------- | -------: | ---------: |
| CNN with Class Weights    |   72.73% | **54.24%** |
| CNN without Class Weights |   75.76% |     47.19% |

Although removing class weights increased accuracy, it reduced Macro F1. This shows that class weighting helped improve more balanced class-wise performance.

## Limitations

* The dataset is relatively small.
* The dataset is highly imbalanced.
* Only 23 images belong to the Low-severity class.
* Environmental factors such as lighting and reflections can affect image classification.
* The severity thresholds are project-defined and are not universal flood standards.
* The model may have limited generalization to different locations and environmental conditions.

## Technologies Used

* Python
* Google Colab
* TensorFlow / Keras
* CNN
* VGG16
* EfficientNetB0
* NumPy
* Pandas
* Matplotlib
* Seaborn
* Scikit-learn

## Project Structure

```text
waterlogging-severity-detection/
│
├── README.md
├── Waterlogging_Severity_Detection.ipynb
│
├── dataset/
│   └── README.md
│
├── results/
│   ├── confusion_matrix/
│   └── plots/
│
└── report/
    └── project_report.pdf
```

## Conclusion

This project investigates the feasibility of using deep learning to classify roadway waterlogging severity from ground-level street imagery. The results provide evidence that deep learning models can identify severity-related visual patterns, with the **Custom CNN achieving the highest Macro F1-score of 54.24%** among the tested models.
