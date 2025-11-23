# 📂 JoyBridge – Dataset Structure & Schema

This document defines the data structure required for training and operating JoyBridge’s AI models. All datasets follow privacy-first and anonymised data policies.

---

## 1. USER DATASET (Families / Sponsors)

**File Name:** user_profiles.csv  
**Purpose:** User behavioural profiling & recommendation training

| Field Name            | Type        | Description |
|----------------------|------------|-------------|
| user_id              | UUID       | Unique user identifier |
| role                 | category   | family / sponsor |
| city                 | string     | User location |
| preferred_festivals  | list       | Festivals user prefers |
| max_children_allowed | integer    | For families |
| total_events_joined  | integer    | Participation count |
| donation_amount      | float      | Total donated |
| verification_status  | boolean    | Verified or not |
| safety_score         | float      | Derived risk indicator |
| last_active_date     | datetime   | Engagement tracking |

---

## 2. INSTITUTION DATASET

**File Name:** institution_profiles.csv  
**Purpose:** Risk prediction & matching optimisation

| Field Name            | Type      | Description |
|----------------------|----------|-------------|
| institution_id       | UUID     | Unique ID |
| city                 | string   | Location |
| capacity             | integer  | Number of children |
| registration_status  | boolean  | Legal verification |
| previous_events      | integer  | Event count |
| avg_feedback_score   | float    | Historical sentiment |
| last_incident_flag   | boolean  | Safety marker |
| risk_level           | category | Low / Medium / High |

---

## 3. EVENT DATASET

**File Name:** festival_events.csv  
**Purpose:** Core system workflow + AI matching

| Field Name         | Type      | Description |
|-------------------|----------|-------------|
| event_id          | UUID     | Event identifier |
| festival_name     | string   | Festival type |
| event_date        | date     | Scheduled date |
| institution_id    | UUID     | Hosting institution |
| available_slots   | integer  | Capacity |
| families_joined   | list     | IDs of families |
| event_status      | category | pending / approved / completed |
| safety_override   | boolean  | Admin control |

---

## 4. FEEDBACK & SENTIMENT DATASET

**File Name:** feedback_data.csv  
**Purpose:** Sentiment analysis & emotional impact scoring

| Field Name      | Type    | Description |
|----------------|--------|-------------|
| feedback_id    | UUID   | Feedback entry |
| event_id       | UUID   | Related event |
| user_id        | UUID   | Author |
| rating         | integer| 1–5 stars |
| text_feedback  | string | Emotional review |
| sentiment_score| float  | AI-generated |
| emotion_label  | string | Joy / Calm / Concern etc |

---

## 5. IMAGE MODERATION DATASET

**File Name:** memory_wall_images.csv  
**Purpose:** Image moderation & safety filtering

| Field Name      | Type    | Description |
|----------------|--------|-------------|
| image_id       | UUID   | Image identifier |
| event_id       | UUID   | Related event |
| uploaded_by    | UUID   | User |
| moderation_flag| category | allow / blur / block |
| face_detected  | boolean | Privacy control |
| approval_status| boolean | Admin decision |

---

## 6. DONATION DATASET

**File Name:** donations.csv  
**Purpose:** Campaign optimisation & prediction model

| Field Name     | Type    | Description |
|---------------|---------|-------------|
| donation_id   | UUID    | Record ID |
| user_id       | UUID    | Donor |
| amount        | float   | Donated value |
| event_id      | UUID    | Sponsored event |
| date          | datetime| Timestamp |
| campaign_type | string  | Festival / Emergency |

---

## 7. MATCHING & MODEL TRAINING DATASET

**File Name:** training_matches.csv  
**Purpose:** Smart matching model learning

| Field Name        | Type      | Description |
|------------------|----------|-------------|
| family_id        | UUID     | Family |
| institution_id   | UUID     | Institution |
| event_id         | UUID     | Event |
| match_score      | float    | AI prediction |
| success_flag     | boolean  | Event completed successfully |

---

## Data Privacy & Governance

- All personal data anonymised using hashed IDs
- No facial recognition storage without consent
- Compliance with:
  - Child safety regulations
  - Data protection policies
- Regular audits & encryption enforced

---

This dataset structure supports:
✅ Recommendation systems  
✅ Risk analysis  
✅ Sentiment modelling  
✅ Impact reporting  
✅ Ethical AI governance  

JoyBridge’s AI operates on structured, compliant, and interpretable datasets.

