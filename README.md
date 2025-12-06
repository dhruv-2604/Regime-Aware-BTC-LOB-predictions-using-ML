# Regime-Aware Order Book Toxicity & Short-Horizon Prediction

## Directory Structure

```
4641-Group80-Project/
├── README.md                 # This file - project documentation
├── RegimeAware_LOB.ipynb     # Main Jupyter notebook with complete ML pipeline
├── BTC_1sec.csv              # Dataset (not in repo - download separately)
├── requirements.txt          # Python dependencies for pip
├── environment.yml           # Conda environment specification
├── Gantt Chart.xlsx          # Project timeline
└── Contribution_Table.png    # Team contribution breakdown
```

## File Descriptions

### Core Files

| File | Description |
|------|-------------|
| **RegimeAware_LOB.ipynb** | Main Jupyter notebook containing the complete ML pipeline: data loading, feature engineering (26 features), PCA dimensionality reduction, HMM-based regime discovery, supervised learning (Logistic Regression and XGBoost), walk-forward validation, and result visualization. |
| **BTC_1sec.csv** | High-frequency cryptocurrency limit order book data (1-second intervals, ~1M rows, 1.67GB). **Not included in repository due to size.** Download from [Kaggle](https://www.kaggle.com/datasets/martinsn/high-frequency-crypto-limit-order-book-data). |

### Configuration Files

| File | Description |
|------|-------------|
| **requirements.txt** | Python package dependencies. Install via `pip install -r requirements.txt`. |
| **environment.yml** | Conda environment specification. Create via `conda env create -f environment.yml`. |
| **.gitignore** | Specifies files excluded from version control (e.g., large CSV files, cache). |

### Documentation Files

| File | Description |
|------|-------------|
| **README.md** | Project overview, setup instructions, and results summary (this file). |
| **Gantt Chart.xlsx** | Project timeline showing task allocation and milestones. |
| **Contribution_Table.png** | Team member contributions breakdown. |

## Setup Instructions

1. Clone the repository:
   ```bash
   git clone https://github.gatech.edu/zghazanfar9/4641-Group80-Project.git
   cd 4641-Group80-Project
   ```

2. Install dependencies (choose one):
   ```bash
   # Option A: pip
   pip install -r requirements.txt

   # Option B: conda
   conda env create -f environment.yml
   conda activate lob-regime
   ```

3. Download the dataset from [Kaggle](https://www.kaggle.com/datasets/martinsn/high-frequency-crypto-limit-order-book-data) and place `BTC_1sec.csv` in the project root directory.

4. Run the notebook:
   ```bash
   jupyter notebook RegimeAware_LOB.ipynb
   ```

## Methodology

### Algorithms Used (3 distinct methods)
1. **Hidden Markov Model (HMM)** - Unsupervised regime discovery
2. **Logistic Regression** - Supervised linear classification
3. **XGBoost** - Supervised gradient boosting

### Key Configuration
- **Classification**: Binary (Up vs Down), 2 bp threshold
- **Features**: 26 microstructure features (depth, imbalances, flows, volatility, momentum)
- **Dimensionality Reduction**: PCA retaining 95% variance (26 -> ~12-15 components)
- **Validation**: Walk-forward with 3-day training, 4-hour test, 60s embargo, 12-hour stride

## Key Results

| Metric | Value |
|--------|-------|
| Random Baseline | 50% |
| Logistic Regression Accuracy | 57.43% (baseline) / 57.45% (+regime) |
| XGBoost Accuracy | 57.77% (baseline) / 57.80% (+regime) |
| Balanced Regime Hit Rate | 58.3% |
| Toxic Regime Hit Rate | 57.0% |
| Lift | -1.3% |

### Hypothesis Evaluation

Our hypothesis that toxic market regimes would be more predictable than balanced regimes was **not supported**. We observed a slight negative lift of -1.3%, with balanced regimes showing marginally higher hit rates (58.3%) than toxic regimes (57.0%).

The HMM-derived regime feature contributed only 3.45% to model importance, suggesting that the regime signal provides minimal additional predictive value beyond what PCA components already capture.

### Interpretation

This null result suggests that:
1. The toxic/balanced regime distinction does not strongly affect predictability in our dataset
2. PCA dimensionality reduction may already implicitly capture regime-related information
3. Both regime types achieve similar accuracy (~57-58%), well above the 50% random baseline

While the regime-awareness hypothesis was not validated, the supervised models still achieve meaningful predictive performance on this high-frequency trading task.
