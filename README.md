# IT Recruitment Data Pipeline & Exploratory Analysis

## Project Overview

This project builds a complete end-to-end data pipeline for Vietnamese IT recruitment data, from raw job posting collection to automated information extraction, preprocessing, and exploratory data analysis (EDA).

The workflow combines:
- Manual data collection
- Human annotation & Ground Truth construction
- Large Language Model (LLM) information extraction
- Data cleaning & missing value imputation
- Exploratory Data Analysis (EDA)

The final output is a cleaned and enriched dataset of 250 IT recruitment postings.

---

# Objectives

The project aims to:

- Build a reproducible recruitment data pipeline
- Evaluate the capability of LLMs in structured information extraction
- Analyze the Vietnamese IT job market
- Explore salary trends, skill demand, and language requirements
- Create a dataset suitable for Machine Learning and NLP tasks

---

# Dataset Information

## Raw Dataset

- Source platforms:
  - ITviec
  - TopDev
- Total records collected: **250**
- Collection method: **Semi-manual extraction**
- File:
  - `Data_Raw.csv`

## Final Processed Dataset

- File:
  - `it_recruitment_processed.csv`
- Total rows:
  - 250
- Final columns:
  - Job information
  - Salary ranges
  - Extracted skills
  - Experience requirements
  - Language requirements

---

# Project Structure

```text
DS108_IT_Recruitment_Preprocessing/
│
├── data/
│   ├── 01_raw/
│   │   └── Data_Raw.xlsx
│   │
│   ├── 02_annotation/
│   │   ├── 100__unannotated_samples.xlsx
│   │   ├── 100__annotated_samples_Phuc.xlsx
│   │   ├── 100__annotated_samples_Phong.xlsx
│   │   └── GroundTruth_100.xlsx
│   │
│   ├── 03_interim/
│   │   └── 150_llm_extracted.xlsx
│   │   └── 250_merged_raw.xlsx
│   │   └── AI_100.xlsx
│   │   └── 150_jobs_for_pipeline.xlsx
│   │
│   └── 04_processed/
│       └── it_recruitment_processed.xlsx
│
├── notebooks/
│   ├── 01_Data_Acquistion.ipynb
│   ├── 02_GroundTruth_Annotation.ipynb
│   ├── 03_LLM_Information_Extraction.ipynb
│   ├── 04_Data_Cleaning_and_Imputation.ipynb
│   └── 05_Exploratory_Data_Analysis.ipynb
│
├── README.md
├── requirements.txt
├── data_dictionary.md
└── .env
```

---

# Pipeline Phases

## Phase 1 — Data Acquisition

- Collected 250 IT job postings manually
- Preserved raw text without modification
- Maintained original formatting and salary representation
- Verified dataset integrity and duplicate records

---

## Phase 2 — Data Splitting & Ground Truth Creation

### Dataset Split

- 100 samples → Human annotation set
- 150 samples → Automated pipeline set

### Human Annotation

Two annotators independently labeled:
- Job Domain
- Minimum Experience
- Language Requirement
- Skills

### Agreement Evaluation

Metrics used:
- Cohen’s Kappa
- Jaccard Similarity

### Ground Truth

Conflicts were manually resolved to produce:
- `GroundTruth_100.csv`

---

## Phase 3 — LLM Extraction & Evaluation

### Model Used

- Gemini 3.1 Flash Lite
- Deterministic mode:
  - `temperature = 0.0`

### Extraction Tasks

The LLM extracted:
- Job Domain
- Minimum Years of Experience
- Language Requirement
- Technical Skills

### Evaluation

AI outputs were compared against Ground Truth using:
- Cohen’s Kappa
- Jaccard Similarity

### Results

- Kappa scores > 0.83
- Skills Jaccard Similarity > 76%

The extraction pipeline demonstrated strong alignment with human annotations.

---

## Phase 4 — Data Cleaning & Missing Value Imputation

### Cleaning Tasks

- Province normalization
- Salary parsing
- Currency standardization
- Duplicate handling
- Feature transformation

### Salary Processing

Raw salary strings were converted into:
- `Salary_Min_VND`
- `Salary_Max_VND`

All salaries were standardized into:
- Monthly VND

### Missing Value Imputation

Applied:
- Groupby Median Imputation
- Nearest Experience Matching
- Market Median Fallback

---

## Phase 5 — Exploratory Data Analysis (EDA)

The analysis explored:

### 1. Job Market Landscape
- Most demanded job domains
- Hiring location distribution

### 2. Salary Benchmarks
- Median salary by domain
- Salary range comparison

### 3. Skill Demand
- Top requested skills per domain

### 4. Language Advantage
- Salary comparison by language requirement

### 5. Skill Co-occurrence
- Frequently paired technical skills

---

# Technologies Used

## Programming Language

- Python 3

## Libraries

- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- google-genai
- python-dotenv
- tqdm
- openpyxl

---

# Installation

## 1. Clone Repository

```bash
git clone https://github.com/phonghoangKHDL/IT_Recruitment_Preprocessing
cd IT_Recruitment_Preprocessing
```

## 2. Install Dependencies

```bash
pip install -r requirements.txt
```

---

# Environment Setup

Create a `.env` file:

```env
GEMINI_API_KEY=your_api_key_here
```

Get your API key from:
https://aistudio.google.com/api-keys

# Running the Project

Run notebooks sequentially:

1. `01_Data_Acquisition.ipynb`
2. `02_Data_Splitting_and_GroundTruth.ipynb`
3. `03_LLM_Information_Extraction.ipynb`
4. `04_Data_Cleaning_and_Imputation.ipynb`
5. `05_Exploratory_Data_Analysis.ipynb`

---

# Final Output

Final processed dataset:

```text
data/04_processed/it_recruitment_processed.csv
```

---

# Potential Applications

- Recruitment Analytics
- Salary Prediction
- Skill Demand Forecasting
- NLP Information Extraction
- Job Recommendation Systems
- Labor Market Research

---

# Notes

- Salary information was heavily missing (~75%)
- Many salaries were disclosed as:
  - Negotiable
  - Competitive
  - Thỏa thuận
- Imputation was used for statistical analysis purposes only
- LLM extraction performance depends on prompt quality and annotation consistency

---

# Authors

- Dinh Hoang Phong
- Nguyen Dinh Tuan Phuc

---

# License

This project is for academic and educational purposes.