# MSc in AI Capstone #1: AI Programming Foundations Project

## Project Description

This project builds a complete, reproducible data workflow around the NYC Airbnb Open Data dataset. It loads the raw listing data, cleans it, explores pricing and availability patterns,
and visualizes the key relationships between price, room type, and borough.

## What Was Built

- `data_workflow.ipynb` — a Jupyter Notebook containing the full workflow: setup, data ingestion, missing-value/duplicate/outlier inspection, data cleaning functions, an exploratory
  analysis function, three (plus one bonus) labeled visualizations with interpretations, and a final summary.
- `requirements.txt` — the Python dependencies needed to run the notebook.
- `module_summary.pdf` — a written summary with academic citations (see separate report).

## Dataset

**NYC Airbnb Open Data** (New York City Airbnb listings — pricing and listing characteristics)
Source: [Kaggle — New York City Airbnb Open Data](https://www.kaggle.com/datasets/dgomonov/new-york-city-airbnb-open-data)
File used: `AB_NYC_2019.csv`

## How to Run the Project

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

(If you set up your own environment instead, regenerate this file with: `pip freeze > requirements.txt`)

### 2. Get the dataset

Download `AB_NYC_2019.csv` from the [Kaggle dataset page](https://www.kaggle.com/datasets/dgomonov/new-york-city-airbnb-open-data) and place it in the same folder as `data_workflow.ipynb`.

### 3. Run the notebook

```bash
jupyter notebook data_workflow.ipynb
```

Run all cells from top to bottom. The notebook should execute without errors and reproduce all
tables and visualizations.

## Reflection Questions

**Bias Awareness — where could poor data cleaning introduce bias?**
Filling missing `reviews_per_month` values with 0 assumes those listings simply have no reviews yet; if some were actually data-entry errors, this could understate review activity for those listings. Dropping price outliers (below $10 or above $1,000) removes real luxury listings along with likely data errors, which could bias the analysis toward mid-market listings and understate the true price range in NYC. Because neighbourhood and room type strongly drive price, any cleaning step that disproportionately removes rows from a specific borough or room type (even unintentionally) could skew borough- or room-type-level comparisons.

**How would this workflow need to change for a machine learning project?**
The dataset would need a defined prediction target (e.g., `price`), a train/test split, and encoding of categorical variables (`room_type`, `neighbourhood_group`) into numeric form. Feature scaling and additional feature engineering (e.g., distance to city center) would likely improve model performance beyond what raw columns provide.

**How would this workflow need to change to prepare data for a neural network?**
Neural networks typically require normalized/standardized numeric inputs, one-hot or embedding encodings for categorical features, and a much larger, more complete dataset (missing values would need imputation rather than exclusion, to preserve training data volume).

**Where could this workflow benefit from agentic automation?**
An agent could automate re-running this cleaning/EDA pipeline whenever a new data export is released, flag when missing-value or outlier percentages shift significantly from this baseline, and automatically regenerate the visualizations and summary statistics without manual intervention.
