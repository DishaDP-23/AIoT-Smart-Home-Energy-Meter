# AIoT-Based Intelligent Home Energy Consumption Prediction and Adaptive Appliance Scheduling

## Overview

An AIoT-based Smart Home Energy Management System that combines machine learning-based household energy forecasting, intelligent appliance scheduling, and real-time IoT telemetry visualization to explore energy-efficient residential energy management.

The system uses historical household energy consumption data to predict aggregate power consumption for the next 15-minute interval. Based on the predicted demand, appliance scheduling strategies are simulated to optimize energy usage, reduce peak demand, and minimize electricity costs under configurable operational constraints.

The project integrates **XGBoost, simulated appliance scheduling, Streamlit visualization, and ThingsBoard Cloud telemetry** into a unified software-based energy management framework.

---

## Objectives

- Predict household aggregate energy consumption using machine learning.
- Develop intelligent appliance scheduling strategies.
- Reduce simulated electricity costs and peak demand.
- Evaluate scheduling decisions under power-cap and appliance timing constraints.
- Visualize energy consumption, predictions, scheduling decisions, and system telemetry.
- Explore the integration of machine learning and IoT technologies for smart home energy management.

---

## System Architecture

The system consists of the following major components:

1. **Historical Energy Data** – Household electricity consumption data from the REFIT dataset.
2. **Data Preprocessing** – Data cleaning, feature preparation, and chronological train-validation-test splitting.
3. **Energy Forecasting** – XGBoost regression model predicting aggregate household power consumption for the next 15-minute interval.
4. **Appliance Scheduling** – Simulation of unscheduled, rule-based, and adaptive scheduling strategies.
5. **Energy Management** – Evaluation of energy costs, peak demand, scheduling delays, and power-cap violations.
6. **Dashboard** – Interactive visualization of forecasts, appliance schedules, and energy management results using Streamlit.
7. **IoT Integration** – Telemetry visualization and integration through ThingsBoard Cloud.

---

## Machine Learning Model

### XGBoost Regression

An XGBoost regression model is used to predict aggregate household power consumption for the next 15-minute interval.

The model is trained using historical household energy consumption data, with chronological data splitting to preserve the temporal order of observations.

### Dataset

**REFIT Electrical Load Measurements Dataset**

The REFIT dataset contains real-world electricity consumption measurements collected from residential households.

