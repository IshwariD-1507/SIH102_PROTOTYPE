# 🔎 MPLADS Project Monitoring & Risk Intelligence System

### Smart India Hackathon 2026 — SIH26102

> **Detect unusual project patterns → explain why they were flagged → prioritize them for human verification.**

An AI-assisted decision-support platform for monitoring **MPLADS projects** and identifying unusual financial, execution, cost, data-quality, and project-overlap patterns.

⚠️ **This system flags risk signals — it does not declare fraud. Final verification remains with authorized officials.**

---

## 🚀 What Does It Do?

The system transforms thousands of MPLADS records into an **explainable review queue**.

```text
MPLADS Data
     ↓
Data Cleaning & Unification
     ↓
Feature Engineering
     ↓
Cost & Lifecycle Analysis
     ↓
Semantic Overlap Detection
     ↓
Explainable Risk Scoring
     ↓
Low / Medium / High / Critical
     ↓
Human Review Dashboard
```

### ✨ Key Features

| Feature                  | Purpose                                                  |
| ------------------------ | -------------------------------------------------------- |
| 📊 Executive Dashboard   | Monitor projects, amounts, status & risk distribution    |
| 🚨 Risk Alerts           | Prioritize Medium, High & Critical projects              |
| 🔍 Project Investigation | Search projects across multiple fields                   |
| 🔗 Duplicate Detection   | Identify potentially overlapping projects                |
| 💰 Cost Analysis         | Compare project costs with peer-group benchmarks         |
| ⏱️ Delay Analysis        | Detect unusually long project durations                  |
| 🗺️ GIS Risk Map         | Visualize projects geographically when coordinates exist |
| 👤 Role-Based Access     | District-level access for officers                       |
| 💡 Explainable Alerts    | Show *why* a project was flagged                         |

---

## 🤖 AI / ML

### Semantic Project Overlap

Project descriptions are converted into semantic embeddings using:

**Sentence Transformers → `all-MiniLM-L6-v2`**

```text
Project Description
       ↓
Text Cleaning
       ↓
384-D Embedding
       ↓
Cosine Similarity
       ↓
Potential Overlap
```

The overlap score combines:

* 📝 Semantic similarity — **60%**
* 💰 Cost similarity — **25%**
* 📅 Date similarity — **15%**

Projects are first grouped by **State + Work Category** to make comparisons more relevant.

> Semantic similarity indicates a **potential overlap**, not confirmed duplication.

### 🌐 Multilingual Support

The codebase also contains an experimental multilingual pipeline using:

* AI4Bharat IndicXlit
* AI4Bharat IndicTrans2
* PyTorch / Transformers

This module is currently **not connected to the active duplicate-detection pipeline**.

---

## 📈 Explainable Risk Engine

Instead of a black-box prediction, the prototype uses a **0–100 explainable risk score**.

### Risk Signals

* 💵 Financial anomaly
* 💰 Cost deviation
* ⏱️ Delay / unusual duration
* 🔗 Potential project overlap
* 📋 Missing project information
* 📸 Missing completion evidence

### Risk Levels

|  Score | Risk        |
| -----: | ----------- |
|   0–30 | 🟢 Low      |
|  31–60 | 🟡 Medium   |
|  61–80 | 🟠 High     |
| 81–100 | 🔴 Critical |

Every flagged project receives human-readable **Risk Reasons**, allowing an officer to understand what triggered the alert.

---

## 📊 Current Prototype

| Metric                  |       Value |
| ----------------------- | ----------: |
| Unified Projects        |  **27,001** |
| Engineered Features     |      **56** |
| Potential Overlap Pairs | **129,117** |
| Review Queue            |   **5,393** |
| Critical Projects       |       **1** |

*Values are specific to the current prototype dataset and change when data is refreshed.*

---

## 🗂️ Data Sources

The prototype currently works with:

* `Works Recommended.csv`
* `Works Sanctioned.csv`
* `Works Completed.csv`
* `Allocated Limit for Honble MPs.csv`
* `Amount consented for Calamity.csv`

