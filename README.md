# Project 1: AI Programming Foundations

## Project Description

In this project i built a small but complete reproducible data workflow that combines two real climate datasets and walks them through download, cleaning, exploratory analysis, visualization and summary using Python, NumPy, Pandas, Matplotlib and Seaborn in a Jupyter notebook. No machine learning model is trained here, the goal is to set up a clean foundation that the later projects in the MSc capstone can build on.

Datasets used:

- **Berkeley Earth Land + Ocean monthly temperature record** (1850 - present): <https://berkeleyearth.org/data/>
- **NOAA Mauna Loa monthly atmospheric CO₂** (1958 - present): <https://gml.noaa.gov/ccgg/trends/>

The data files are downloaded automatically by the notebook into a local `data/` folder on first run.

## How to Run

This project was developed and tested with **Python 3.12**.

1. Clone this repository and `cd` into it.
2. (Recommended) create and activate a virtual environment:

   ```bash
   python -m venv .venv
   source .venv/bin/activate
   ```

3. Install the dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Open `data_workflow.ipynb` in Jupyter (or VS Code / Cursor) and run all cells from top to bottom.

## Requirements

The exact package versions used to produce the notebook are pinned in `requirements.txt`. To install them, or to regenerate the file from your own environment after adding a package:

```bash
pip install -r requirements.txt
pip freeze > requirements.txt
```

## Responsible Practice (Bias and Data Quality)

A few things in this dataset could mislead a reader if i did not handle them explicitly:

- **Anomalies, not absolute temperatures.** Values like `+1.5` mean "1.5 °C above the 1951 - 1980 average", not "1.5 °C absolute". Every plot axis says so, and section 3.1 of the notebook gives the absolute baseline (≈ 14.10 °C).
- **The 1940s bump.** The small spike around 1940 in Figure 1 is mostly a wartime SST measurement artifact, not a real warm period. Berkeley Earth corrects most of it but not all.
- **Sparse 19th-century coverage.** Far fewer stations were reporting before 1900, so the uncertainty band is wider there. Trends drawn from that era alone are not trustworthy on their own.
- **CO₂ from one place.** Mauna Loa is a good global proxy because the air mixes well at that altitude, but it is still one point on the planet. The 7-month gap (Nov 2022 - Jul 2023) when measurements came from nearby Maunakea is marked on Figure 2.
- **Global means hide regional differences.** These two datasets cannot say anything about the Arctic warming faster than the tropics, for example. That is a real limit of using global aggregates.

Poor cleaning here would not flip the climate signal, but it could make it look bigger than it is (artifacts read as warming) or be misread (anomalies as absolute temperatures), so the notebook tries to make every such choice visible.

## Future Integration Reflections

This project is the first of eight in the MSc capstone, so the workflow is built modular on purpose so later projects can extend it.

**ML workflow changes.** For a classical ML version (say, predict next-month anomaly from CO₂ and prior anomalies) i would add a time-aware train/test split (no random shuffling on a time series), some lagged features, scaling for distance-based models, a simple baseline to beat (next month = this month), and proper regression metrics like RMSE and MAE. The download, clean and merge functions can be reused as is.

**Neural network preparation.** For a deep learning version (LSTM or 1D-CNN), the data would be reshaped into fixed-length input windows, normalized to a common scale, and batched for GPU training. Random seeds would be pinned, the train/val/test split would stay time-ordered to avoid look-ahead leakage, and i would track loss curves on both splits.

**Agentic automation potential.** An agent could automate the chores: scheduled monthly re-runs that pull fresh data, anomaly detection that flags an unusually large month-over-month jump, automated regeneration of figures and the summary, and a freshness check that warns if an upstream source has not updated. Further out, an agent could draft the report narrative from the figures and test results with a human only editing.
