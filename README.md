                                📘 XGBoost-Powered Fraud Detection Engine

📌 Overview

XGBoost-Powered Fraud Detection Engine is a production-inspired backend system designed to proactively detect fraudulent financial transactions.
The project processes raw transaction events, dynamically engineers model-ready features, and applies an XGBoost classifier trained on millions of transactions. An AI decision agent translates model scores into actionable outcomes—allow, step-up authentication, or block—along with human-readable explanations.

The system intentionally focuses on the fraud detection and decisioning layer, mirroring how real-world financial fraud systems are designed.

🧠 Key Features

Handles extreme class imbalance

Uses XGBoost for fraud prediction

Permutation Feature Importance for explainability

AI Decision Agent for risk-based actions

Dynamic runtime feature engineering

Guaranteed training–inference consistency

Monitoring-ready design

Backend-first (no UI dependency)

📂 Dataset

The dataset used in this project is publicly available and exceeds GitHub’s file size limits, so it is not included in this repository.

📌 Users should download the dataset separately and place it in the /data directory before running the notebook or scripts.

📖 Data Dictionary
Feature	Description:

step-	Unit of time in the real world. Each step represents 1 hour. Total of 744 steps (30 days simulation).

type-	Type of transaction: CASH-IN, CASH-OUT, DEBIT, PAYMENT, TRANSFER.

amount-	Transaction amount in local currency.

nameOrig-	Customer who initiated the transaction.

oldbalanceOrg-	Initial balance of the origin account before the transaction.

newbalanceOrig-	Balance of the origin account after the transaction.

nameDest-	Recipient of the transaction.

oldbalanceDest-	Initial balance of the destination account. (Not available for merchants starting with “M”)

newbalanceDest-	Balance of the destination account after the transaction. (Not available for merchants starting with “M”)

isFraud-	Indicates fraudulent transactions simulated by agents attempting account takeover and fund draining.

isFlaggedFraud-	Rule-based flag for illegal transfers exceeding 200,000 in a single transaction.

🔄 System Architecture

                                            Incoming Transaction Event
                                                        ↓
                                          Feature Engineering (Runtime)
                                                        ↓
                                        Feature Alignment (Saved Schema)
                                                        ↓
                                              XGBoost Fraud Model
                                                        ↓
                                              Fraud Probability Score
                                                        ↓
                                                AI Decision Agent
                                                        ↓
                                      Allow / Step-up Authentication / Block
                                                        ↓
                                              Logging & Monitoring


🤖 AI Decision Agent

The AI agent converts raw fraud probabilities into actionable decisions with explanations.

Decision Logic
Fraud Score	Risk Level	Action
> 0.85	High	Block

> 0.60 – 0.85	Medium	Step-up Authentication

> 0.60	Low	Allow

Example Output
{
  "risk_level": "High",
  "decision": "Block",
  "reason": "High-value transaction with complete balance depletion at the origin account; classified as high risk."
}

📊 Explainability

Permutation Feature Importance is used to identify global drivers of fraud predictions.

Ensures the model relies on meaningful financial behavior rather than identifiers.

Lightweight and scalable for large datasets.

📈 Monitoring Strategy

The system is designed for post-deployment monitoring:

Precision, recall, and PR-AUC trends

Fraud loss rate

False positive rate

Transaction amount and balance drift

Logged predictions for auditing and retraining

🚀 Tech Stack

Python

Pandas, NumPy

Scikit-learn

XGBoost

FastAPI (optional backend API)

JSON-based feature schema persistence

🎯 Design Philosophy

Backend-first architecture

No UI dependency

Modular and extensible

Training–inference consistency guaranteed

Business-aligned fraud decisioning

📌 Future Extensions

Analyst dashboard

Real-time streaming ingestion

Automated retraining

Cost-sensitive decision thresholds
