# Explainable Retinal Disease Classification using Vision Foundation Models

## Benchmarking DINOv2, CLIP and Vision Transformer Models with Explainable AI Validation


## Overview

Deep learning models have shown promising results for automated retinal disease diagnosis from fundus images. However, for medical applications, model transparency and reliability are essential.

In this project, we investigate the performance of vision foundation models for retinal disease classification and evaluate their explainability using lesion-level annotations.

We benchmark three pretrained vision architectures:

- DINOv2
- CLIP
- Vision Transformer (ViT)

using different adaptation strategies:

- Full Fine-tuning
- Linear Probing
- LoRA (Low-Rank Adaptation)


The project focuses on two main objectives:

1. Achieving strong retinal disease classification performance.
2. Understanding whether model predictions are based on clinically meaningful retinal regions.


---

# Dataset Description


Three publicly available retinal datasets were used for training, external evaluation, and explainability validation.


## ODIR-5K

ODIR-5K was used as the primary training dataset.

The dataset contains retinal fundus images covering multiple ophthalmic conditions.

| Dataset | Number of Images | Purpose |
|---|---:|---|
| ODIR-5K | 12,784 | Training and Internal Evaluation |



---

## APTOS 2019


APTOS 2019 Blindness Detection dataset was used for external evaluation.

The original diabetic retinopathy grading was converted into binary classification:

| Original Grade | Class |
|---|---|
| 0 | No DR |
| 1-4 | DR |


| Dataset | Purpose |
|---|---|
| APTOS 2019 | External Testing |



---

## IDRiD


IDRiD was used only for explainability validation because it provides expert lesion segmentation masks.

The segmentation annotations include:

- Microaneurysms (MA)
- Hemorrhages (HE)
- Hard Exudates (EX)
- Soft Exudates (SE)


A segmentation subset containing 54 images was used for quantitative XAI evaluation.


---

# Methodology


The complete workflow consists of:


1. Retinal image preprocessing

2. Feature extraction using pretrained vision foundation models

3. Model adaptation using different fine-tuning strategies

4. Disease classification

5. External validation on APTOS

6. Explainability evaluation using Grad-CAM and HiResCAM


---

# Model Architectures


Nine different models were evaluated:


| Backbone | Strategy |
|---|---|
| DINOv2 | Full Fine-tuning |
| DINOv2 | Linear Probe |
| DINOv2 | LoRA |
| CLIP | Full Fine-tuning |
| CLIP | Linear Probe |
| CLIP | LoRA |
| ViT | Full Fine-tuning |
| ViT | Linear Probe |
| ViT | LoRA |


---

# Fine-Tuning Strategies


## Full Fine-Tuning

The complete pretrained model parameters are updated during training.

Advantages:

- Maximum adaptation capability
- Better task-specific learning


---

## Linear Probing

The pretrained backbone is frozen and only the classification head is trained.

Advantages:

- Faster training
- Less computational cost


---

## LoRA Fine-Tuning

Low-Rank Adaptation introduces small trainable parameters while keeping the main backbone frozen.

Advantages:

- Parameter efficient
- Lower memory requirements
- Maintains pretrained knowledge


---

# Evaluation Metrics


## Classification Metrics

Models were evaluated using:

- AUROC
- Confidence Intervals
- Calibration Analysis


## Explainability Metrics

Generated explanations were compared with expert segmentation masks using:

- Dice Score
- Intersection over Union (IoU)
- Pointing Game Accuracy


---

# Model Performance


AUROC comparison of all evaluated models:


| Model | Internal AUROC | External AUROC |
|---|---:|---:|
| DINOv2-Full | 0.756 | 0.920 |
| DINOv2-Linear | 0.703 | 0.843 |
| DINOv2-LoRA | 0.758 | 0.907 |
| CLIP-Full | 0.695 | 0.748 |
| CLIP-Linear | 0.684 | 0.796 |
| CLIP-LoRA | 0.696 | 0.806 |
| ViT-Full | - | - |
| ViT-Linear | - | - |
| ViT-LoRA | - | - |


---

# ROC Curve Analysis


ROC curves show the ability of each model to distinguish between diseased and non-diseased retinal images.

Higher AUROC indicates better classification performance.


![ROC Curves](plots_complete/roc_all9models.png)



---

# Calibration Analysis


Calibration curves evaluate whether predicted probabilities represent the true confidence of the model.

A well-calibrated model should provide reliable confidence estimates.


![Calibration Curves](plots_complete/reliability_diagram.png)



---

# Explainable AI Visualization


To understand model decisions, Grad-CAM and HiResCAM were applied.

These methods generate heatmaps showing which retinal regions influenced the prediction.


The generated explanations were compared with expert lesion segmentation masks from IDRiD.


![Grad-CAM and HiResCAM Lesion Segmentation](plots_complete/xai_final_grid_lesiononly.png)



The visualization demonstrates that the model focuses on retinal regions containing disease-related abnormalities such as lesions and pathological structures.


---

# Results Files


Complete numerical results are provided in:

results/final_results_9models.json


Explainability evaluation results:

results/xai_metrics_final.csv

results/xai_metrics_lesiononly.csv




---

# Limitations


The current study has several limitations:


- Experiments were performed using publicly available datasets only.

- Differences in imaging devices and patient populations may affect generalization.

- Explainability methods provide visual evidence but cannot completely represent clinical reasoning.

- Further evaluation with ophthalmologists is required.


---

# Future Work


Future research directions include:


## Multi-Class and Multi-Label Disease Detection


Currently, the study mainly focuses on binary diabetic retinopathy classification.

Future work will extend the framework towards:

- Multi-class retinal disease classification

- Multi-label disease detection


This will better represent real clinical scenarios where a patient may have multiple retinal diseases simultaneously.


Possible target diseases include:

- Diabetic Retinopathy
- Glaucoma
- Cataract
- Age-related Macular Degeneration


---

## Larger Clinical Validation


Future studies should include:

- Multi-center datasets
- Different imaging devices
- Diverse patient populations


---

## Multimodal Clinical AI


Future models can combine:

- Retinal images
- Patient metadata
- Clinical information


to develop more comprehensive decision-support systems.


---

# Repository Structure

Explainable-DR-Foundation-Models/

├── README.md
├── LICENSE
│
├── checkpoints/
│
├── plots_complete/
│ ├── reliability_diagram.png
│ ├── roc_all9models.png
│ └── xai_final_grid_lesiononly.png
│
├── results/
│ ├── final_results_9models.json
│ ├── xai_metrics_final.csv
│ └── xai_metrics_lesiononly.csv
│
└── src/




---

# Acknowledgements


We would like to thank **Prof. Juan Miguel Lopez** for his continuous guidance and valuable feedback throughout this project.

His regular consultations helped improve the methodology, evaluation framework, and overall quality of this work.


---



# License


This project is intended for research and educational purposes.







