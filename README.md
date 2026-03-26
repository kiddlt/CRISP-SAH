```markdown
# CRISP-SAH

**CRISP‑SAH** is an open‑source deep learning framework for early prediction of severe pneumonia (SP) after subarachnoid hemorrhage (SAH) using clinical parameters and CT radiomics.

This repository contains the complete training and inference pipeline built on top of [nnU‑Net v2](https://github.com/MIC-DKFZ/nnUNet).

---

## Requirements

- Python 3.9+
- CUDA 11.8+ (GPU recommended)
- Linux / macOS / Windows (WSL recommended)

---

## Installation

```bash
git clone https://github.com/yourusername/CRISP-SAH.git
cd CRISP-SAH
pip install -r requirements.txt
```

---

## Usage

### 1. Prepare your data

- CT scans in NIfTI format (.nii.gz) or DICOM.
- Clinical data in CSV format with one row per patient, including an identifier column that matches the CT file name.

Organize the data as required by nnU‑Net (see [nnU‑Net documentation](https://github.com/MIC-DKFZ/nnUNet) for details).

### 2. Train the model

```bash
python run_training.py --config config.yaml
```

The configuration file `config.yaml` must specify:

- Paths to nnU‑Net preprocessed and results folders
- Path to clinical CSV
- Training folds, batch size, number of epochs, etc.

### 3. Predict on new cases

```bash
python predict.py \
    --input_ct /path/to/ct.nii.gz \
    --clinical /path/to/clinical.csv \
    --output /path/to/results
```

Outputs include:

- `prediction.csv` – predicted probability of SP
- `shap_plots/` – SHAP explanation for each case

---

## Repository structure

```
CRISP-SAH/
├── crisp_sah/            # Core modules (nnU‑Net integration, radiomics, stacking)
├── config.yaml           # Example configuration
├── run_training.py       # Training entry point
├── predict.py            # Inference entry point
├── requirements.txt
└── README.md
```

---

## License

This project is licensed under the Apache License 2.0 – see the [LICENSE](LICENSE) file for details.
```