The main project table is built by combining **Recommended + Sanctioned + Completed** records using `Work_ID`.

---

## 🛠️ Technology Stack

**Data & Backend**

`Python` · `Pandas` · `NumPy` · `PyYAML`

**AI / ML**

`Sentence Transformers` · `scikit-learn` · `PyTorch` · `Hugging Face Transformers`

**Dashboard & GIS**

`Streamlit` · `Folium` · `streamlit-folium`

**Storage**

`CSV` · `YAML`

---

## 📁 Project Structure

```text
Sih_102Prototype/
│
├── app/
│   ├── main.py
│   ├── components/
│   └── pages/
│
├── data/
│   ├── raw/
│   ├── processed/
│   └── synthetic/
│
├── pipelines/
│   ├── build_dataset.py
│   ├── build_features.py
│   ├── test_duplicates.py
│   └── build_review_queue.py
│
├── src/mplads/
│   ├── data/
│   ├── features/
│   ├── models/
│   ├── risk/
│   ├── verification/
│   └── geo/
│
├── configs/
├── docs/
├── notebooks/
├── requirements.txt
└── README.md
```

---

## ⚡ Quick Start

### 1. Clone

```bash
git clone <your-repository-url>
cd Sih_102Prototype
```

### 2. Create Virtual Environment

**Windows**

```bash
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**macOS / Linux**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Add Data

Place the required CSV files inside:

```text
data/raw/
```

### 5. Run the Pipeline

```bash
python pipelines/build_dataset.py
python pipelines/test_duplicates.py
python pipelines/build_features.py
python pipelines/build_review_queue.py
```

### 6. Launch Dashboard

```bash
streamlit run app/main.py
```

---

## 🎯 Judge Demonstration Flow

```text
Login
  ↓
Executive Dashboard
  ↓
Risk Alerts
  ↓
Select High/Critical Project
  ↓
View Risk Reasons
  ↓
Project Investigation
  ↓
Duplicate / Overlap Analysis
  ↓
Delay & Financial Analysis
  ↓
GIS View
```

### The key idea:

**Detection → Explanation → Prioritization → Human Investigation**

---

## 🔐 Responsible AI & Safeguards

The system is designed as a **screening and decision-support tool**.

It:

* ❌ Does not declare fraud
* ❌ Does not fabricate missing coordinates
* ❌ Does not invent physical progress percentages
* ✅ Provides explainable risk reasons
* ✅ Keeps human officers in the decision loop
* ✅ Supports district-level access control

---

## ⚠️ Current Limitations

This is a **hackathon prototype**, not a production fraud-detection system.

Currently:

* Risk scoring is rule-based.
* Delay detection uses statistical thresholds.
* Cost anomaly detection uses peer-group benchmarks.
* Semantic similarity identifies *potential* overlaps.
* Authentication uses a mock database.
* Data storage is CSV-based.
* Several ML/verification modules are experimental or scaffolded.

---

## 🔮 Future Scope

* Train validated anomaly-detection models
* Add predictive delay modelling
* Integrate multilingual NLP into duplicate detection
* Add precision / recall / F1 evaluation
* Add verified GPS and image-based evidence verification
* Introduce database-backed scalable storage
* Add secure authentication and audit logs
* Add automated data refresh and model monitoring

---

## 🏆 Why It Matters

MPLADS monitoring involves large volumes of project information.

Instead of manually examining every record, this system helps officials:

**Find unusual projects faster → understand why → prioritize verification → make informed decisions.**

> **AI-assisted monitoring, with humans always in the loop.**

---

### 📌 Project Status

**Smart India Hackathon 2026 · Prototype · Educational / Research / Demonstration**

The system is intended to support administrative monitoring. Final conclusions require verification against authoritative records and appropriate human review.


For production use, the project should undergo appropriate security, data-governance, model-
validation, privacy, authorization and infrastructure reviews.
