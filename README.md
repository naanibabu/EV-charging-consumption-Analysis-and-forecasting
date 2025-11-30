# EV Charging Consumption Analysis & Forecasting — TGSPDCL

A concise end-to-end analysis and forecasting notebook for EV charging consumption in the Telangana Southern Power Distribution Company (TGSPDCL). The work: data ingestion, cleaning, EDA, time-series decomposition, stationarity checks, ARIMA modeling and model comparison are implemented in the main notebook: [`ev_eneryconsumption.ipynb`](ev_eneryconsumption.ipynb).

Why this project is valuable
- Real-world utility dataset (June 2021 → Oct 2025) covering area-level EV charging consumption.
- Clear EDA and visual storytelling (distribution, trends, top areas/circles).
- Time-series pipeline showing transformations, stationarity checks and model selection.
- Forecasting with transparent model comparison and original-scale metrics.

Summary
- Period: Data covers June 2021 → October 2025 (monthly, area-level).
- Rows: ~9k records after cleaning.
- Cleaning steps:
  - Filled NaNs in `billdservices` with 0 (`data['billdservices'] = data['billdservices'].fillna(0)`).
  - Removed rows with negative `units` (12 rows) via `data = data[data['units'] >= 0].copy()`.
  - Dropped constant columns `catdesc`, `catcode` and helper `source_file`.
  - Created monthly Date column: `data['Date'] = pd.to_datetime(data[['Year','Month']].assign(Day=1))`.
- EDA highlights:
  - Units and load are right‑skewed with clear growth over time.
  - Top areas/circles identified using groupby sums and bar plots.
  - Units, load and services correlate when aggregated monthly.
- Time‑series analysis:
  - Series constructed as monthly aggregated units [`ts`](ev_eneryconsumption.ipynb).
  - Log transform + second differencing used: `ts_log = np.log(ts)` and `ts_diff = ts_log.diff().diff().dropna()`.
  - Stationarity confirmed on differenced log series via ADF (p < 0.05).
  - ACF/PACF analysis suggested MA(1) and AR(2) components for the transformed series.
- Model selection & results:
  - Models compared: $(2,2,1), (1,2,1), (2,2,0), (0,2,1)$ fitted on `train_data` and evaluated on `test_data`.
  - Best by AIC/BIC: $ARIMA(2,2,0)$.
  - Best by RMSE (original scale): $ARIMA(0,2,1)$.
  - Example reported metrics (one fit): AIC: -35.16, BIC: -31.59, RMSE (log): 0.1516, RMSE (original): 171011.59 (see notebook outputs).
- Conclusion:
  - Growth in EV charging consumption is strong and accelerating → forecasting requires transformations and careful model validation.
  - $ARIMA(0,2,1)$ (MA(1) on twice-differenced log series) produced the lowest RMSE on the test split in this analysis, while $ARIMA(2,2,0)$ was favored by information criteria.


Quick highlights
- Data: stored in the repository under the `Data/` folder — e.g. [`Data/ev_charging_6_2021.csv`](Data/ev_charging_6_2021.csv).
- Notebook entrypoint: [`ev_eneryconsumption.ipynb`](ev_eneryconsumption.ipynb).
- Key variables used in analysis: [`ts`](ev_eneryconsumption.ipynb), [`ts_log`](ev_eneryconsumption.ipynb), [`train_data`](ev_eneryconsumption.ipynb), [`results`](ev_eneryconsumption.ipynb).
- Best ARIMA selected in the notebook: $ARIMA(0,2,1)$ (simple MA(1) on twice-differenced log series).

Getting started (local)
1. Clone the repo and open in VS Code or Jupyter.
2. Install minimal dependencies:
   pip install numpy pandas matplotlib seaborn statsmodels scikit-learn jupyter
3. Open and run: [`ev_eneryconsumption.ipynb`](ev_eneryconsumption.ipynb). The notebook walks from data loading to model evaluation.






