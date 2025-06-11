# 🪫 Battery-PINN — Physics-Informed Capacity-Fade Prediction  
Predicting lithium-ion battery health on the NASA PCoE dataset with a two-stage Physics-Informed Neural Network (PINN).

[![Python](https://img.shields.io/badge/Python-3.11-blue.svg)](#requirements)  
[![PyTorch](https://img.shields.io/badge/PyTorch-2.2%20%7C%20CUDA%2012.3-lightgrey)](#requirements)

---

## ✨ Project Highlights
* **Physics prior ⇒ data efficiency** – embedding a degradation ODE in the loss halves test RMSE versus a data-only MLP.  
* **Rich 26-D feature set** – time-domain stats + FFT descriptors + entropy + charge/time metrics.  
* **One-file reproducibility** – `run.py` executes *end-to-end* (data → features → training → evaluation → figures) in ≈20 min on a single GPU (≈1 h CPU-only).  
* **Paper-ready** – LaTeX report and figures are generated automatically.

---

## 🗂️ Repository Layout
```text
battery-pinn/
├── Battery_Dataset/              
│   ├──   1. BatteryAgingARC-FY08Q4
│   ├──   2. BatteryAgingARC_25_26_27_28_P1
│   ├──   3. BatteryAgingARC_25-44
│   ├──   4. BatteryAgingARC_45_46_47_48
│   ├──   5. BatteryAgingARC_49_50_51_52
│   ├──   6. BatteryAgingARC_53_54_55_56
├── run.ipynb                 # one-shot script that reproduces the paper and adds additional features that improve performance
├── docs/
│   └── paper.pdf          # compiled report (generated)
├── environment.yml        # Conda environment (PyTorch 2.2 | CUDA 12.3)
└── README.md              # ← you are here
```

---

## 🔧 Requirements
| Package    | Version | Notes                                   |
|------------|---------|-----------------------------------------|
| Python     | ≥ 3.10  | developed on 3.11                       |
| PyTorch    | 2.2     | CPU works; GPU (CUDA 12.3) recommended  |
| NumPy      | 1.26    |                                         |
| SciPy      | 1.13    | for `.mat` loading                      |
| pandas     | 2.2     |                                         |
| matplotlib | 3.9     | plotting                                |

```bash
conda env create -f environment.yml
conda activate battery-pinn
```

---

## ⚡ Quick Start (single run)
```bash
# 1 Download NASA data from the GitHub Battery Dataset or the link below(~170 MB)
https://phm-datasets.s3.amazonaws.com/NASA/5.+Battery+Data+Set.zip

# 2 Train + evaluate
Run all blocks of the IPYNB after installing all dependences

# 3 View results
Results will be output inside the Jupyter notebook
```
Expected output:
```
Test RMSE = 0.0091 Ah
Test MAE  = 0.0070 Ah
```
plus loss figures.

---

## 🔍 Detailed Usage

| Argument        | Default              | Description                                       |
|-----------------|----------------------|---------------------------------------------------|
| `--data_dir`    | `Battery_Dataset`   | folder containing NASA `.mat` files               |
| `--epochs`      | `1000`               | training epochs                                   |
| `--batch`       | `256`                | batch size                                        |
| `--lr`          | `1e-3`               | initial learning rate                             |
| `--alpha`       | `1.0`                | weight on PDE residual (`MSE_PDE`)                |
| `--beta`        | `1.0`                | weight on physics residual 

---

## 📜 Citation
```bibtex
@misc{battery_pinn_2025,
  title        = {Physics-Informed Learning for Li-Ion Battery Health
Prediction},
  author       = {Peter Quawas, Nathaniel Greenberg, Arturo Amaya, Anushka Sarode},
  year         = {2025},
}

@misc{Saha2007BatteryData,
  author       = {Saha, B. and Goebel, K.},
  title        = {Battery Data Set},
  year         = {2007},
  howpublished = {\url{https://www.nasa.gov/intelligent-systems-division/discovery-and-systems-health/pcoe/pcoe-data-set-repository/}}
}
```

---

