# streamlit-ml-nlp-review-app

An end-to-end Machine Learning and Natural Language Processing (NLP) intelligence platform built with **Scikit-Learn**, **HuggingFace Transformers**, and **Streamlit**. This dashboard ingests raw customer reviews, performs advanced sentiment analysis, extracts text-based feature metrics, and predicts customer recommendation intent.

---

## 🎯 Project Overview & Business Value
In e-commerce, customer retention hinges on understanding feedback at scale. This project provides businesses with a dual-purpose tool:
1. **Interactive Analytics Dashboard:** Aggregates and visualizes customer sentiments, rating distributions, and text metrics to pinpoint customer friction points.
2. **AI-Powered Review Simulator:** A real-time diagnostic playground where developers or business analysts can input raw review text and instantly run it through a multi-stage NLP and Machine Learning classification pipeline to predict customer churn/recommendation status.

---

## 🛠️ Tech Stack & Key Libraries
* **Frontend UI:** Streamlit (clean, interactive, and responsive)
* **Natural Language Processing (NLP):** HuggingFace `transformers` (`distilbert-base-uncased-finetuned-sst-2-english`)
* **Machine Learning:** Scikit-Learn (`RandomForestClassifier` for predictive modeling)
* **Data Engineering & Visualization:** Pandas, NumPy, Plotly
* **Model Serialization:** Joblib

---
## 📦 Dataset Overview & Schema

This project utilizes the **Women's E-Commerce Clothing Reviews** dataset sourced from Kaggle. It contains **23,486 authentic customer reviews** and ratings across high-level e-commerce product categories. 

The dataset provides a hybrid blend of unstructured raw text alongside structured numerical and categorical features, making it ideal for combined NLP and predictive classification modeling.

### Key Attributes & Schema

| Column Name | Data Type | Description | Role in Pipeline |
| :--- | :--- | :--- | :--- |
| **`Review Text`** | Text | The raw body of the customer's written review | Input for DistilBERT NLP & Text Feature Extraction |
| **`Rating`** | Integer | Product star rating given by the customer (1 to 5) | Feature for Random Forest Classifier |
| **`Recommended IND`** | Binary | Recommendation status (1 = Recommended, 0 = Not Recommended) | **Primary Target Variable ($y$)** |
| **`Age`** | Integer | Positive integer indicating the reviewer's age | Demographic Feature (Optional) |
| **`Title`** | Text | Short headline/subject of the review | Auxiliary Text |
| **`Positive Feedback Count`** | Integer | Number of other customers who found the review helpful | Engagement Metric |
| **`Division Name`** | Categorical | High-level product division (e.g., *Initials, Petite, General*) | Product Metadata |
| **`Department Name`** | Categorical | Product department (e.g., *Dresses, Tops, Bottoms*) | Product Metadata |
| **`Class Name`** | Categorical | Specific product class (e.g., *Pants, Blouses, Fine Knit*) | Product Metadata |

---

### Data Characteristics & Preprocessing Highlights
* **Unstructured Text:** `Review Text` contains varying lengths of natural language customer feedback, capturing nuances of customer sentiment, size/fit complaints, and product quality.
* **Target Imbalance:** Approximately 82% of reviews are positive recommendations (`Recommended IND = 1`), requiring stratified sampling (`stratify=y`) during the train-test split to ensure reliable model evaluation.
* **Engineered Features:** Preprocessing derives additional tabular signals from raw text, including `Review_Length`, `Word_Count`, `Has_Exclamation`, and a fine-tuned Transformer sentiment binary score (`Transformer_Sentiment`).

---

### Data Source & Citation
* **Source:** [Kaggle: Women's E-Commerce Clothing Reviews](https://www.kaggle.com/datasets/nicapotato/womens-ecommerce-clothing-reviews)
* **Access Note:** Data is anonymized and licensed for public educational and non-commercial research use.
---

## 📁 Repository Structure
Code output
SUCCESS

```text
streamlit-ml-nlp-review-app/
│
├── data/                          # Organized dataset storage
│   ├── raw/                       # Original, untouched Kaggle CSV
│   └── processed/                 # Engineered datasets (git-ignored)
│
├── models/                        # Serialized model artifacts
│   └── review_model.pkl           # Trained Random Forest Model (git-ignored)
│
├── notebooks/                     # Exploratory Phase
│   └── exploratory_analysis.ipynb # Data cleaning & visual prototyping
│
├── src/                           # Production Source Code
│   ├── __init__.py                
│   ├── data_preprocessing.py      # Feature engineering and data cleaning
│   ├── sentiment_engine.py        # HuggingFace Sentiment Pipeline
│   └── train_model.py             # Model training and metric evaluations
│
├── app.py                         # Streamlit Application Entrypoint
├── requirements.txt               # Dependencies
└── .gitignore                     # Tidy repository exclusions
