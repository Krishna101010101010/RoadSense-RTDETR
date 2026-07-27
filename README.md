# RoadSense
### Real-Time Road Damage Detection and Severity Assessment using RT-DETR

RoadSense is an end-to-end computer vision pipeline for automated pothole detection, localization, and severity estimation from road images and videos. The project leverages state-of-the-art transformer-based object detection (RT-DETR) together with image processing techniques to build an intelligent road inspection system suitable for smart city infrastructure monitoring, transportation authorities, and autonomous inspection workflows.

The project focuses on developing a robust detection model trained on multiple public road damage datasets and extends traditional object detection by estimating pothole severity using geometric and visual characteristics.

---

# Project Objectives

- Build a high-quality unified pothole dataset from multiple public datasets.
- Analyze dataset quality and distribution before training.
- Train a transformer-based object detector (RT-DETR).
- Evaluate model performance using standard detection metrics.
- Perform real-time inference on images and videos.
- Estimate pothole severity using geometric measurements.
- Provide a complete reproducible research pipeline.

---

# Features

- RT-DETR based real-time object detection
- Multi-dataset training
- Dataset preprocessing and cleaning
- Exploratory Data Analysis (EDA)
- Automatic annotation validation
- Video inference pipeline
- Severity estimation engine
- Visualization utilities
- Performance evaluation

---

# Dataset

The model is trained using a combination of publicly available road damage datasets.

### Primary Datasets

- MWPD (Multiple Weather Pothole Dataset)
- RDD2022 (Road Damage Dataset - India & Japan)

The datasets were merged, cleaned, standardized, and converted into the YOLO annotation format before training.

---

# Technology Stack

| Category | Technology |
|----------|------------|
| Language | Python |
| Deep Learning | PyTorch |
| Detection Framework | Ultralytics |
| Model | RT-DETR |
| Computer Vision | OpenCV |
| Visualization | Matplotlib, Seaborn |
| Data Analysis | Pandas, NumPy |
| Notebook Environment | Jupyter / Kaggle |
| Annotation Format | YOLO |

---

# Project Pipeline

```
Dataset Collection
        │
        ▼
Dataset Audit
        │
        ▼
Dataset Preprocessing
        │
        ▼
Exploratory Data Analysis
        │
        ▼
RT-DETR Training
        │
        ▼
Model Evaluation
        │
        ▼
Video/Image Inference
        │
        ▼
Severity Estimation
```

---

# Repository Structure

```
RoadSense/
│
├── notebooks/
│
├── datasets/
│
├── models/
│
├── outputs/
│
├── videos/
│
├── images/
│
├── weights/
│
├── README.md
│
└── requirements.txt
```

---

# Notebook Overview

The project has been organized into modular notebooks, where each notebook performs one stage of the complete machine learning pipeline.

---

## 1. Dataset Audit

### Purpose

Before training any model, the datasets are inspected to identify inconsistencies, missing labels, duplicate files, corrupted annotations, and class imbalance.

### This notebook performs

- Dataset integrity verification
- Missing image detection
- Missing annotation detection
- Duplicate sample identification
- Invalid bounding box detection
- Label statistics
- Image dimension analysis
- Dataset summary generation

### Output

- Clean dataset report
- Annotation quality statistics
- Dataset health metrics

---

## 2. Dataset Preprocessing

### Purpose

Standardizes multiple datasets into one unified training dataset.

### This notebook performs

- Merge MWPD and RDD datasets
- Convert annotations into YOLO format
- Normalize class labels
- Rename files
- Resize images (if required)
- Generate train/validation splits
- Organize directory structure

### Output

```
dataset/
    train/
    valid/
    test/
```

ready for RT-DETR training.

---

## 3. Exploratory Data Analysis (EDA)

### Purpose

Understand the characteristics of the dataset before model training.

### This notebook analyzes

- Number of images
- Number of annotations
- Class distribution
- Bounding box size distribution
- Aspect ratio distribution
- Object density
- Image resolution statistics
- Dataset imbalance
- Sample visualizations

### Output

Insights used for improving training quality.

---

## 4. RT-DETR Training

### Purpose

Train the RT-DETR object detection model.

### Training pipeline

- Load pretrained RT-DETR weights
- Configure training hyperparameters
- Train on merged dataset
- Monitor training loss
- Save best model
- Export trained weights

### Output

```
best.pt
last.pt
training metrics
```

---

## 5. Model Evaluation

### Purpose

Evaluate the trained detector on the validation dataset.

### Metrics computed

- Precision
- Recall
- mAP@0.5
- mAP@0.5:0.95
- F1 Score
- Confusion Matrix
- PR Curve
- Detection visualizations

### Output

Comprehensive model performance report.

---

## 6. Video Inference

### Purpose

Run the trained model on videos for real-time road inspection.

### Features

- Frame-by-frame detection
- Bounding box visualization
- Confidence scores
- Video rendering
- Detection statistics

### Output

Annotated detection video.

---

## 7. Severity Estimation

### Purpose

Estimate pothole severity beyond object detection.

Instead of only detecting potholes, this notebook analyzes each detected pothole using geometric measurements to estimate its relative severity.

### Current methodology

The notebook computes features such as

- Bounding box area
- Relative road coverage
- Estimated pothole size
- Detection confidence
- Visual Severity Index (VSI)

The severity score is then categorized into classes such as

- Low
- Moderate
- High

This provides richer information for maintenance prioritization.

### Output

Example

| Detection | Severity | Score |
|------------|----------|-------|
| Pothole | Low | 0.28 |
| Pothole | Moderate | 0.56 |
| Pothole | High | 0.91 |

---

# Current Project Achievements

The project has successfully completed the following milestones:

- Combined multiple public pothole datasets.
- Standardized annotations into YOLO format.
- Built an automated dataset preprocessing pipeline.
- Performed comprehensive exploratory data analysis.
- Successfully trained an RT-DETR detector.
- Achieved accurate pothole localization.
- Developed an evaluation framework using standard detection metrics.
- Implemented real-time video inference.
- Designed a severity estimation pipeline based on geometric analysis.
- Established a reproducible end-to-end deep learning workflow.

---

# Future Improvements

The project can be extended with several advanced capabilities:

- Road crack detection
- Multi-class road damage classification
- Depth estimation using monocular vision
- GPS-based pothole localization
- Road condition heatmaps
- Edge deployment using TensorRT
- Mobile application integration
- Drone-based inspection
- Real-time municipal reporting system
- Temporal tracking across video frames

---

# Model

Current Detection Model

```
RT-DETR
```

Framework

```
Ultralytics
```

Backend

```
PyTorch
```

---

# Example Workflow

```
Road Video
      │
      ▼
Frame Extraction
      │
      ▼
RT-DETR Detection
      │
      ▼
Bounding Boxes
      │
      ▼
Severity Estimation
      │
      ▼
Annotated Output
```

---

# Installation

```bash
git clone https://github.com/<username>/RoadSense.git

cd RoadSense

pip install -r requirements.txt
```

---

# Running the Project

Train Model

```bash
python train.py
```

Run Inference

```bash
python predict.py
```

Evaluate Model

```bash
python evaluate.py
```

---

# Research Scope

RoadSense demonstrates a complete research workflow for intelligent road infrastructure monitoring using transformer-based object detection. Beyond object localization, the project introduces a severity estimation module that supports data-driven maintenance prioritization. The modular notebook-based design enables experimentation with datasets, architectures, and post-processing techniques, making the repository suitable for academic research, benchmarking, and future development of large-scale automated road inspection systems.

---

# License

This project is intended for educational and research purposes.
