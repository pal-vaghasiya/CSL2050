# 🔬 CERN CMS Dielectron Collision Data — Analysis Suite

**Dataset**: 100,000 dielectron events from the CERN CMS detector (LHC, 2010)  
**Source**: [CERN Open Data Portal](https://opendata.cern.ch/record/304) via [Kaggle](https://www.kaggle.com/datasets/fedesoriano/cern-electron-collision-data)

---

## 📦 Package Requirements

### Python Version
```
Python >= 3.9
```

### Required Libraries

| Package | Version | Purpose |
|---|---|---|
| `kagglehub` | >= 0.3.0 | Downloading the CERN dielectron dataset from Kaggle |
| `pandas` | >= 1.5.0 | Data loading, manipulation, and tabular analysis |
| `numpy` | >= 1.23.0 | Numerical computation and array operations |
| `matplotlib` | >= 3.6.0 | Plotting histograms, scatter plots, and bar charts |
| `seaborn` | >= 0.12.0 | Heatmaps and statistical visualisations |
| `scikit-learn` | >= 1.2.0 | Preprocessing, PCA, Linear Regression, cross-validation, and metrics |
| `torch` (PyTorch) | >= 2.0.0 | GPU-accelerated MLP neural network (NB2, NB3, NB5) |
| `shap` | >= 0.42.0 | Installed as a dependency; available for feature importance extension |

### Install All at Once

```bash
pip install kagglehub pandas numpy matplotlib seaborn scikit-learn torch shap
```

> **Note — PyTorch GPU support**: The MLP notebooks automatically detect and use a CUDA GPU if available. If you are running locally without a GPU, training will fall back to CPU (slower but fully functional). For free GPU access, use **Google Colab** or **Kaggle Notebooks** — both have PyTorch and CUDA pre-installed.

---

## 🗂️ Notebook Overview

| File | Task |
|---|---|
| `NB1_EDA.ipynb` | Exploratory Data Analysis |
| `NB2_InvariantMass.ipynb` | Invariant Mass Determination (Formula → PCA → Linear Regression → MLP) |
| `NB3_SensorCost.ipynb` | Sensor Cost vs Accuracy Tradeoff |
| `NB4_Redundancy.ipynb` | Sensor Redundancy Analysis |
| `NB5_CrossValidation.ipynb` | K-Fold Cross Validation |

Each notebook is **fully self-contained** — the first code cell in every notebook handles all installs, imports, data downloading, and preprocessing automatically. You can run any notebook independently.

---

## 🚀 Run Instructions

### Option A — Google Colab (Recommended)

This is the easiest route and gives you free GPU access for the MLP notebooks.

1. Go to [https://colab.research.google.com](https://colab.research.google.com)
2. Click **File → Upload notebook**
3. Upload the notebook you want to run (e.g., `NB2_InvariantMass.ipynb`)
4. *(Recommended for NB2, NB3, NB5)* Enable GPU:  
   **Runtime → Change runtime type → Hardware accelerator → T4 GPU → Save**
5. Click **Runtime → Run all** (or press `Ctrl + F9`)

The Setup cell at the top of each notebook will automatically install `kagglehub` and download the dataset on first run — no manual data download needed.

---

### Option B — Kaggle Notebooks

1. Go to [https://www.kaggle.com/code](https://www.kaggle.com/code) and click **New Notebook**
2. Click **File → Import Notebook** and upload the `.ipynb` file
3. Enable GPU: **Session options (⚙️) → Accelerator → GPU P100**
4. Click **Run All**

> All packages (`kagglehub`, `torch`, `sklearn`, etc.) are pre-installed in the Kaggle environment — no extra installation steps required.

---

### Option C — Local Machine (Jupyter)

**Step 1 — Download the notebooks**

Place all five `.ipynb` files in the same folder:
```
cern-analysis/
├── NB1_EDA.ipynb
├── NB2_InvariantMass.ipynb
├── NB3_SensorCost.ipynb
├── NB4_Redundancy.ipynb
└── NB5_CrossValidation.ipynb
```

**Step 2 — Create a virtual environment** *(recommended)*
```bash
python -m venv cern-env
source cern-env/bin/activate        # macOS / Linux
cern-env\Scripts\activate           # Windows
```

**Step 3 — Install all dependencies**
```bash
pip install kagglehub pandas numpy matplotlib seaborn scikit-learn torch shap jupyter
```

**Step 4 — Configure Kaggle API credentials** *(required for dataset auto-download)*

`kagglehub` uses your Kaggle API key to download the dataset automatically on first run.

1. Log in to [https://www.kaggle.com](https://www.kaggle.com)
2. Go to **Settings → API → Create New Token** — this downloads `kaggle.json`
3. Place the file in the correct location:
   ```
   macOS / Linux:  ~/.kaggle/kaggle.json
   Windows:        C:\Users\<YourName>\.kaggle\kaggle.json
   ```
4. Set file permissions (macOS/Linux only):
   ```bash
   chmod 600 ~/.kaggle/kaggle.json
   ```

**Step 5 — Launch Jupyter and open a notebook**
```bash
jupyter notebook
```
Then open any of the five notebooks in your browser. The dataset will be downloaded automatically when the Setup cell runs.

**Step 6 — Run the notebook**

- Run all cells at once: **Kernel → Restart & Run All**
- Or step through cells one at a time: `Shift + Enter`

---

## ▶️ Recommended Run Order

While each notebook is fully independent, running them in this sequence gives the best conceptual flow:

```
NB1_EDA  →  NB2_InvariantMass  →  NB3_SensorCost  →  NB4_Redundancy  →  NB5_CrossValidation
```

---

## ⚠️ Common Issues & Fixes

| Issue | Fix |
|---|---|
| `kagglehub` download fails | Ensure `kaggle.json` is correctly placed and valid (see Step 4 above) |
| `ModuleNotFoundError: torch` | Run `pip install torch` or switch to a Colab GPU runtime |
| `CUDA out of memory` | Reduce `batch_size` in the MLP cell (e.g., from `512` to `256`) |
| Slow MLP training on CPU | Enable GPU on Colab/Kaggle, or reduce `max_iter` (e.g., from `500` to `150`) |
| `seaborn-v0_8-darkgrid` style error | Upgrade seaborn: `pip install --upgrade seaborn` |
