## Prophet-EMD Hybrid Time Series Forecasting and Feature Extraction

This project demonstrates two main workflows for univariate time series analysis:

1. **Hybrid Forecasting**: Combines **Empirical Mode Decomposition (EMD)** and **Prophet** for forecasting.
2. **Feature Extraction**: Extracts advanced features using Python and R, such as chaos detection and seasonal strength metrics.

---

## Project Structure

### Notebook: Prophet-EMD Forecasting and Feature Extraction
- **Data Loading**: Reads multiple CSV files containing time series with columns `ds` (timestamps) and `y` (values).
- **Data Splitting**: Divides the series into training and testing sets with a forecast horizon, typically 12 or 15 months depending on dataset.
- **Chaos Analysis**: Uses the `nolds` package to compute the **Lyapunov exponent**, identifying chaotic behavior.
- **STL Decomposition**: Applies `STL` from `statsmodels` to extract seasonal and trend components.
- **R Feature Extraction**: Integrates with R (via `rpy2`) to run `tsfeatures`, extracting additional statistical features.
- **EMD Forecasting**:
  - Applies **EMD** to decompose the training series into Intrinsic Mode Functions (IMFs).
  - Trains a separate **Prophet** model for each IMF.
  - Aggregates IMF forecasts to produce the final prediction.
- **CEEMDAN Forecasting**:
  - Applies **CEEMDAN** to obtain more refined IMFs.
  - Forecasting logic mirrors the EMD section.
- **ICEEMDAN Forecasting**:
  - Uses precomputed **ICEEMDAN** IMFs obtained from original source implementations.
  - Loads these IMFs from CSV files to ensure consistency and comparability.
  - Fits Prophet models on each IMF and aggregates forecasts.
- **Evaluation**: Calculates **MAPE** and **RMSE** to evaluate the forecast accuracy of all three methods.
- **Visualization**: Generates plots for STL decomposition and forecast comparisons.

---

## Requirements

Install required Python packages:

```bash
pip install numpy==2.2.6 pandas==2.3.1 matplotlib==3.10.5 scipy==1.15.3 scikit-learn==1.7.1 nolds==0.6.2 rpy2==3.6.2 emd-signal==1.6.4 prophet==1.1.7 statsmodels==0.14.5
```

Install **R** and the following R packages:

```R
install.packages(c("tsfeatures", "forecast", "dplyr", "tidyr"))
```

---

## How to Run

1.Place your datasets as CSV files in the ./Datasets/ directory, each containing ds and y columns.
2.Ensure precomputed ICEEMDAN IMFs are available as CSV files in ./iceemdan_imfs/ICEEMDAN/ folder, named {dataset_name}_iceemdan_imf.csv.
3.Run the notebook cells in order:
&emsp; -Chaos and STL analysis
&emsp; -R-based feature extraction
&emsp; -Prophet forecasting using EMD, CEEMDAN, and ICEEMDAN methods
4.Review output metrics, forecasts, and plots saved in ./result/{dataset_name}_result/.
---

## Key Highlights

- **Lyapunov Exponent** detects chaos within time series data.
- **EMD, CEEMDAN, and ICEEMDAN** provide layered decompositions for improved forecasting.
- **Prophet** models are applied individually to each IMF, capturing intrinsic modes effectively.
- **ICEEMDAN IMFs** are sourced from original published methods to ensure reproducibility and benchmark alignment.
- **R** Integration enriches feature extraction with established time series statistical summaries.
- **Evaluation Metrics** include MAPE and RMSE over multi-step forecast horizons

---

## References

- Abbasimehr, H., Behboodi, A., & Bahrini, A. (2023). A novel hybrid model to forecast seasonal and chaotic time series. Expert Systems with Applications, 239, Article 122461.

