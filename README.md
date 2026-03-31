# Forecast customer churn I made this project Seam part of mine Fundamentals of AI and ML Course The idea Came from a beautiful straightforward observation— Telecom companies invest a lot. Money acquiring customers, But losing them is just as common and far more expensive. I would observe about machine learning It can actually contribute to predict it customers Before they go, they must go.



## Why This Problem I've Then people around me change telecom providers Still— usually because of prices or poor support. This got me thinking: the company Probably had no idea that the customer was going to vacate. If they did, they probably would have done something That's basically what it's all about this project tries To solve— to give a business that early warning system.



## The Dataset I used the IBM Telco Customer Churn dataset, which is publicly available. Kaggle. It contains information. 7, 043 customers— Things like how long they've been together. The company, What services they use, how much they contribute per month, and whether they eventually quit.

The target variable is` Churn`— A simple yes or no. Everything And me the dataset It is used to predict.

-** Rows:** 7, 043 customers-** Column:** 21 features-** Release frequency:**~ 26.5%( About 1 inch 4 customers Again)## Project structure Customer churn forecast/│├── data/│└── telco_churn. Csv│├── notebook/│├── 01_eda. Ipynb│├── 02_preprocessing. Ipynb│└── 03_modelling. Ipynb│├── models/│└── random_forest_model. Pkl│├── results/│├── churn_distribution. Png│├── churn_by_contract. Png│├── monthly_charges_churn. Png│├── confusion_matrix. Png│├── roc_curve. Png│└── feature_importance. Png│├── requirements. Txt└── README. Md## How to tune It Up Produce guaranteed you have it. Python 3 Install and then install. The required libraries:``` bash Pip3 install- r requirements. Txt`` That's it. No complex setup, No environment variables, Don't like anything.



## How to run it The project Goes over three Jupyter notebooks, And they must be run in order. Every single one but do the previous.

** steps 1— Open Jupyter:**``` bash Cd customer- churn- prediction Jupyter notebook``** steps 2— run the notebooks I this sequence:**` 01_eda. Ipynb`— Start here. This notebook burden the dataset and explores it visually. You'll Witness how Manthan is distributed, what types of contracts there are. The highest dropout rates, And how? monthly charges There is a difference customers Those who stayed and those who left. Three plots Be safe the results folder Automatic` 02_preprocessing. Ipynb`— This one cleaning up the data And found it ready For modeling The TotalCharges column our some formatting issues( stored as strings instead of numbers), so that fixed here. All text columns are converted to numbers, and the data is divided into training and test sets. The processed data is saved as a pickle file So the next notebook Can load directly.

` 03_modelling. Ipynb`— The main event. This burden the processed data, trains two models( Logistic Regression and Random Forest), Evaluates them and generates them. The plots. Save on the best model. The end.



## What I got Before you touch a model, go EDA told a clear story: Customers Hover around on month- to- month contracts 42%. Users on two- year contracts? approx 3%. The difference is huge and it immediately suggests what type of contract it will be. One Of the strongest signals I the model.

Monthly charges Also stands outside— the circle customers De som ble igjen betalte I gjennomsnitt mer. And there was a deadline. The reverse— Some had been together for a long time. The company, They were less likely to vacate.



## Model results I trained. Two models And compared them. The test set( 20% Of the data, Approx 1, 409 customers):| Model| Accuracy| AUC- ROC| F1 Score||---|---|---|---|| Random Forest| 81.2%| 0.82| 0.61|| Logistic Regression| 79.6%| 0.79| 0.57| Random Forest Get ahead of every calculation, so it is. The final model. Go AUC Of 0.82 Importance the model do a solid job Distinguishing churners non- churners— okay above random guessing( 0.5).

The top There were functions in order of importance. Monthly charges, duration, and total Charges- Which line is with whom? the EDA Already recommended## Challenges I faced The` TotalCharges` column Looked like numbers but was actually stored as text in the CSV, including some empty strings. This caused errors until I figured out what was going on and used` pd. To_numeric` with it. ` errors=' coerce'` To handle nicely.

The dataset If- is also unbalanced 73% Of customers Not cored, and only 27% Means it a model Which just predicts that technically there will be" no churn" for everyone. 73% accuracy Without learning anything useful. F1 score and AUC The case more here from raw accuracy, And that's what I noticed when comparing models.



## Things I would do differently. More Time A few things If I return to it, I will discover:- Seek SMOTE to handle the class imbalance More aggressive- Strive it. XGBoost or LightGBM, Those who perform well. Tabular data In this strategy- Develop. A simple web interface Where you can enter and retrieve customer details. A churn prediction Immediately- Witness misclassified customers In particular- to understand where the model Mistakes are often more useful the accuracy number## Libraries used-` panda'— data loading and manipulation-' numpy'- numerical operations-` matplotlib` and` seaborn`— concepts-" Learn to Skate"- model training and evaluation-' jupyter'- notebook environment## The author TANAY BHATT Course: Fundamentals of AI and ML Data set:[ IBM Telco Customer Churn— Kaggle]( https:// www. Kaggle. Com/ datasets/ blastchar/ telco- customer- churn)
