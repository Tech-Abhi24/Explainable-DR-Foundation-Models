# Explainable Retinal Disease Classification using Foundation Vision Models

## An Evaluation of DINOv2, CLIP and Vision Transformer Models with Explainable AI for Retinal Disease Prediction


## Overview

Artificial intelligence based retinal image analysis has shown promising results for automated disease screening and clinical decision support. However, despite achieving high predictive performance, deep learning models often lack transparency, which limits their adoption in clinical environments.

In this project, we investigate the performance and explainability of modern vision foundation models for retinal disease classification.

We benchmark multiple pretrained vision architectures using different adaptation strategies and evaluate their:

- Classification performance
- External generalization capability
- Model calibration
- Explainability using lesion-level annotations


The evaluated foundation models include:

- DINOv2
- CLIP
- Vision Transformer (ViT)


Each model is evaluated under three fine-tuning strategies:

- Full fine-tuning
- Linear probing
- LoRA (Low-Rank Adaptation)



# Clinical Motivation

Retinal diseases such as diabetic retinopathy, glaucoma, and age-related macular degeneration are major causes of visual impairment worldwide.

Deep learning models can assist ophthalmologists by automatically identifying disease patterns from fundus images. However, reliable clinical deployment requires not only accurate predictions but also interpretable decision-making.

Therefore, this work focuses on combining:

**High-performance retinal classification + Explainable AI evaluation**


---

# Dataset Description

The experiments use multiple publicly available retinal datasets for training, external validation, and explainability evaluation.


## Training Dataset

## ODIR-5K

The ODIR-5K dataset is used as the primary training dataset.

The dataset contains retinal fundus images covering multiple ophthalmic conditions.

Dataset statistics:

| Dataset | Number of Images | Purpose |
|---|---:|---|
| ODIR-5K | 12,784 | Model training and internal evaluation |


The dataset includes diseases such as:

- Normal retina
- Diabetic retinopathy
- Cataract
- Glaucoma
- Age-related macular degeneration
- Other retinal abnormalities


---

# External Evaluation Dataset

## APTOS 2019 Blindness Detection

APTOS is used as an external benchmark to evaluate model generalization on unseen retinal images.

The original grading labels were converted into binary classification:

| Original Grade | Label |
|---|---|
| Grade 0 | No DR |
| Grade 1-4 | DR |


| Dataset | Purpose |
|---|---|
| APTOS 2019 | External testing |


---

# Explainability Validation Dataset

## IDRiD

The IDRiD dataset is used exclusively for explainability evaluation because it provides expert annotated lesion segmentation masks.

The segmentation annotations contain clinically relevant retinal lesions:

- Microaneurysms (MA)
- Hemorrhages (HE)
- Hard Exudates (EX)
- Soft Exudates (SE)


A segmentation subset containing **54 images** was used for quantitative explainability evaluation.


---

# Methodology

The complete workflow consists of:


1. Retinal image preprocessing

2. Feature extraction using pretrained foundation models

3. Model adaptation using different fine-tuning strategies

4. Disease classification

5. External validation

6. Explainability analysis using Grad-CAM and HiResCAM



---

# Model Architectures


The following vision foundation models were evaluated:


| Model | Adaptation Methods |
|---|---|
| DINOv2 | Full, Linear, LoRA |
| CLIP | Full, Linear, LoRA |
| Vision Transformer (ViT) | Full, Linear, LoRA |



---

# Fine-Tuning Strategies


## Full Fine-Tuning

In full fine-tuning, all parameters of the pretrained backbone are updated during training.

Advantages:

- Maximum model adaptation
- Higher learning capacity


Disadvantages:

- Requires more computational resources


---

## Linear Probing

In linear probing, the pretrained backbone is frozen and only the classification head is trained.

Advantages:

- Faster training
- Lower computational cost
- Fewer trainable parameters


---

## LoRA Fine-Tuning

Low-Rank Adaptation (LoRA) introduces small trainable matrices while keeping the original backbone parameters frozen.

Advantages:

- Parameter-efficient adaptation
- Reduced training cost
- Preserves pretrained knowledge


---

# Evaluation Metrics


The models are evaluated using:


## Classification Metrics

- AUROC (Area Under Receiver Operating Characteristic Curve)
- Confidence Intervals
- Calibration Error


## Explainability Metrics

Explainability methods are evaluated using expert lesion segmentation masks:

- Dice Score
- Intersection over Union (IoU)
- Pointing Game Accuracy


---

# Explainable AI Analysis


To understand model predictions, two explainability approaches were used:


## Grad-CAM

Grad-CAM generates heatmaps showing which retinal regions contributed most to the model prediction.


## HiResCAM

HiResCAM provides higher-resolution localization of important image regions and improves visualization of disease-related areas.



Example visualizations:


```
Add Grad-CAM figure here

figures/plots_complete/gradcam_example.png
```


```
Add HiResCAM figure here

figures/plots_complete/hirescam_example.png
```



---

# Results


## AUROC Performance


