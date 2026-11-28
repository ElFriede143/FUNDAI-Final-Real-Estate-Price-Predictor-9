# FUNDAI-Final-Real-Estate-Price-Predictor-9
**Course:** Fundamentals of Artificial Intelligence (FUNDAI), Section 09282-FUNDAI
**Group:** 9
**Assigned Topic:** #9, Real Estate Price Predictor with "Why" Explainer

## Team
| Member | Primary responsibility |
|---|---|
| John Benedict Z. Bengcolita | Data cleaning, exploration, preprocessing pipeline |
| Dave Weckl O. Geonzon | Models, tuning, evaluation, explainer logic |
| Jan Andrie Waper | Gradio app, bias audit, PDF assembly |

## Overview
A tabular regression system that predicts a house's sale price from its features and explains each prediction by showing which features added or subtracted the most value. It uses Linear, Ridge and Lasso regression on the Ames Housing dataset and is deployed as an interactive Gradio demo.

## Dataset
- **Source:** Ames Housing Dataset, compiled by Dean De Cock (2011) from the Ames City Assessor's records; accessed through a Kaggle upload by kozue.
- **Size:** 2,930 home sales (2006 to 2010), 82 columns (79 property features, two ID columns, and the target `SalePrice`).
- **Note:** `NA` and `None` in several columns mean the feature is absent (for example, no alley, pool or fireplace), so they are kept as categories instead of treated as missing data.
- **License:** the Kaggle page lists the license as "Unknown." The data is used only for coursework.
- **Privacy:** public assessor records; no names or personal identifiers.

## Ethics and bias
Home prices carry the history of redlining and neighborhood segregation, and features such as Neighborhood can act as proxies for race or income. We audit prediction error by neighborhood, test the model with and without Neighborhood, and present results as estimates, not appraisals. Full analysis is in the technical documentation.

## Method
1. Clean the data: keep `NA`/`None` as categories, fill Lot Frontage with the neighborhood median, drop Order and PID, remove houses over 4,000 sq ft, 80/20 train/test split
2. Preprocess: log-transform `SalePrice`, one-hot encode categories, scale numbers
3. Train Linear Regression (baseline), Ridge and Lasso with 5-fold cross-validation
4. Evaluate: R², RMSLE, MAE, RMSE, plus a tuning log
5. Bias audit: error by neighborhood, with vs. without Neighborhood
6. Explainer: contribution = coefficient x (input value - training mean)
7. Gradio app: inputs, predicted price, top features that raised or lowered it

## Target metrics
| Metric | Target (test set) |
|---|---|
| R² | at least 0.85 |
| RMSLE | at most 0.16 |
| MAE | at most $20,000 |
| RMSE | reported, no fixed target |
| Fairness check | median percentage error per neighborhood within 5 points of the overall figure |

*(Results will be added as the project progresses.)*

## Repository structure
```
FUNDAI-Final-Real-Estate-Price-Predictor-9/
├── README.md
├── notebook.ipynb        # Master Colab notebook (runs with Restart and run all)
├── data/                 # AmesHousing.csv or download instructions
├── docs/
│   ├── M1_Proposal.pdf
│   └── Technical_Documentation.pdf
└── requirements.txt
```

## How to run
1. Open the notebook in Google Colab: [Colab link]
2. Choose **Runtime > Restart and run all**
3. The Gradio demo launches at the end of the notebook: [demo link]

## Progress
- [x] M1: Proposal and architecture (Nov 28)
- [ ] M2: Working prototype and draft docs (Dec 5)
- [ ] M3: Final artifacts (Dec 7, 8:00 AM)
- [ ] M4: Individual defense (Dec 10 to 15)

## AI-use disclosure
[Write honestly how your group used AI tools, for which tasks, and what you checked or wrote yourselves.]

## References
De Cock, D. (2011). Ames, Iowa: Alternative to the Boston Housing data as an end of semester regression project. *Journal of Statistics Education, 19*(3). http://jse.amstat.org/v19n3/decock.pdf

kozue. (n.d.). *Ames Housing Dataset* [Data set]. Kaggle. https://www.kaggle.com/datasets/shashanknecrothapa/ames-housing-dataset
