# Heart Disease Risk Prediction

## Overview
This application uses a Random Forest classifier to predict heart disease risk based on clinical patient data.

## Features
- Train a model on the included clinical dataset
- Input patient details via an interactive form
- Get real-time risk predictions with probability scores
- Save prediction results to a Snowflake table

## Setup
1. Install the application
2. Grant the requested privileges (CREATE TABLE, warehouse USAGE)
3. Open the Streamlit app from the installed application

## Input Parameters
| Parameter         | Range     |
|-------------------|-----------|
| Age               | 20 - 90   |
| Gender            | M / F     |
| BMI               | 15 - 45   |
| Blood Pressure    | 80 - 200  |
| Glucose Level     | 70 - 250  |
| Cholesterol       | 100 - 300 |
| Smoking           | 0 / 1     |
| Physical Activity | 0 / 1     |
| Family History    | 0 / 1     |
| Diet Score        | 2 - 10    |
| Stress Level      | 2 - 10    |
| Heart Rate        | 50 - 120  |

## Output
- **Prediction**: High Risk or Low Risk
- **Probability**: Confidence score (0 to 1)

## Privileges Required
- CREATE TABLE: To save prediction results
- USAGE on a warehouse: To run queries
