# Cloud-Based Health Monitoring System

Real-time healthcare prediction system using Google Cloud Platform for monitoring patient vitals and predicting health risks.
## [Dashboards](https://raghuveer9303.github.io/mediguard-dashboard/#/)
### Insights
Real-time patient vital signs monitoring
Health risk probability scores
Trend analysis across patient populations
Alert triggers for critical thresholds

## Overview
This system generates synthetic patient data, processes sensor readings, and uses machine learning models to predict various health risks including:
- Hypoglycemia
- Fall risk
- Cardiac anomalies
- Severe hypotension
- Autonomic dysregulation

## Tools
Python - Data generation, ML models, Flask APIs, data transformation
Google Cloud Platform - Cloud Run, Cloud Functions (Gen 2), Pub/Sub, BigQuery, Cloud Storage, Cloud Scheduler
SQL - BigQuery queries, data aggregation, relationship modeling
Flask - RESTful API for prediction service
Machine Learning - Health risk prediction models (scikit-learn, TensorFlow)
Visualization Tools - Dashboard creation for stakeholder insights

## Goal
Identify patient health risks in real-time by monitoring vital signs and predicting adverse events to support proactive clinical interventions.
Health Risks Predicted: Hypoglycemia, Fall risk, Cardiac anomalies, Severe hypotension, Autonomic dysregulation

## Process Overview
Extract: Generated synthetic patient sensor data (heart rate, blood pressure, temperature, glucose) via Cloud Run service triggered by Cloud Scheduler
Transform: Aggregated streaming sensor readings into 5-minute windows using Cloud Functions, cleaned and normalized data for ML input
Load: Published aggregated data to Pub/Sub topics, ingested predictions into BigQuery tables for analysis
Predict: Deployed ML models via Cloud Run Flask API to generate real-time health risk scores
Visualize: Created BigQuery-powered dashboards displaying patient vitals and risk predictions
Decide: Delivered actionable health insights to clinical stakeholders through interactive dashboards

## Data Architecture / Pipeline
- **Cloud Scheduler**: Triggers data generation every minute
- **Data Generator**: Cloud Run service that generates synthetic patient sensor data
- **Sensor Aggregator**: Cloud Function that aggregates 5-minute windows of sensor data
- **Health Predictor**: Cloud Run service that runs ML predictions on aggregated data
- **Predictions Writer**: Cloud Function that writes predictions to BigQuery
- **Vitals Writer**: Cloud Function that writes vitals and predictions to BigQuery for
  
## Components

### Files

- `data-generator.py` - Generates synthetic patient data and publishes to Pub/Sub
- `sensor-aggregator.py` - Aggregates sensor data into 5-minute windows
- `health-predictor.py` - ML predictor module for loading models and making predictions
- `cloud_run_for_health_predictor.py` - Flask app for prediction service
- `predictions-writer.py` - Writes prediction results to BigQuery
- `vitals-predictions-writer.py` - Writes vitals and predictions to BigQuery
- `requirements.txt` - Python dependencies

### Google Cloud Services Used

- Cloud Run
- Cloud Functions (Gen 2)
- Pub/Sub
- BigQuery
- Cloud Storage
- Cloud Scheduler

### Key Tables
sensor_data → Raw patient vitals (patient_id, timestamp, vitals)
aggregated_vitals → 5-minute aggregated windows
predictions → Health risk scores (patient_id, risk_type, probability)

### Relationships
sensor_data → aggregated_vitals (via patient_id, time_window)
aggregated_vitals → predictions (via patient_id, timestamp)
predictions → dashboard_vitals (via patient_id)

### Key Queries
Aggregating 5-minute sensor windows
Joining predictions with patient vitals
Calculating risk score trends
Identifying high-risk patients

### The Impact
#### Key Findings:
Successfully processed 1,440+ data points per patient daily (1 RPM)
Achieved sub-second prediction latency through Cloud Run autoscaling
Identified high-risk patients requiring immediate clinical attention
Enabled proactive intervention by predicting adverse events priorly

#### Technical Achievements:
Built fully automated, serverless pipeline requiring zero manual effort
Implemented scalable architecture handling multiple patients
Integrated 5 GCP services into cohesive data workflow

## Usage
Once deployed, the system runs automatically:
1. Cloud Scheduler triggers data generation every minute
2. Sensor data flows through Pub/Sub topics
3. Data is aggregated and predictions are made
4. Results are stored in BigQuery for analysis