| Model | Internal AUROC | External AUROC |
|---|---:|---:|
| DINOv2-Full | 0.756 | 0.920 |
| DINOv2-LoRA | 0.758 | 0.907 |
| DINOv2-Linear | 0.703 | 0.843 |
| CLIP-Full | 0.695 | 0.748 |
| CLIP-LoRA | 0.696 | 0.806 |
| ViT Models | TBD | TBD |



---

# Calibration Analysis


Calibration curves were used to evaluate whether predicted probabilities represent true model confidence.


A well-calibrated model should provide:

- Higher confidence for correct predictions
- Lower confidence for uncertain predictions


Calibration plots are available in:


```
figures/plots_complete/
```


---

# Repository Structure


```
Explainable-DR-Foundation-Models/

│
├── README.md
├── requirements.txt
│
├── notebooks/
│   └── retinal_foundation_models.ipynb
│
├── checkpoints/
│   ├── ckpt_dinov2_full.pth
│   ├── ckpt_dinov2_linear.pth
│   ├── ckpt_dinov2_lora.pth
│   ├── ckpt_clip_full.pth
│   ├── ckpt_clip_linear.pth
│   ├── ckpt_clip_lora.pth
│   ├── ckpt_vit_full.pth
│   ├── ckpt_vit_linear.pth
│   └── ckpt_vit_lora.pth
│
├── datasets/
│
├── results/
│   ├── final_results_9models.json
│   ├── xai_metrics_final.csv
│   └── xai_metrics_lesiononly.csv
│
├── figures/
│   └── plots_complete/
│
├── paper/
│   └── paper.pdf
│
└── presentation/
    └── presentation.pdf
```


---

# How to Run


## Installation


Install required dependencies:


```bash
pip install -r requirements.txt
```


## Dataset Preparation


Download the datasets and place them inside the datasets folder.


Required datasets:

- ODIR-5K
- APTOS 2019
- IDRiD


## Training and Evaluation


Run:


```
notebooks/retinal_foundation_models.ipynb
```


The notebook contains:

- Data preprocessing
- Model training
- Evaluation
- XAI analysis


---


# Explainable Retinal Disease Classification using Vision Foundation Models

## Benchmarking DINOv2, CLIP and Vision Transformer Models with Explainable AI for Retinal Image Analysis


## Overview

Deep learning approaches have demonstrated strong potential for automated retinal disease diagnosis from fundus images. However, the lack of transparency in model decision-making remains a major challenge for clinical adoption.

In this project, we investigate the performance and explainability of modern vision foundation models for retinal disease classification.

We benchmark multiple pretrained vision architectures under different adaptation strategies and evaluate:

- Classification performance
- External generalization capability
- Model calibration
- Explainability using lesion-level annotations


The evaluated foundation models include:

- DINOv2
- CLIP
- Vision Transformer (ViT)


Each architecture is evaluated using three fine-tuning strategies:

- Full fine-tuning
- Linear probing
- LoRA (Low-Rank Adaptation)



---

# Clinical Motivation

Retinal diseases such as diabetic retinopathy, glaucoma, cataract, and age-related macular degeneration are among the leading causes of visual impairment worldwide.

Artificial intelligence-based retinal analysis systems can assist clinicians by providing automated screening and decision support.

However, for medical applications, accurate predictions alone are not sufficient. Models should also provide interpretable evidence explaining why a particular prediction was made.

Therefore, this work focuses on:

**High-performance retinal classification combined with explainable AI evaluation.**



---

# Dataset Description


The experiments use multiple publicly available retinal datasets for training, external evaluation, and explainability validation.


## Training Dataset

## ODIR-5K

ODIR-5K is used as the primary training dataset.

The dataset contains retinal fundus images covering multiple ophthalmic conditions.

| Dataset | Number of Images | Purpose |
|---|---:|---|
| ODIR-5K | 12,784 | Training and internal evaluation |


The dataset contains diseases including:

- Normal retina
- Diabetic Retinopathy
- Cataract
- Glaucoma
- Age-related Macular Degeneration
- Other retinal abnormalities



---

# External Evaluation Dataset


## APTOS 2019 Blindness Detection


APTOS is used as an external benchmark to evaluate model generalization on unseen retinal images.


The original diabetic retinopathy grading labels were converted into binary classification:


| Original Grade | Class |
|---|---|
| Grade 0 | No DR |
| Grade 1-4 | DR |



| Dataset | Purpose |
|---|---|
| APTOS 2019 | External Testing |



---

# Explainability Validation Dataset


## IDRiD


IDRiD is used exclusively for explainability evaluation because it provides expert annotated retinal lesion segmentation masks.


The annotations include:

- Microaneurysms (MA)
- Hemorrhages (HE)
- Hard Exudates (EX)
- Soft Exudates (SE)


A segmentation subset containing 54 images was used for quantitative explainability evaluation.



---

# Methodology


The complete workflow consists of:


1. Retinal image preprocessing

2. Feature extraction using pretrained foundation models

3. Model adaptation using different fine-tuning strategies

4. Disease classification

5. External validation

