# Regime-Aware Order Book Toxicity & Short-Horizon Prediction

## Project Structure

### Files

**RegimeAware_LOB.ipynb**: Main Jupyter notebook containing the complete ML pipeline for regime-aware order book analysis and price prediction. Includes data loading, feature engineering, PCA dimensionality reduction, HMM-based regime discovery, supervised learning models (Logistic Regression and XGBoost), walk-forward validation, and performance visualization.

**requirements.txt**: Python package dependencies required to run the project. Install via `pip install -r requirements.txt`.

**environment.yml**: Conda environment specification for reproducible setup. Create environment via `conda env create -f environment.yml`.

**BTC_1sec.csv**: High-frequency cryptocurrency limit order book data (1-second intervals) from Kaggle. Not included in repository due to size (1.67GB). Download from: https://www.kaggle.com/datasets/martinsn/high-frequency-crypto-limit-order-book-data

## Setup Instructions

1. Clone the repository
2. Install dependencies: `pip install -r requirements.txt` or `conda env create -f environment.yml`
3. Download `BTC_1sec.csv` from the Kaggle link above and place in the project root directory
4. Run `RegimeAware_LOB.ipynb`

## Key Results

- **Overall Accuracy**: ~39.6% (vs 33.3% random baseline)
- **Balanced Regime Hit Rate**: 38.8%
- **Toxic Regime Hit Rate**: 44.8%
- **Lift**: +6.0% (validates hypothesis that toxic regimes are more predictable)
