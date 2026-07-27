# Experiment 1 — Model Refinement Using Higher Image Resolution

---

## Overview

This experiment represents the first refinement stage of the baseline RT-DETR-L pothole detector developed in the previous notebooks.

The baseline model demonstrated strong detection performance after being trained for 75 epochs on the processed MWPD + RDD (India & Japan) pothole dataset. Rather than restarting training from the original COCO-pretrained weights, this experiment continues training from the previously obtained best-performing checkpoint.

The objective of this refinement stage is to investigate whether increasing the input image resolution while fine-tuning an already trained detector can improve localization accuracy, particularly for small potholes that were identified as challenging during the baseline evaluation.

---

# Motivation

The exploratory data analysis and error analysis performed in previous notebooks revealed several important observations:

- The majority of potholes occupy a relatively small portion of the image.
- Small potholes were responsible for a significant proportion of missed detections.
- Medium and large potholes were detected reliably.
- The baseline model converged successfully without significant overfitting.

These findings suggested that increasing the spatial resolution presented to the detector could potentially improve localization of smaller potholes.

Instead of retraining a completely new model, this experiment adopts an incremental refinement strategy by continuing training from the previously learned detector.

---

# Why Continue From the Baseline Model?

Most benchmark studies compare independent models trained from identical pretrained weights.

However, the primary objective of this project is to develop the strongest possible pothole detector rather than perform only isolated benchmark comparisons.

Since the baseline detector had already learned meaningful pothole representations, continuing from the trained checkpoint provides several advantages:

- Preserves previously learned feature representations.
- Reduces unnecessary retraining.
- Simulates practical model improvement used in real engineering workflows.
- Enables iterative refinement of the detector.

The baseline model therefore serves as the starting point for all subsequent refinement experiments.

---

# Baseline Model

The experiment begins from the checkpoint obtained in Notebook 3.

**Starting checkpoint**

```
best.pt
```

Performance before refinement:

| Metric | Baseline |
|---------|----------|
| Precision | 0.891 |
| Recall | 0.792 |
| mAP@50 | 0.854 |
| mAP@50-95 | 0.541 |

---

# Research Hypothesis

Increasing the input image resolution from **640×640** to **800×800** may preserve additional spatial information, enabling the detector to recognize smaller potholes more accurately.

Expected improvements included:

- Better localization accuracy
- Improved recall
- Higher mAP@50-95
- Improved detection of small potholes

Potential disadvantages included:

- Longer training time
- Increased GPU memory consumption
- Slower inference

---

# Experimental Configuration

| Parameter | Value |
|-----------|-------|
| Model | RT-DETR-L |
| Starting Model | Baseline best.pt |
| Dataset | Processed MWPD + RDD (India & Japan) |
| Epochs | 30 |
| Image Size | 800 × 800 |
| Batch Size | 16 |
| Optimizer | AdamW |
| Learning Rate | 0.0005 |
| Weight Decay | 0.0005 |
| Mixed Precision | Enabled |

---

# Changes Compared to Baseline

| Parameter | Baseline | Experiment 1 |
|-----------|----------|--------------|
| Starting Model | COCO pretrained | Baseline best.pt |
| Training Strategy | Initial training | Fine-tuning |
| Image Size | 640 | 800 |
| Learning Rate | 0.001 | 0.0005 |
| Epochs | 75 | 30 |

---

# Results

| Metric | Baseline | Experiment 1 |
|---------|---------:|-------------:|
| Precision | **0.891** | **0.862** |
| Recall | **0.792** | **0.768** |
| mAP@50 | **0.854** | **0.831** |
| mAP@50-95 | **0.541** | **0.511** |

Training Time:

- Baseline: 7h 24m
- Experiment 1: 5h 22m

---

# Observations

The detector converged successfully throughout training.

Training remained stable without numerical instability or divergence.

However, increasing the image resolution while fine-tuning did **not** improve detection performance.

Compared to the baseline model:

- Precision decreased.
- Recall decreased.
- mAP@50 decreased.
- mAP@50-95 decreased.

Although the detector remained stable, the larger image resolution did not produce measurable benefits under the current training configuration.

---

# Possible Reasons

Several factors may explain the observed decrease in performance.

## 1. Multiple variables changed simultaneously

Compared to the baseline, more than one parameter was modified.

Changes included:

- image resolution
- learning rate
- starting checkpoint
- training duration

Therefore, the observed performance cannot be attributed solely to image resolution.

---

## 2. Fine-tuning duration

The model was fine-tuned for only 30 additional epochs.

The detector may require additional optimization after adapting to the larger image resolution.

---

## 3. Optimization dynamics

Increasing image size changes the scale of the input representation.

Although more spatial information becomes available, optimization becomes more computationally demanding and may require different learning-rate schedules or longer adaptation.

---

# Conclusion

Experiment 1 did not outperform the baseline model.

Although the detector successfully converged, increasing the input image resolution from 640×640 to 800×800 during fine-tuning resulted in lower precision, recall, and mean Average Precision.

Consequently, this experiment does not justify replacing the baseline detector.

The baseline model remains the strongest-performing checkpoint and will continue to serve as the reference model for subsequent refinement experiments.

---

# Future Work

The next refinement stage will investigate alternative strategies that are more likely to improve detector performance without substantially increasing computational cost.

Potential directions include:

- Data augmentation refinement
- Learning-rate scheduling
- Regularization improvements
- Longer fine-tuning
- Combined optimization after identifying the most effective individual modifications

Each future experiment will be compared against the baseline model to ensure that performance improvements are objectively measured.

---

# Experiment Status

**Result:** ❌ No Improvement Over Baseline

Baseline model retained for subsequent experiments.
