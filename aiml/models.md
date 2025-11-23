# 🧠 JoyBridge – Model Design Overview

This document describes the core AI/ML models used in JoyBridge, their purpose, input features, algorithms, and future improvement plans.

---

## 1. Smart Matching Engine

**Goal:**  
Match families, institutions, and events in a way that is safe, relevant, and emotionally impactful.

**Problem Type:**  
Recommendation System (Hybrid: content-based + collaborative)

**Inputs (Features):**
- Geographical distance (family ↔ institution)
- Festival type & cultural preferences
- Family capacity (max number of children)
- Past participation history
- Institution capacity & constraints
- Safety score (from Risk Prediction Model)

**Baseline Approach:**
- Content-based similarity using:
  - Location vectors
  - Festival tags
  - Capacity ranges
- Collaborative filtering using:
  - Matrix factorisation over historical matches
  - Implicit feedback (attendance, ratings)

**Output:**
- Ranked list of recommended institutions/families
- Match score (0–1)

**Future Improvements:**
- Learning-to-rank model (e.g., XGBoost / LightGBM)
- Context-aware recommendations (time, festival importance)
- Reinforcement Learning for continuous optimisation

---

## 2. Risk Prediction Model

**Goal:**  
Identify potentially unsafe or high-risk pairings **before** they are approved.

**Problem Type:**  
Binary / Multi-class Classification (Low / Medium / High risk)

**Inputs (Features):**
- Verification completeness (ID, address, references)
- Number of past events
- Past warnings or incident flags
- No-show or late cancellation history
- Time since last participation
- Institution feedback rating

**Baseline Algorithms:**
- Logistic Regression (simple, interpretable)
- Random Forest / Gradient Boosting (better performance)

**Output:**
- Risk score (0–1)
- Risk class: `LOW`, `MEDIUM`, `HIGH`

**Usage:**
- Integrated into approval workflow:
  - HIGH → manual admin review required
  - MEDIUM → institution confirmation mandatory
  - LOW → auto-suggested

**Future Improvements:**
- Calibrated probability estimates
- Explainable AI (feature importance per decision)
- Continual learning as more data arrives

---

## 3. Sentiment & Emotion Analysis

**Goal:**  
Measure emotional impact of events on children, families, and institutions.

**Problem Type:**  
NLP Sentiment Analysis + Emotion Classification

**Data Sources:**
- Post-event feedback text
- Story captions on memory wall
- Volunteer & staff notes

**Baseline Approach:**
- Pre-trained transformer (e.g., BERT / DistilBERT) fine-tuned on:
  - Positive / Neutral / Negative sentiment
- Optional extension:
  - Multi-label emotions: Joy, Gratitude, Calm, Concern, Sadness

**Output:**
- Sentiment score (−1 to +1 or 0–1)
- Dominant emotion label

**Usage:**
- Aggregate emotional health indicators per:
  - Institution
  - Festival
  - Time period

**Future Improvements:**
- Multilingual sentiment models
- Domain-specific fine-tuning on NGO / social-impact text

---

## 4. Image Moderation & Safety Model

**Goal:**  
Prevent unsafe, inappropriate, or privacy-violating images from being published.

**Problem Type:**  
Image Classification + Rule-based Filtering

**Checks:**
- NSFW / unsafe content
- Violence / abuse indicators
- Face detection for children (to anonymise if needed)
- Detecting text overlays with offensive content (OCR)

**Baseline Approach:**
- CNN-based classifier (or pretrained models)
- OpenCV/YOLO for:
  - Face detection → blurring / masking
  - Object detection of sensitive items

**Output:**
- `ALLOW`, `BLUR_FACE`, or `BLOCK`
- Moderation log entry

**Future Improvements:**
- Fine-tuned CV model on JoyBridge-specific dataset
- Active learning pipeline from moderation feedback

---

## 5. Donation Behaviour & Campaign Prediction

**Goal:**  
Predict donation likelihood and optimise timing / targeting of campaigns.

**Problem Type:**  
Binary Classification / Regression (amount prediction)

**Inputs (Features):**
- Past donation history
- Festival type & theme (Diwali, Eid, Christmas, etc.)
- Engagement level (app usage, event participation)
- Emotional sentiment from interactions
- Time since last donation

**Baseline Algorithms:**
- Logistic Regression (likelihood)
- Random Forest / Gradient Boosting (likelihood + segmenting donors)

**Output:**
- Probability of donation for each user
- Recommended campaign targeting list

**Usage:**
- Prioritise outreach to high-likelihood donors
- Design “Adopt-a-Festival” campaigns

---

## 6. Impact Analytics & Scoring Model

**Goal:**  
Quantify and visualise social impact for NGOs, CSR partners, and reports.

**Problem Type:**  
Regression + Aggregation Metrics

**Inputs:**
- Number of children engaged
- Sentiment/emotion scores
- Number of events & frequency
- Donations and sponsorship levels
- Repeat participation rate

**Output:**
- Impact score per:
  - Institution
  - Sponsor
  - Region
  - Festival
- Trend lines over time

**Usage:**
- CSR dashboards
- NGO impact reporting
- Internal prioritisation of regions / institutions

---

## 7. Training & Evaluation Strategy (Common to All Models)

**Data Handling:**
- Anonymised and privacy-preserving
- Train/validation/test split
- K-fold cross-validation for robustness

**Evaluation Metrics:**
- Classification: Accuracy, F1-score, ROC-AUC
- Recommendation: Precision@K, Recall@K, NDCG
- Regression: MAE, RMSE
- Fairness: bias checks across demographic or institution groups

**Deployment:**
- Served via REST APIs (FastAPI/Flask)
- Monitored for drift and performance degradation
- Periodic retraining scheduled (e.g., monthly / per festival season)

---

This document defines the **model layer** of JoyBridge.  
`ai_architecture.md` describes *how* these models are wired into the overall system; `models.md` explains *what* each model does and how it behaves.

