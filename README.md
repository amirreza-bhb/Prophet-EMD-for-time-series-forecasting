## Prophet-EMD Hybrid Time Series Forecasting and Feature Extraction

This project demonstrates two main workflows for univariate time series analysis:

1. **Hybrid Forecasting**: Combines **Empirical Mode Decomposition (EMD)** and **Prophet** for forecasting.
2. **Feature Extraction**: Extracts advanced features using Python and R, such as chaos detection and seasonal strength metrics.

---

## Project Structure

### Notebook: Prophet-EMD Forecasting and Feature Extraction
- **Data Loading**: Reads a CSV file containing a time series with columns `ds` (timestamps) and `y` (values).
- **Data Splitting**: Divides the series into training and testing sets with a forecast horizon (`test_size = 12`).
- **Chaos Analysis**: Uses the `nolds` package to compute the **Lyapunov exponent**, identifying chaotic behavior.
- **STL Decomposition**: Applies `STL` from `statsmodels` to extract seasonal and trend components.
- **R Feature Extraction**: Integrates with R (via `rpy2`) to run `tsfeatures`, extracting additional statistical features.
- **EMD Forecasting**:
  - Applies **EMD** to decompose the training series into IMFs.
  - Trains a separate **Prophet** model for each IMF.
  - Aggregates IMF forecasts to produce the final prediction.
- **CEEMDAN Forecasting** *(optional)*:
  - Applies **CEEMDAN** to obtain more refined IMFs.
  - Forecasting logic mirrors the EMD section.
- **Evaluation**: Calculates **MAPE** and **RMSE** to evaluate the forecast accuracy.

---

## Requirements

Install required Python packages:

```bash
pip install pandas numpy matplotlib scikit-learn prophet PyEMD nolds statsmodels rpy2
```

> **Note**: Prophet requires `pystan`. Install it first:
```bash
pip install pystan==2.19.1.1
pip install prophet
```

Install **R** and the following R packages:

```R
install.packages(c("tsfeatures", "forecast", "dplyr", "tidyr"))
```

---

## How to Run

1. Replace `#path/to/dataset` in the notebook with your CSV file path.
2. Ensure the CSV includes two columns:
   - `ds`: Date or timestamp
   - `y`: Time series values
3. Execute the notebook cells in sequence:
   - First: Chaos and STL analysis
   - Then: Feature extraction via R
   - Finally: EMD/CEEMDAN + Prophet forecasting and evaluation
4. Review output metrics and plots.

---

## Key Highlights

- **Lyapunov Exponent** helps detect chaos in the time series.
- **EMD & CEEMDAN** break the series into meaningful intrinsic components.
- **Prophet** is run independently on each IMF to model trends and seasonality.
- **Feature Extraction** leverages R's rich ecosystem (`tsfeatures`) and Python libraries.
- **Evaluation** uses test data to compute MAPE and RMSE over a 12-step forecast horizon.

---

## References

- Abbasimehr, H., Behboodi, A., & Bahrini, A. (2023). A novel hybrid model to forecast seasonal and chaotic time series. Expert Systems with Applications, 239, Article 122461.
