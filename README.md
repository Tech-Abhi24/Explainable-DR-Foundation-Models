# Explainable Diabetic Retinopathy Classification using Vision Foundation Models

This repository contains the implementation of our MSc research project on **Explainable Diabetic Retinopathy Classification** using **Vision Foundation Models**.

The project evaluates **DINOv2**, **CLIP**, and **Vision Transformer (ViT)** using three different fine-tuning strategies (**Full Fine-tuning, Linear Probing, and LoRA**) and validates explainability using **Grad-CAM** and **HiResCAM**.

---

# Authors

- **Abhishek Verma**
- **Anila Krishna**
- **Abhishek Gajanan Bankar**


**Supervisor:** Prof. Dr. Nils Strodthoff
**Supervisor:** Prof. Dr. rer. nat. Juan Lopez Alcaraz

**Carl von Ossietzky University of Oldenburg**

---

# Repository Structure

```text
Retinal-Disease-XAI/
│
├── notebook/
│   └── retinal_project.ipynb
│
├── checkpoints/
│
├── paper/
│   └── Final_Paper.pdf
│
├── presentation/
│   └── Final_Presentation.pdf
│
├── results/
│
├── assets/
│
├── requirements.txt
├── README.md
├── LICENSE
└── .gitignore
```

---

# Features

- ✅ Binary Diabetic Retinopathy Classification
- ✅ Patient-wise Train/Validation/Test Split
- ✅ Three Vision Foundation Models
- ✅ Nine Fine-tuning Configurations
- ✅ External Validation on APTOS
- ✅ Explainability using Grad-CAM
- ✅ Explainability using HiResCAM
- ✅ Quantitative XAI Validation
- ✅ Calibration using Isotonic Regression
- ✅ Bootstrap 95% Confidence Intervals
- ✅ Automatic Checkpoint Loading

---

# Models

| Backbone | Full | Linear | LoRA |
|----------|:----:|:------:|:----:|
| DINOv2 | ✅ | ✅ | ✅ |
| CLIP | ✅ | ✅ | ✅ |
| Vision Transformer | ✅ | ✅ | ✅ |

**Total Models:** **9**

---

# Datasets

| Dataset | Purpose | Images |
|---------|---------|-------:|
| **ODIR** | Training + Internal Testing | **12,784** |
| **APTOS 2019** | External Testing | **366** |
| **IDRiD Segmentation** | XAI Validation | **54** |

---

# Training Pipeline

```text
ODIR Dataset
      │
      ▼
Patient-wise Split
      │
      ▼
Data Augmentation
      │
      ▼
Foundation Model
      │
      ▼
Binary Classification
      │
      ▼
Evaluation
      │
      ▼
Calibration
      │
      ▼
Explainability
      │
      ▼
Grad-CAM / HiResCAM
      │
      ▼
Dice • IoU • Pointing Game
```

---

# Data Augmentation

Training images were augmented using:

- Resize
- Horizontal Flip
- Vertical Flip
- Random Rotation
- Color Jitter

Validation and test images used deterministic preprocessing only.

---

# Evaluation Metrics

- **AUROC**
- **Bootstrap 95% Confidence Interval**
- **Internal Evaluation**
- **External Evaluation**
- **Calibration AUROC**

---

# Explainability

Two explainability techniques were evaluated:

- **Grad-CAM**
- **HiResCAM**

The generated attention maps were quantitatively validated using expert lesion masks from the **IDRiD Segmentation Dataset**.

Evaluation metrics:

- Dice Score
- Intersection over Union (IoU)
- Pointing Game Accuracy

---

# Main Results

- **DINOv2 achieved the strongest overall performance.**
- **LoRA achieved competitive performance with significantly fewer trainable parameters.**
- **External validation demonstrated good generalization across datasets.**
- **Grad-CAM and HiResCAM highlighted clinically relevant retinal lesion regions.**

---

# Installation

```bash
git clone https://github.com/your-username/Explainable-DR-Foundation-Models.git

cd Explainable-DR-Foundation-Models

pip install -r requirements.txt
```

---

# Running the Project

Open:

```text
notebook/retinal_project.ipynb
```

Run all notebook cells sequentially.

If pretrained checkpoints are available inside the **checkpoints/** directory, they will be loaded automatically.

---

# Checkpoints

Filenames:

- ckpt_dinov2_full.pth
- ckpt_dinov2_linear.pth
- ckpt_dinov2_lora.pth
- ckpt_clip_full.pth
- ckpt_clip_linear.pth
- ckpt_clip_lora.pth
- ckpt_vit_full.pth
- ckpt_vit_linear.pth
- ckpt_vit_lora.pth

---

## Pretrained Checkpoints

Due to GitHub file size limitations, pretrained checkpoints are hosted externally.

Download:

Google Drive:(https://drive.google.com/drive/u/0/folders/17g9pLrwz_A7ZCgStMZGiEhUe_7jCaUsy)

After downloading just run the entire code.

---

# Acknowledgements

We sincerely thank **Prof. Dr. Nils Strodthoff**  **Prof. Dr. rer. nat. Juan Lopez Alcaraz** for their continuous guidance, valuable feedback, and regular consultations throughout this project. Their support significantly improved both the implementation and the scientific quality of this work.

We also acknowledge the authors of the **ODIR**, **APTOS 2019**, and **IDRiD** datasets for making these valuable resources publicly available.

---

# License

This project is intended for **academic and research purposes**.