- Dataset: REFIT Electrical Load Measurements
- Source: [REFIT Dataset – Zenodo](https://zenodo.org/records/5063428)
- Application: Household energy consumption forecasting and appliance scheduling simulation

### Data Splitting

| Dataset | Percentage |
|---|---:|
| Training | 70% |
| Validation | 15% |
| Testing | 15% |

The chronological split avoids randomly mixing future observations into the training data.

### Model Configuration

| Parameter | Value |
|---|---:|
| Algorithm | XGBoost Regressor |
| Number of Estimators | 500 |
| Learning Rate | 0.05 |
| Maximum Depth | 6 |
| Minimum Child Weight | 3 |
| Subsample | 0.8 |
| Column Subsample | 0.8 |
| Random State | 42 |
| Objective | Regression |
| Evaluation Metric | RMSE |
| Early Stopping | 40 rounds |

### Model Performance

Evaluated on the test dataset:

| Metric | Value |
|---|---:|
| Mean Absolute Error (MAE) | 169.41 W |
| Root Mean Squared Error (RMSE) | 365.66 W |
| R² Score | 0.2703 |
| Mean Absolute Percentage Error (MAPE) | 40.55% |
| Test Samples | 7,476 |
| Input Features | 21 |
| Best Iteration | 109 |

The model demonstrates the ability to learn patterns from historical household energy consumption. However, prediction errors remain significant, highlighting the challenges of forecasting dynamic residential loads.

---

## Appliance Scheduling Strategies

The system evaluates three scheduling strategies using simulated appliance jobs and historical household consumption.

### 1. Unscheduled Strategy

Appliances operate according to their original simulated start times without scheduling-based load optimization.

This serves as the baseline for comparing the energy management strategies.

### 2. Rule-Based Scheduling

Appliance jobs are scheduled using predefined scheduling rules and operational constraints, considering factors such as:

- Appliance availability windows
- Job duration
- Power requirements
- Scheduling delays
- Configured electricity tariffs
- Household demand

### 3. Adaptive Scheduling

The adaptive scheduling strategy uses predicted household power consumption and existing scheduled loads to make scheduling decisions dynamically.

The scheduler considers:

- Predicted household demand
- Previously committed appliance loads
- Power-cap constraints
- Appliance operating windows
- Job duration
- Maximum allowable delay

The objective is to improve load distribution and reduce peak demand while maintaining appliance scheduling constraints.

---

## Evaluation Metrics

The scheduling strategies are evaluated using:

- Total simulated electricity cost
- Mean daily peak power demand
- Power-cap violation slots
- Unserved appliance jobs
- Unserved energy
- Mean appliance scheduling delay
- Job constraint violations

---

## Results

The scheduling strategies were evaluated across **68 comparable days**, with **204 appliance jobs per strategy**.

### Overall Comparison

| Metric | Unscheduled | Rule-Based | Adaptive |
|---|---:|---:|---:|
| Total Cost (simulation units) | 7039.61 | 5162.81 | 5162.81 |
| Mean Daily Peak (kW) | 4.0635 | 4.4677 | 3.8869 |
| Power-Cap Violation Slots | 14 | 8 | 7 |
| Mean Delay (min) | 0 | 160 | 180 |
| Unserved Jobs | 0 | 0 | 0 |
| Job Constraint Violations | 0 | 0 | 0 |

### Key Findings

- Both scheduling strategies reduced simulated electricity costs by approximately **26.66%** compared with the unscheduled baseline.
- Adaptive scheduling achieved approximately **4.35% lower mean daily peak demand** compared with the unscheduled strategy.
- Adaptive scheduling recorded the lowest mean daily peak power among the evaluated strategies.
- The adaptive strategy reduced power-cap violation slots from 14 to 7 compared with the unscheduled baseline.
- Both scheduling strategies successfully served all simulated appliance jobs without job-level constraint violations.
- Adaptive scheduling involved a higher average scheduling delay compared with rule-based scheduling, illustrating the trade-off between demand optimization and appliance waiting time.

The results indicate that scheduling decisions can influence residential load distribution and simulated energy costs. However, aggregate power-cap violations were not completely eliminated.

> **Note:** Cost values represent configured simulation units and should not be interpreted as actual household electricity bills or INR savings.

---

## Dashboard

The project includes an interactive dashboard developed using Streamlit for visualizing and exploring the energy management system.

Dashboard functionality includes:

- Household energy consumption visualization
- Actual versus predicted power consumption
- Energy forecasting results
- Appliance scheduling decisions
- Scheduling strategy comparisons
- Peak demand analysis
- Energy cost comparisons
- IoT telemetry visualization

---

## IoT Integration

The project integrates with **ThingsBoard Cloud** for telemetry visualization and IoT data integration.

The integration demonstrates how energy consumption measurements, predictions, and energy management information can be represented through an IoT platform.

The current implementation is software-based and does not directly control physical appliances.

---

## Technologies Used

| Category | Technologies |
|---|---|
| Programming Language | Python |
| Machine Learning | XGBoost, Scikit-learn |
| Data Processing | Pandas, NumPy |
| Visualization | Matplotlib, Plotly |
| Dashboard | Streamlit |
| IoT Platform | ThingsBoard Cloud |
| Dataset | REFIT Electrical Load Measurements |
| Development | Jupyter Notebook, Python IDE |

---

## Project Limitations

- Energy forecasting accuracy remains limited, with significant prediction errors for dynamic household consumption.
- Appliance scheduling is evaluated through simulation rather than physical appliance control.
- Scheduling cost reductions depend on the configured tariff model.
- Power-cap violations remain in some simulation intervals.
- Scheduling results are based on selected historical household data and simulated appliance jobs.
- The current implementation has not been validated through a real-world smart meter and controllable appliance deployment.

---

## Future Work

- Improve energy forecasting accuracy through feature engineering and alternative forecasting models.
- Incorporate prediction uncertainty into scheduling decisions.
- Evaluate the system using additional households and consumption profiles.
- Explore dynamic electricity tariffs and real-time demand response.
- Integrate physical IoT sensors and smart plugs.
- Implement real-time appliance control and validate scheduling decisions in a physical smart home environment.
- Investigate reinforcement learning-based scheduling approaches.

---

## Team Project

Developed as an academic project exploring the integration of Artificial Intelligence, IoT, machine learning, and intelligent energy management for smart homes.

---

## References

- REFIT Electrical Load Measurements Dataset: [https://zenodo.org/records/5063428](https://zenodo.org/records/5063428)
- XGBoost Documentation: [https://xgboost.readthedocs.io/](https://xgboost.readthedocs.io/)
- Streamlit Documentation: [https://docs.streamlit.io/](https://docs.streamlit.io/)
- ThingsBoard Documentation: [https://thingsboard.io/docs/](https://thingsboard.io/docs/)
