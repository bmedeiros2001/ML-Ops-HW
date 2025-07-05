# ML-Ops-HW1 · Data Versioning with lakeFS and DVC

This project compares two data-versioning tools—**lakeFS** and **DVC**—for managing dataset evolution in a machine-learning workflow. Using an athletes dataset, the notebooks cover EDA, cleaning, feature engineering, model training, and a differentially-private (DP-SGD) model.

---

## Repository Structure

```text
ML-Ops-HW1/
├── dvc/
│   ├── code_dvc.ipynb
│   ├── athletes.csv.dvc
│   ├── athletes_v1.csv.dvc
│   ├── athletes_v2.csv.dvc
│   └── .gitignore
├── lakefs/
│   ├── code_lakefs.ipynb
│   ├── athletes.csv
│   ├── athletes_main.csv
│   ├── athletes_v1.csv
│   └── athletes_v2.csv
├── model3_dp.ipynb
├── results_platform_comparison.pptx
└── README.md
```

---

## lakeFS Workflow

Implemented in `lakefs/code_lakefs.ipynb`

### Branches

| Branch | Purpose |
|--------|---------|
| `main` | Raw dataset (athletes_main.csv) |
| `v1` | Minimal cleaning + total_lift feature |
| `v2` | Full cleaning + encoded categorical features |

### Commands Used (lakectl)

```bash
# Download original data
lakectl fs download \
  lakefs://ml-ops-hw1-athletes/main/athletes_main.csv \
  athletes_main.csv

# Save v1
lakectl fs upload \
  lakefs://ml-ops-hw1-athletes/v1/athletes.csv \
  --source athletes_v1.csv
lakectl commit \
  lakefs://ml-ops-hw1-athletes/v1 \
  -m "v1: minimal cleaning + total_lift"

# Save v2
lakectl fs upload \
  lakefs://ml-ops-hw1-athletes/v2/athletes.csv \
  --source athletes_v2.csv
lakectl commit \
  lakefs://ml-ops-hw1-athletes/v2 \
  -m "v2: full cleaning + encoding"
```

---

## DVC Workflow

Implemented in `dvc/code_dvc.ipynb`

```bash
# Initialize
cd dvc
git init
dvc init

# Track raw dataset
dvc add athletes.csv
git add athletes.csv.dvc .gitignore
git commit -m "Add raw athletes.csv to DVC"

# Track v1
dvc add athletes_v1.csv
git add athletes_v1.csv.dvc
git commit -m "Add athletes_v1.csv (minimal cleaning)"

# Track v2
dvc add athletes_v2.csv
git add athletes_v2.csv.dvc
git commit -m "Add athletes_v2.csv (full cleaning)"
```

---

## Models

| File | Description |
|------|-------------|
| `code_lakefs.ipynb` | Models 1 & 2 with lakeFS workflow |
| `code_dvc.ipynb` | Models 1 & 2 replicated with DVC |
| `model3_dp.ipynb` | Model 3: DP-SGD using TensorFlow Privacy |

### Model Details

- **Model 1:** Random Forest on v1
- **Model 2:** Random Forest on v2  
- **Model 3:** DP-SGD (TF Privacy) on v2

Performance and tooling comparisons are summarized in `results_platform_comparison.pptx`.
