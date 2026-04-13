# cartwave-late-delivery-prediction

# CartWave Marketplace: Late Delivery Prediction using Machine Learning
## Installation
To use this project, first clone the repo on your device using the commands below:

git init

git clone https://github.com/PraseedaSaripalle/cartwave-late-delivery-prediction.git

## Project Overview

This project was developed as part of a data science course final project to demonstrate the ability to solve a realistic business problem using machine learning and to communicate technical findings in a business-oriented way.

Our hypothetical company, **CartWave Marketplace**, is a mid-sized online marketplace that connects customers with third-party sellers across multiple product categories. The company is facing a business challenge related to **late deliveries**, which negatively affect customer satisfaction, review scores, and repeat purchasing behavior.

To address this challenge, we developed a machine learning pipeline to **predict whether an order will be delivered late** based on historical e-commerce order data.

---

## Business Problem

Late deliveries create multiple operational and customer experience issues for CartWave Marketplace, including:

- lower customer satisfaction
- increased negative reviews
- loss of trust in sellers and the platform
- reduced repeat purchase likelihood
- increased need for customer support intervention

The goal of this project is to build a binary classification model that predicts whether an order is likely to be delivered late so that the business can take proactive actions such as:

- alerting customers in advance
- prioritizing risky shipments
- monitoring sellers with poor fulfillment performance
- improving shipping and logistics planning

---

## Project Objective

The objective of this project is to build a machine learning model that predicts the following target:

- **late_delivery_flag = 1** if an order was delivered later than its estimated delivery date
- **late_delivery_flag = 0** if an order was delivered on time or early

This transforms the business problem into a supervised binary classification problem.

---

## Datasets Used

This project uses the **Olist Brazilian E-Commerce Public Dataset** from Kaggle.

Source:
- [Olist Brazilian E-Commerce Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

### Raw files used in this project

We used the following **4 raw datasets**:

1. **olist_orders_dataset.csv**
   - Main order table
   - Contains order status, purchase timestamp, approval timestamp, estimated delivery date, and actual delivery date

2. **olist_order_items_dataset.csv**
   - Item-level details for each order
   - Contains item price, freight value, seller ID, and item sequence

3. **olist_order_payments_dataset.csv**
   - Payment information for each order
   - Contains payment type, payment installments, and payment value

4. **olist_customers_dataset.csv**
   - Customer identifiers and location information
   - Contains customer city and customer state

### Why these datasets were selected

These files were selected because they provide the core information required to:
- identify whether an order was delivered late
- engineer operational and transactional features
- capture shipping-related signals
- incorporate regional customer information

---

## Project Workflow

The project was completed in two main notebook stages.

### Notebook 1: Data Preprocessing
File:
- `notebooks/01_data_preprocessing_olist.ipynb`

This notebook performs the following steps:

- loads the raw datasets from Amazon S3
- inspects the data structure, columns, and missing values
- converts order timestamp columns into datetime format
- filters the data to delivered orders only
- creates the target variable `late_delivery_flag`
- aggregates item-level data to the order level
- aggregates payment data to the order level
- selects customer location features
- merges all relevant datasets into one modeling table
- creates time-based features
- handles missing values
- encodes categorical variables
- splits the data into training and testing sets
- saves processed datasets for reuse

### Notebook 2: Model Training
File:
- `notebooks/02_model_training_late_delivery.ipynb`

This notebook performs the following steps:

- loads processed training and testing data from Amazon S3
- separates the feature matrix and target variable
- trains a baseline **Logistic Regression** model
- trains a **Random Forest** model
- evaluates both models using:
  - accuracy
  - precision
  - recall
  - F1-score
  - ROC-AUC
- compares model performance
- examines Random Forest feature importance
- saves model results for reporting

---

## Data Storage Approach

Because the notebook runtime environment did not reliably access files uploaded through the workspace interface, the project used **Amazon S3** as the main storage layer for both raw and processed data.

### Raw data storage
The raw Olist CSV files were uploaded to an S3 bucket and loaded into the preprocessing notebook from there.

### Processed data storage
The processed datasets generated during preprocessing were also uploaded to S3 so that they could be reused in the model training notebook without rebuilding the preprocessing pipeline.

This approach improved reproducibility and aligned better with cloud-based machine learning workflows.

---

## Processed Outputs

The preprocessing pipeline generated the following outputs:

- `merged_orders.csv`
- `train.csv`
- `test.csv`

The model training notebook also generated:

- `model_results.csv`

These processed outputs were stored in Amazon S3 for reuse and documentation.

---

## Repository Structure

```text
cartwave-late-delivery-prediction/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── data/
│   ├── raw/
│   │   └── raw_data_source_links.md
│   └── processed/
│       └── processed_data_notes.md
│
├── notebooks/
│   ├── 01_data_preprocessing_olist.ipynb
│   └── 02_model_training_late_delivery.ipynb
│
├── reports/
│   ├── Data_Science_Design_Document.pdf
│   └── Executive_Presentation.pdf
│
└── images/

---

## Presentations and projects
- Amazon SageMaker (AWS) Python - Jupyter Notebook notebooks
- Video Presentation [reports/Final Project Video Presentation_Team 3_Predicting Late Deliveries.mp4]
