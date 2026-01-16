# Multi-Task-Multimodal-Image-Text-Classification-for-Country-and-Weather-Prediction

This repository contains the implementation and analysis of a **multimodal machine learning framework** for predicting **country** and **weather** labels from **travel images and textual descriptions**.
The project was developed as part of **ENCS5341 – Machine Learning and Data Science (Assignment #3)** at **Birzeit University**.

The work covers the complete machine learning pipeline, including **data consolidation and cleaning**, **exploratory data analysis**, **image-based learning**, **text-based learning**, and **multimodal fusion**, with extensive quantitative evaluation and error analysis.

---

## 1. Project Objectives

The main objectives of this project are:

* To consolidate and clean heterogeneous data collected from multiple student submissions
* To analyze the characteristics and challenges of a real-world, highly imbalanced dataset
* To evaluate the effectiveness of image-based, text-based, and multimodal classification approaches
* To investigate the benefits of **multi-task learning** for jointly predicting country and weather
* To compare traditional machine learning models with deep learning approaches

---

## 2. Dataset Description

* **Total samples:** 966
* **Contributors:** 106 students
* **Countries:** 122 (severe class imbalance)
* **Labels available:**

  * Country
  * Weather
  * Time of Day
  * Season
  * Activity
  * Mood / Emotion

Each data instance follows the standardized schema:

```
Image URL | Description | Country | Weather | Time of Day | Season | Activity | Mood/Emotion
```

---

## 3. Data Concatenation and Cleaning Pipeline

A dedicated preprocessing pipeline was developed to ensure data consistency and quality prior to model training.

### Key Capabilities

* Robust loading of CSV files with multiple encodings (UTF-8, Latin-1, ISO-8859-1, CP1252)
* Detection and correction of inconsistent column naming conventions
* Enforcement of a canonical schema with eight standardized columns
* Validation and filtering of invalid image URLs
* Duplicate removal to prevent data leakage
* Missing value imputation using the category *“Not Clear”*
* Generation of exploratory data analysis (EDA) reports and visualizations

### Output

The pipeline produces a single cleaned dataset:

```
all_students_combined_and_cleaned.csv
```

This file is required for all subsequent machine learning experiments.

---

## 4. Image-Based Classification

### Approaches

* **Baseline:** k-Nearest Neighbors using handcrafted visual features
* **Deep Learning:** EfficientNet-B0 with ImageNet pre-trained weights
* **Multi-Task Learning:** Joint prediction of country and weather using a shared CNN backbone

### Techniques

* Data augmentation
* Transfer learning
* Early stopping
* Multi-task loss optimization

---

## 5. Text-Based Classification

### Feature Extraction

* TF-IDF vectorization (unigrams and bigrams)

### Models Evaluated

* k-Nearest Neighbors
* Random Forest
* Multinomial Naive Bayes

### Key Observation

Textual references to landmarks and geographical entities were found to be the most discriminative features for country classification.

---

## 6. Multimodal Classification

Multimodal learning was performed by combining image and text features using early and late fusion strategies.

### Fusion Methods

* Feature concatenation (early fusion)
* Weighted fusion
* Ensemble-based late fusion

### Finding

Multimodal fusion did not outperform the best single-modality models, primarily due to limited expressiveness of simplified image features, highlighting the importance of high-quality representations in multimodal systems.

---

## 7. Experimental Results (Summary)

| Approach                     | Best Accuracy |
| ---------------------------- | ------------- |
| Image-Based (Multi-Task CNN) | 66.3%         |
| Text-Based (Random Forest)   | 61.34%        |
| Multimodal Fusion            | 58.12%        |

### General Observations

* Multi-task learning improved generalization for both targets
* Class imbalance significantly affected rare countries and weather classes
* Transfer learning enabled effective image classification despite limited data
* Text-based models performed competitively due to strong semantic cues

---

## 8. Execution Instructions

### Step 1: Data Preprocessing

1. Open `Data_concatenation_and_clean.ipynb` in Google Colab
2. Mount Google Drive
3. Place raw student CSV files in the expected directory
4. Execute all cells to generate the cleaned dataset

### Step 2: Machine Learning Experiments

1. Open `Assignment3_Main_Code.ipynb`
2. Upload `all_students_combined_and_cleaned.csv`
3. Mount Google Drive
4. Ensure images are stored in:

```
MyDrive/Assignment3_ENCS5341/images/
```

5. Run all cells sequentially

---

## 9. Technologies Used

* Python
* PyTorch
* scikit-learn
* EfficientNet-B0
* TF-IDF
* NumPy, Pandas
* Matplotlib, Seaborn

---

## 10. Limitations

* Extreme class imbalance across countries
* Short and generic textual descriptions
* Limited samples for minority weather classes
* Simplified image features in multimodal fusion

---

## 11. Authors

* **Asma’a Abdalrahman Shejaeya** — Student ID: 1210084
* **Khaled Azmi Rimawi** — Student ID: 1210618

Department of Electrical & Computer Engineering
Birzeit University





Just tell me.

