# EV Charging Consumption Analysis & Forecasting — TGSPDCL

A concise end-to-end analysis and forecasting notebook for EV charging consumption in the Telangana Southern Power Distribution Company (TGSPDCL). The work: data ingestion, cleaning, EDA, time-series decomposition, stationarity checks, ARIMA modeling and model comparison are implemented in the main notebook: [`ev_eneryconsumption.ipynb`](ev_eneryconsumption.ipynb).

Why this project is valuable
- Real-world utility dataset (June 2021 → Oct 2025) covering area-level EV charging consumption.
- Clear EDA and visual storytelling (distribution, trends, top areas/circles).
- Time-series pipeline showing transformations, stationarity checks and model selection.
- Forecasting with transparent model comparison and original-scale metrics.

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

What to review for hiring managers
- Reproducibility: clear preprocessing steps and a single notebook that reproduces figures and forecasts.
- Time-series knowledge: decomposition (additive/multiplicative), STL, ADF tests and differencing strategy.
- Model selection: ARIMA grid, AIC/BIC and RMSE comparisons shown in [`ev_eneryconsumption.ipynb`](ev_eneryconsumption.ipynb).
- Communication: concise visualizations and insights accompanying code cells.

Suggested next steps (extensions)
- Add a lightweight CLI or Python script to export forecasts (e.g., forecasts.csv).
- Build cross-validation for time-series (walk-forward).
- Try exponential smoothing (ETS) or Prophet for comparison.
- Deploy a simple dashboard to visualize forecasts and anomalies.

License & Contact
- MIT-style permissive use (add LICENSE if required).
- Review full notebook: [`ev_eneryconsumption.ipynb`](ev_eneryconsumption.ipynb) and source data: [`Data/`](Data/).
