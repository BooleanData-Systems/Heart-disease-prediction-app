# Boolean Data - Heart Disease Risk Prediction

## Overview
A Snowflake Native Application that predicts heart disease risk based on clinical
and lifestyle parameters using a Random Forest Classifier. The app includes
preloaded sample data and an interactive Streamlit interface for immediate use.

## Features
- Predict heart disease risk from 12 clinical input features
- View prediction probability scores
- Save prediction results to Snowflake tables
- Preloaded training dataset (32 patient records)

## Configuration Steps

1. Install the application from Snowflake Marketplace.
2. Open the application in Snowsight.
3. The CREATE WAREHOUSE privilege is automatically granted at install time.
4. In the **Permissions** sidebar, click **Connect Warehouse** to bind a warehouse for query execution.
5. The app is ready — enter patient details and run predictions.

## Application Components

### Tables

| Table | Description |
|-------|-------------|
| `app_schema.CLINICAL_DATA` | Preloaded training dataset with 32 patient records used to train the model |
| `app_schema.CLINICAL_PREDICTION_RESULTS` | Stores user-generated prediction results |

### Stored Procedures

| Procedure | Parameters | Description |
|-----------|------------|-------------|
| `config.register_reference` | `(ref_name STRING, operation STRING, ref_or_alias STRING)` | Callback procedure for binding consumer warehouse reference via the Permissions SDK |

### Streamlit App

| Component | Description |
|-----------|-------------|
| `app_schema.heart_disease_app` | Interactive UI for entering patient data, running predictions, and saving results |

## Required Privileges

| Privilege / Reference | Type | Purpose |
|-----------------------|------|---------|
| `CREATE WAREHOUSE` | Account privilege (auto-granted at install) | Allows the app to create a warehouse if needed |
| `consumer_warehouse` (USAGE, OPERATE) | Warehouse reference | Consumer-provided warehouse for executing prediction queries |

## Machine Learning Model

The application trains a Random Forest Classifier (100 estimators) on the CLINICAL_DATA
table at app launch. The model uses an 80/20 train/test split and displays accuracy in the sidebar.

### Input Features
AGE, GENDER, BMI, BLOOD_PRESSURE, GLUCOSE_LEVEL, CHOLESTEROL, SMOKING,
PHYSICAL_ACTIVITY, FAMILY_HISTORY, DIET_SCORE, STRESS_LEVEL, HEART_RATE

### Output
- Predicted Risk: High Risk (1) or Low Risk (0)
- Probability Score (0.0 - 1.0)

## Example SQL Commands

View the training dataset:

    SELECT * FROM <app_name>.app_schema.CLINICAL_DATA LIMIT 10;

View saved prediction results:

    SELECT * FROM <app_name>.app_schema.CLINICAL_PREDICTION_RESULTS;

Count predictions by risk level:

    SELECT PREDICTED_RISK, COUNT(*) AS total
    FROM <app_name>.app_schema.CLINICAL_PREDICTION_RESULTS
    GROUP BY PREDICTED_RISK;
