# Wind speed forecasting – Tibau

Next-hour wind speed forecast from the previous 24 hours of measurements, using a two-layer LSTM.

**Data:** `tibau_wind_data.csv` – hourly wind speed [m/s] and direction [°], March 2020 onwards.

**What's in the notebook**
- gap filling, wind direction encoded as sin/cos (so 359° and 1° are close)
- 24-hour sliding windows, chronological 70/15/15 split, scaler fitted on training data only
- LSTM (64 → 32 units) with early stopping
- comparison against a persistence forecast (next hour = current hour)

**Results (test period)**

| Model | MAE [m/s] | RMSE [m/s] |
|---|---|---|
| Persistence | 0.251 | 0.333 |
| **LSTM (24 h look-back)** | **0.160** | **0.215** |

The LSTM cuts the error by about a third compared with persistence. My first version, which only saw 1 timestep, was
actually slightly *worse* than persistence. Using a full day of history made the difference. Next step: a 6–24 h
horizon, which is what grid operators and traders plan on.

**Run it:** open `Wind_Energy_Forecasting.ipynb` in Jupyter or Colab, with the CSV next to it.
`pip install pandas scikit-learn matplotlib tensorflow`

*University group project (Group B), M.Sc. Smart Energy Systems.*
