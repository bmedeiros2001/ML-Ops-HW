# ML-Ops-HW1: Data Versioning for ML with lakeFS and DVC

This repository compares two data versioning platforms — **lakeFS** and **DVC** — using a dataset of athletes. It includes exploratory data analysis, preprocessing, and ML modeling for predicting `total_lift` based on personal and training attributes.

---

## 🔧 Repository Structure

```bash
ML-Ops-HW1/
├── dvc/
│ ├── code_dvc.ipynb
│ ├── athletes.csv
│ ├── athletes.csv.dvc
│ ├── athletes_v1.csv
│ ├── athletes_v1.csv.dvc
│ ├── athletes_v2.csv
│ ├── athletes_v2.csv.dvc
│ └── .gitignore
├── lakefs/
│ ├── code_lakefs.ipynb
│ ├── athletes.csv
│ ├── athletes_main.csv
│ ├── athletes_v1.csv
│ ├── athletes_v2.csv
├── model3_dp.ipynb # Differential Privacy model (TF Privacy)
├── results_platform_comparison.pptx
└── README.md
```
---

## 🚀 lakeFS Workflow (used in `lakefs/code_lakefs.ipynb`)

Each version of the dataset was stored as a branch:
- `main`: original dataset (`athletes_main.csv`)
- `v1`: minimal cleaning + engineered `total_lift`
- `v2`: full cleaning + encoded features

### Terminal Commands Used (lakeFS)

```bash
# Download original dataset from main branch
lakectl fs download \
  lakefs://ml-ops-hw1-athletes/main/athletes_main.csv \
  athletes_main.csv

# Upload cleaned v1
lakectl fs upload \
  lakefs://ml-ops-hw1-athletes/v1/athletes.csv \
  --source athletes_v1.csv

lakectl commit \
  lakefs://ml-ops-hw1-athletes/v1 \
  -m "v1: minimal cleaning + total_lift"

# Upload cleaned v2
lakectl fs upload \
  lakefs://ml-ops-hw1-athletes/v2/athletes.csv \
  --source athletes_v2.csv

lakectl commit \
  lakefs://ml-ops-hw1-athletes/v2 \
  -m "v2: full cleaning + total_lift + region & gender encoding"
  
---
## 📁 DVC Workflow (used in dvc/code_dvc.ipynb)
Versioning done locally using DVC + Git. Each version is tracked using .dvc files:

### Terminal Commands Used (DVC)
```bash
# Initialize DVC
cd /your/project/path/dvc
git init
dvc init

# Track raw dataset
dvc add athletes.csv
git add athletes.csv.dvc .gitignore
git commit -m "Add raw athletes.csv to DVC"

# Track cleaned v1
dvc add athletes_v1.csv
git add athletes_v1.csv.dvc .gitignore
git commit -m "Add athletes_v1.csv: cleaned data for baseline model"

# Track cleaned v2
dvc add athletes_v2.csv
git add athletes_v2.csv.dvc .gitignore
git commit -m "Add athletes_v2.csv: further cleaning of the data (v2)"```

---

## 📊 Modeling Overview
- Model 1: Trained on minimally cleaned data (v1)
- Model 2: Trained on fully cleaned & encoded data (v2)
- Model 3: Differential Privacy (DP-SGD) model using TensorFlow Privacy, trained on v2

File names and explanation: 
- **code_lakefs.ipynb:** Model 1 and 2 (+ Lake FS terminal commands commented out)
- **code_dvc.ipynb:** Model 1 and 2 (+ DVC terminal commands commented out). Same results as **code_lakefs.ipynb**
- **model3_dp.ipynb:** Model 3 (DP)

---

## 📈 Results & Comparison
See results_platform_comparison.pptx for a side-by-side comparison of model performance across versions

---
##  Notes
- The .env file and virtual environment folder (tfdp_env/) are excluded and should not be committed.
- Credentials for lakeFS are not included for security reasons. Environment variables were loaded via dotenv.

