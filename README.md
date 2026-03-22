# Customer Churn Prediction

I built this project as part of my Fundamentals of AI and ML course. The idea came from a pretty straightforward observation — telecom companies spend a lot of money acquiring customers, but losing them is just as common and far more costly. I wanted to see if machine learning could actually help predict which customers are about to leave, before they do.



## Why This Problem

I've seen people around me switch telecom providers constantly — usually because of pricing or poor support. It got me thinking: the company probably had no idea that customer was about to leave. If they did, maybe they'd have done something about it. That's essentially what this project tries to solve — giving a business that early warning system.



## The Dataset

I used the IBM Telco Customer Churn dataset, which is publicly available on Kaggle. It has information on 7,043 customers — things like how long they've been with the company, what services they use, how much they pay monthly, and whether they eventually left.

The target variable is `Churn` — a simple Yes or No. Everything else in the dataset is used to predict it.

- **Rows:** 7,043 customers  
- **Columns:** 21 features  
- **Churn rate:** ~26.5% (roughly 1 in 4 customers left)



## Project Structure


customer-churn-prediction/
│
├── data/
│   └── telco_churn.csv
│
├── notebooks/
│   ├── 01_eda.ipynb
│   ├── 02_preprocessing.ipynb
│   └── 03_modelling.ipynb
│
├── models/
│   └── random_forest_model.pkl
│
├── results/
│   ├── churn_distribution.png
│   ├── churn_by_contract.png
│   ├── monthly_charges_churn.png
│   ├── confusion_matrix.png
│   ├── roc_curve.png
│   └── feature_importance.png
│
├── requirements.txt
└── README.md



## How to Set It Up

Make sure you have Python 3 installed. Then install the required libraries:

```bash
pip3 install -r requirements.txt
```

That's it. No complex setup, no environment variables, nothing fancy.



## How to Run It

The project runs across three Jupyter notebooks, and they need to be run in order. Each one builds on the previous.

**Step 1 — Open Jupyter:**
```bash
cd customer-churn-prediction
jupyter notebook
```

**Step 2 — Run the notebooks in this sequence:**

`01_eda.ipynb` — Start here. This notebook loads the dataset and explores it visually. You'll see how churn is distributed, which contract types have the highest dropout rates, and how monthly charges differ between customers who stayed and those who left. Three plots get saved to the results folder automatically.

`02_preprocessing.ipynb` — This one cleans the data and gets it ready for modelling. The TotalCharges column had some formatting issues (stored as strings instead of numbers), so that gets fixed here. All text columns get converted to numbers, and the data gets split into training and test sets. The processed data is saved as a pickle file so the next notebook can load it directly.

`03_modelling.ipynb` — The main event. This loads the processed data, trains two models (Logistic Regression and Random Forest), evaluates them, and generates the plots. The best model gets saved at the end.



## What I Found

Before even touching a model, the EDA told a clear story:

Customers on month-to-month contracts churn at around 42%. Customers on two-year contracts? About 3%. That gap is enormous, and it immediately suggested contract type would be one of the strongest signals in the model.

Monthly charges also stood out — churned customers were paying noticeably more on average than those who stayed. And tenure was the reverse — the longer someone had been with the company, the less likely they were to leave.



## Model Results

I trained two models and compared them on the test set (20% of the data, roughly 1,409 customers):

| Model | Accuracy | AUC-ROC | F1 Score |
|---|---|---|---|
| Random Forest | 81.2% | 0.82 | 0.61 |
| Logistic Regression | 79.6% | 0.79 | 0.57 |

Random Forest came out ahead on every metric, so that's the final model. The AUC of 0.82 means the model does a solid job of separating churners from non-churners — well above random guessing (0.5).

The top features by importance were monthly charges, tenure, and total charges — which lines up exactly with what the EDA already suggested.



## Challenges I Ran Into

The `TotalCharges` column looked like numbers but was actually stored as text in the CSV, including some empty strings. That caused errors until I figured out what was happening and used `pd.to_numeric` with `errors='coerce'` to handle it cleanly.

The dataset is also imbalanced — about 73% of customers didn't churn, and only 27% did. This means a model that just predicts "no churn" for everyone would technically get 73% accuracy without learning anything useful. The F1 score and AUC matter more here than raw accuracy, and that's what I focused on when comparing models.



## Things I'd Do Differently With More Time

A few things I'd explore if I came back to this:

- Apply SMOTE to handle the class imbalance more aggressively
- Try XGBoost or LightGBM, which tend to perform well on tabular data like this
- Build a simple web interface where you can enter customer details and get a churn prediction instantly
- Look at misclassified customers specifically — understanding where the model fails is often more useful than the accuracy number


## Libraries Used

- `pandas` — data loading and manipulation  
- `numpy` — numerical operations  
- `matplotlib` and `seaborn` — visualizations  
- `scikit-learn` — model training and evaluation  
- `jupyter` — notebook environment  



## Author

TANAY BHATT
Course: Fundamentals of AI and ML  
Dataset: [IBM Telco Customer Churn — Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
