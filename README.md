Explainable Diabetic Retinopathy Classification using Foundation Models

Explainable AI Evaluation of Retinal Foundation Models for Disease Classification

Overview

Diabetic retinopathy (DR) is one of the leading causes of preventable blindness worldwide. Deep learning models have shown strong performance in retinal disease classification; however, their lack of interpretability remains a major limitation for clinical adoption.

In this project, we investigate the capability of foundation vision models for retinal disease classification and evaluate their explainability using lesion-level annotations.

We benchmark multiple pretrained vision architectures under different fine-tuning strategies and analyze their performance, calibration, and explainability.

The evaluated models include:

DINOv2
CLIP
Vision Transformer (ViT)

with three adaptation strategies:

Full fine-tuning
Linear probing
LoRA-based parameter-efficient fine-tuning
Dataset

The experiments use multiple retinal datasets to evaluate generalization across different clinical domains.

Training Dataset
ODIR-5K

The main training dataset consists of retinal fundus images collected from multiple ophthalmic conditions.

Dataset statistics:

Dataset	Images	Purpose
ODIR-5K	12,784	Model training and internal evaluation

The dataset contains multiple retinal diseases including:

Normal
Cataract
Diabetic Retinopathy
Glaucoma
AMD
Other retinal abnormalities
External Evaluation Dataset
APTOS 2019 Blindness Detection

APTOS is used for external validation to evaluate model generalization on an unseen dataset.

The original grading labels were converted into binary classification:

Grade 0 → No DR
Grade 1–4 → DR
Dataset	Samples	Purpose
APTOS	677	External testing
Explainability Validation Dataset
IDRiD

IDRiD provides expert-annotated lesion segmentation masks, enabling quantitative evaluation of explainability methods.

It is used only for XAI validation.

Annotated lesions include:

Microaneurysms (MA)
Hemorrhages (HE)
Hard Exudates (EX)
Soft Exudates (SE)

A segmentation subset containing 54 images was used for lesion-level evaluation.

Methodology

The complete workflow consists of:

Image preprocessing
Foundation model feature extraction
Model adaptation
Disease classification
External validation
Explainability evaluation
Model Architectures

We evaluate:

Model	Strategy
DINOv2	Full / Linear / LoRA
CLIP	Full / Linear / LoRA
Vision Transformer	Full / Linear / LoRA
Fine-tuning Strategies
Full Fine-tuning

All backbone parameters are updated during training.

Advantages:

Maximum adaptation capability

Disadvantage:

High computational cost
Linear Probing

The pretrained backbone is frozen and only the classifier head is trained.

Advantages:

Faster training
Fewer parameters
LoRA Fine-tuning

Low-Rank Adaptation updates a small number of additional parameters while keeping the original backbone frozen.

Advantages:

Parameter efficient
Maintains pretrained knowledge
Explainable AI Evaluation

To understand model decision-making, we applied:

Grad-CAM

Grad-CAM generates heatmaps highlighting image regions that contribute most to the prediction.

HiResCAM

HiResCAM provides higher-resolution localization of discriminative regions.

The explanations were compared against expert lesion segmentation masks using:

Dice Score
Intersection over Union (IoU)
Pointing Game Accuracy
Results
Classification Performance

Models were evaluated using:

AUROC
Confidence intervals
Calibration performance

Example comparison:

Model	Internal AUROC	External AUROC
DINOv2-Full	0.756	0.920
DINOv2-LoRA	0.758	0.907
Explainability Results

Visualization examples:

Grad-CAM and HiResCAM

(figure add karo)

These methods highlight clinically relevant retinal regions associated with disease prediction, showing alignment with annotated lesions.

Calibration Analysis

Calibration curves were used to evaluate whether predicted probabilities correspond to actual confidence.

A well-calibrated model should produce:

High confidence for correct predictions
Lower confidence for uncertain predictions
Repository Structure
Explainable-DR-Foundation-Models/

├── notebooks/
│   └── retinal_foundation_models.ipynb

├── checkpoints/

├── datasets/

├── results/

├── figures/

├── paper/

└── presentation/
Conclusion

This study demonstrates that foundation vision models can effectively classify retinal diseases while providing interpretable predictions.

Key findings:

DINOv2 achieved strong generalization on external evaluation.
LoRA provides competitive performance with fewer trainable parameters.
XAI methods improve transparency by highlighting clinically meaningful regions.
Future Work

Future improvements include:

Larger multi-center retinal datasets
Vision-language foundation models
Automated lesion-aware training
Clinical validation with ophthalmologists
Improved explainability evaluation methods
