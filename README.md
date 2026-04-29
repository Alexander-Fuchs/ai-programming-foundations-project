# Project 1: AI Programming Foundations

## Project Description

In this project i built a small but complete reproducible data workflow that combines two real climate datasets and walks them through download, cleaning, exploratory analysis, visualization and summary using Python, NumPy, Pandas, Matplotlib and Seaborn in a Jupyter notebook. No machine learning model is trained here, the goal is to set up a clean foundation that the later projects in the MSc can build on.

Datasets used:

- **Berkeley Earth Land + Ocean monthly temperature record** (1850 - present): <https://berkeleyearth.org/data/>
- **NOAA Mauna Loa monthly atmospheric CO₂** (1958 - present): <https://gml.noaa.gov/ccgg/trends/>

The data files are downloaded automatically by the notebook into a local `data/` folder on first run.

## How to Run

1. Clone this repository and `cd` into it.
2. (Recommended) create and activate a virtual environment:

   ```bash
   python3 -m venv .venv
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