6. Explainability evaluation using Grad-CAM and HiResCAM



---

# Model Architectures


Three vision foundation models were evaluated:


| Model | Fine-tuning Strategies |
|---|---|
| DINOv2 | Full, Linear, LoRA |
| CLIP | Full, Linear, LoRA |
| Vision Transformer (ViT) | Full, Linear, LoRA |



---

# Fine-Tuning Strategies


## Full Fine-Tuning

The complete pretrained backbone is updated during training.

Advantages:

- Maximum adaptation capability
- Higher learning capacity


Disadvantage:

- Requires more computational resources



---

## Linear Probing

The pretrained backbone is frozen and only the classification head is trained.


Advantages:

- Faster training
- Lower computational requirements
- Fewer trainable parameters



---

## LoRA Fine-Tuning


Low-Rank Adaptation introduces small trainable matrices while keeping the original backbone frozen.


Advantages:

- Parameter-efficient training
- Reduced computational cost
- Preservation of pretrained features



---

# Evaluation Metrics


## Classification Evaluation

The models are evaluated using:


- AUROC
- Confidence intervals
- Calibration analysis



## Explainability Evaluation


Model explanations are compared with expert lesion segmentation masks using:


- Dice Score
- Intersection over Union (IoU)
- Pointing Game Accuracy



---

# Explainable AI Analysis


To understand model decision-making, two explanation techniques were used:


## Grad-CAM


Grad-CAM generates heatmaps highlighting image regions that contribute most strongly to model predictions.


## HiResCAM


HiResCAM provides higher-resolution localization of important retinal regions and allows comparison with expert lesion annotations.



## Explainability Visualization


### HiResCAM with Lesion Segmentation Overlay


![HiResCAM Segmentation](figures/plots_complete/hirescam_segmentation_example.png)



The visualization demonstrates the relationship between model attention regions and clinically annotated retinal lesions.


Highlighted regions correspond to disease-related areas such as:

- Hemorrhages
- Exudates
- Other retinal abnormalities



---

# Classification Results


Performance comparison of all evaluated models:


| Model | Strategy | Internal AUROC | External AUROC |
|---|---|---:|---:|
| DINOv2 | Full | 0.756 | 0.920 |
| DINOv2 | Linear | 0.703 | 0.843 |
| DINOv2 | LoRA | 0.758 | 0.907 |
| CLIP | Full | 0.695 | 0.748 |
| CLIP | Linear | 0.684 | 0.796 |
| CLIP | LoRA | 0.696 | 0.806 |
| ViT | Full | - | - |
| ViT | Linear | - | - |
| ViT | LoRA | - | - |



---

# ROC Curve Analysis


ROC curves were generated to compare the discriminative ability of different models.


A higher AUROC indicates better separation between diseased and non-diseased retinal images.



![ROC Curves](figures/plots_complete/roc_curves.png)



---

# Calibration Analysis


Calibration curves were used to evaluate whether predicted probabilities represent the true confidence of the models.


A well-calibrated model should provide:

- High confidence for correct predictions
- Lower confidence for uncertain predictions



![Calibration Curves](figures/plots_complete/calibration_curves.png)




---

# Key Findings


The main observations of this study are:


- Vision foundation models achieve strong retinal disease classification performance.

- DINOv2 models demonstrate strong external generalization capability.

- LoRA provides competitive performance while reducing trainable parameters.

- Explainability methods highlight clinically meaningful retinal regions.

- Lesion-level evaluation provides quantitative validation of model explanations.


---

# Limitations


The current study has several limitations:


- Evaluation is performed using publicly available datasets only.

- Dataset variability across imaging devices may affect generalization.

- Explainability methods provide visual evidence but do not guarantee complete clinical reasoning.

- Further validation with ophthalmologists is required.


---

# Future Work


Future improvements include:


## Multi-Class and Multi-Label Disease Detection


The current study focuses mainly on binary diabetic retinopathy classification.

Future work will extend the framework towards:


- Multi-class retinal disease classification

- Multi-label disease detection


where a single retinal image can contain multiple simultaneous pathological conditions.


This direction better reflects real clinical scenarios where patients may present with multiple retinal abnormalities such as:

- Diabetic retinopathy
- Glaucoma
- Cataract
- Age-related macular degeneration



---

## Larger Clinical Validation


Future studies should evaluate models using:


- Multi-center retinal datasets

- Different imaging devices

- Diverse patient populations



---

## Advanced Vision-Language Models


Future research can explore multimodal models combining:


- Retinal images

- Clinical metadata

- Medical reports



---

## Improved Explainability


Future work can investigate:


- Lesion-aware training approaches

- Better explanation methods

- Expert ophthalmologist evaluation of generated explanations


---

# Acknowledgements


We would like to thank **Prof. Dr. Nils Strodthoff** and **Dr. Juan Lopez Alcaraz** for his continuous guidance, valuable feedback, and support throughout this project.

Their valuable suggestions and feedback during regular consultations helped improve the methodology, evaluation framework, and overall quality of this work.


---


# License

This project is intended for research and educational purposes.
