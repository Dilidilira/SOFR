# SOFR Swaption Pricer & Exposure Engine

This project demonstrates pricing and exposure analysis for SOFR swaptions using QuantLib and Python.  The included Jupyter notebook walks through loading market data, building the SOFR curve, calibrating a model, valuing swaptions, and simulating exposures with MonteCarlo Simulations.

## Data

- **OIS_Swaption_Vol_20250725.csv** – swaption normal volatility matrix as of 2025‑07‑25. (Derived from Bloomberg)
- **SOFR_OIS_Fut_data.csv** – SOFR OIS futures and swap rates for several tenors. (Derived from Bloomberg)
 
## Framework and Technical Details

The notebook is organized into four major components:

1. **Curve Construction** – SOFR OIS futures and swaps are converted to rate helpers and stitched into a `PiecewiseLogCubicDiscount` curve that supports extrapolation for long-dated cash flows.
2. **Model Calibration** – A one‑factor Hull–White model is calibrated to the normal volatility surface using a Jamshidian swaption engine and nonlinear least‑squares to fit the mean‑reversion (`a`) and volatility (`σ`) parameters.
3. **Swaption Pricing** – Closed‑form Black‑76 values are compared with Hull–White model prices.  Path‑wise valuation relies on Jamshidian decomposition to handle callability along each simulated path.
4. **Exposure Engine** – Hull‑White short‑rate paths are generated with a `GaussianPathGenerator`.  Each path reprices the swaption and underlying swap. Finally, a list of exposure metrics is generated and visualized.

## Next Steps

The notebook can be extended with scenario analysis, stress testing, or additional risk metrics to support more comprehensive risk management.
