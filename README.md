# PBR Matchup Prediction

Machine learning system for predicting **rider–bull matchup outcomes in Professional Bull Riding (PBR)**.

This project was developed as part of a **Wake Forest MSBA Practicum project** and focuses on modeling the interaction between riders and bulls using historical competition data.

The system combines **survival probability modeling and neural network score prediction** to estimate the **expected value of each matchup**, enabling data-driven evaluation of rider–bull pairings.

---

# Project Overview

Professional Bull Riding outcomes depend heavily on the **interaction between a specific rider and a specific bull**.  
Traditional performance metrics often evaluate riders and bulls separately, but matchup dynamics introduce complex interaction effects.

This project implements a **two-engine machine learning framework** that models:

- the probability that a rider stays on the bull for the full **8 seconds**
- the **expected score** if the ride qualifies

These predictions are combined to produce a **risk-adjusted expected value (EV)** for each matchup.

Expected Value Formula:

EV = P(Qualify) × Predicted Score

This allows matchups to be ranked not just by potential score but by **expected performance considering risk**.

---

# Dataset

The modeling framework uses a historical PBR dataset containing **200+ engineered and raw features** related to riders, bulls, and matchup characteristics.

Example feature categories include:

Rider features  
- historical ride performance  
- consistency metrics  
- volatility indicators  

Bull features  
- buckoff percentage  
- scoring volatility  
- average ride score allowed  

Matchup features  
- rider–bull interaction characteristics  
- spin direction and riding hand physics  

Temporal features  
- seasonality encoding  
- event timing patterns  

---

# Data Availability Notice

This project was developed as part of an **industry practicum** and is subject to **non-disclosure agreements (NDA)**.

As a result:

- The original dataset cannot be shared publicly
- The modeling code and analytical framework are included for demonstration purposes
- Certain production tools (such as the internal interface currently under development) are not included in this repository

This repository therefore focuses on the **modeling methodology and system architecture** used in the project.

---

# Model Architecture

```text
                  Rider-Bull Matchup
                           |
        -----------------------------------------
        |                                       |
        v                                       v
  Survival Model                         Score Model
 (Random Forest)                      (Neural Network)
        |                                       |
        v                                       v
 P(Qualify in 8s)                        Predicted Score
        \                                       /
         \                                     /
          ---------------+---------------------
                         |
                         v
                  Expected Value
            EV = P(Qualify) × Score
```

This architecture separates **ride survival probability** from **score estimation**, improving interpretability and predictive performance.

---

# Modeling Components

## 1. Survival Model

The first model predicts the probability that a rider stays on the bull for the required **8 seconds**.

Model type:

Random Forest / Gradient Boosting classifier.

Purpose:

Estimate the likelihood of ride qualification.

Output:

P(Qualify)

---

## 2. Score Prediction Model

The second model predicts the expected **ride score conditional on qualification**.

This model uses a neural network with embedding layers.

Key characteristics:

- embedding layers for rider and bull identities
- prediction of score residuals relative to bull baseline
- batch normalization and dropout for regularization

Output:

Predicted score if the ride qualifies.

---

## 3. Expected Value Framework

The outputs from the two models are combined to produce a **risk-adjusted expected score**.

Expected Value = P(Qualify) × Predicted Score

This allows matchup evaluation based on both:

- scoring potential
- probability of successful rides

The EV framework also allows identification of **high-risk matchups** where predicted scores are high but survival probability is low.

---

# Feature Engineering

Extensive feature engineering was used to capture matchup dynamics.

## Physics-Based Features

Handedness and spin interactions between riders and bulls are used to estimate matchup difficulty.

These features capture the biomechanical alignment between rider stance and bull spin direction.

---

## Temporal Features

Seasonality effects are encoded using sine and cosine transformations.

These features capture patterns related to event timing and seasonal performance variation.

---

## Interaction Features

Custom interaction variables capture relationships between rider ability and bull behavior.

Examples include:

- volatility clash metrics
- rider potential indicators
- heavy hitter bonus variables
- bull difficulty statistics
- historical buckoff percentages

---

# Prediction System

The modeling framework includes a simulation wrapper that allows matchup evaluation.

Capabilities include:

- predicting ride survival probability
- estimating conditional ride scores
- calculating matchup expected value
- evaluating hypothetical rider–bull pairings

The system can also identify **“trap matchups”**, where a high predicted score is paired with a low probability of ride success.

---

# Applications

This modeling framework supports several sports analytics use cases.

- rider–bull matchup evaluation  
- performance prediction  
- event strategy analysis  
- risk-adjusted matchup ranking  
- team selection decision support  

---

# Technologies Used

Python  
Scikit-learn  
Random Forest  
Neural Networks  
Embedding Models  
Feature Engineering  
Sports Analytics  

---

# Project Context

This work was developed as part of a **Wake Forest University MSBA Practicum project** in collaboration with an external partner.

The project focuses on building analytical tools that help teams better understand performance dynamics in professional bull riding.

---

# Author

Yiran Liu  
MS in Business Analytics  
Wake Forest University
