
# CRISP-SAH

**CRISP‑SAH** is an open‑source deep learning framework for early prediction of severe pneumonia (SP) after subarachnoid hemorrhage (SAH) using clinical parameters and CT radiomics.

This repository contains the complete training and inference pipeline built on top of [nnU‑Net v2](https://github.com/MIC-DKFZ/nnUNet).


The code is responsible for:
- Loading medical image data and associated clinical labels
- Applying data augmentation (spatial, intensity, cascaded augmentations)
- Training a segmentation network (2D/3D U‑Net) with deep supervision
- Managing distributed training (DDP), learning rate scheduling, and logging
- Performing validation and checkpointing

This module is designed to be used as part of the larger CRISP‑SAH pipeline, where the trained segmentation model is later used for radiomics feature extraction and final risk prediction.



## 🧩 File Overview

- `crisp_sah/trainer.py` – Contains the `nnUNetTrainer` class that inherits from the nnU‑Net v2 trainer and adds CRISP‑SAH‑specific adaptations (if any).
- The class is fully compatible with the nnU‑Net data structure and configuration files (`plans.json`, `dataset.json`, etc.).



## 📦 Dependencies

The code requires the following Python packages (see `requirements.txt` for full list):

- `torch` (>=2.0)
- `nnunetv2`
- `batchgenerators`, `batchgeneratorsv2`
- `numpy`, `scipy`, `pandas`
- `scikit‑learn`, `matplotlib`, `shap`

All dependencies are automatically installed with the main CRISP‑SAH installation.



## 🚀 Usage

### Training a model

To train a model using this trainer, you need a **nnU‑Net dataset** (preprocessed with `nnUNetv2_plan_and_preprocess`). Then run:

```
python -m nnunetv2.training.run_training \
    --dataset_name DATASET_NAME \
    --configuration CONFIG \
    --fold FOLD \
    --trainer nnUNetTrainer
Replace DATASET_NAME, CONFIG (e.g., 2d, 3d_fullres), and FOLD (0‑4 or all) accordingly.
```
### Continuing training from a checkpoint
```
python -m nnunetv2.training.run_training \
    --dataset_name DATASET_NAME \
    --configuration CONFIG \
    --fold FOLD \
    --trainer nnUNetTrainer \
    --c /path/to/checkpoint.pth
```
    
###  Running validation only
```
python -m nnunetv2.training.run_training \
    --dataset_name DATASET_NAME \
    --configuration CONFIG \
    --fold FOLD \
    --trainer nnUNetTrainer \
    --val

```

---

## License

This project is licensed under the Apache License 2.0 – see the [LICENSE](LICENSE) file for details.
```
