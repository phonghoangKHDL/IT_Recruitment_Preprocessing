# Data Dictionary

## Dataset Information

### Dataset Name
IT Recruitment Processed Dataset

### File Name
`it_recruitment_processed.csv`

### Description
This dataset contains a cleaned and standardized collection of Vietnamese IT recruitment postings gathered from online recruitment platforms, primarily ITviec and TopDev.

The dataset was constructed through a multi-phase preprocessing pipeline that integrates:

- Semi-manual raw data collection
- Human-validated Ground Truth annotation
- LLM-assisted information extraction using Gemini 3.1 Flash Lite
- Statistical missing value imputation
- Salary normalization and location standardization

The final dataset is designed to support exploratory data analysis, labor market research, and machine learning applications related to the Vietnamese IT sector.

---

# Dataset Dimensions

| Property | Value |
|---|---|
| Total Records | 250 |
| Dataset Type | Structured Tabular Dataset |
| Domain | IT Recruitment / Labor Market |
| Language | Vietnamese + English |
| Format | CSV |

---

# Column Descriptions

| Column Name | Data Type | Description |
|---|---|---|
| `Job_Title` | string | Original title of the job posting provided by the employer |
| `Job Domain` | categorical string | Standardized job category extracted from the job description |
| `Company` | string | Name of the company posting the job |
| `Location` | categorical string | Standardized job location mapped to Vietnamese administrative provinces |
| `Min years of exp` | float | Minimum years of experience required for the role |
| `Language Requirement` | categorical string | Foreign language requirement extracted from the posting |
| `Skills` | categorical string | Comma-separated list of standardized technical skills extracted by the LLM |
| `Link` | string | Original URL of the recruitment post used for provenance tracking |
| `JD & Requirements` | string | Original unstructured job description and requirements |
| `Salary_Min_VND` | float | Estimated or parsed minimum monthly salary in VND |
| `Salary_Max_VND` | float | Estimated or parsed maximum monthly salary in VND |

---

# Job Domain Categories

The `Job Domain` column contains one of the following standardized categories:

- Software Development
- Data & AI
- Infrastructure
- Testing & Quality
- Management & Analysis
- Design & UX
- Others

---

# Language Requirement Categories

The `Language Requirement` column contains one of the following values:

- English
- Japanese
- Korean
- French
- None

---

# Skills Taxonomy

Technical skills were extracted using a predefined whitelist of 78 standardized IT skills, including:

- Programming Languages: Python, Java, C/C++, JavaScript, Golang
- Cloud Platforms: AWS, Azure, GCP
- DevOps Tools: Docker, Kubernetes, CI/CD, Terraform
- Data Technologies: SQL, Data Engineering, Machine Learning
- Web Technologies: ReactJS, NodeJS, VueJS, NextJS
- Testing Frameworks: Automation Test, API Testing, Unit Test

The `Skills` field may contain multiple comma-separated values for a single record.

---

# Important Notes

## Salary Information
Approximately 75% of the original job postings did not contain explicit salary figures. Missing values were statistically estimated using domain-aware median imputation.

As a result:
- Salary columns represent estimated market distributions
- Values should not be interpreted as exact compensation figures

## Skill Extraction
Skills were extracted automatically using an LLM with a constrained whitelist-based extraction framework.

Although the extraction achieved strong agreement with human annotators:
- Minor extraction inconsistencies may still exist
- Emerging technologies outside the whitelist may not appear in the dataset

## Location Standardization
Free-text locations were mapped to standardized Vietnamese provinces and major cities. Remote and overseas postings were preserved as separate categories.

---

# Potential Use Cases

This dataset may be used for:

- Exploratory Data Analysis (EDA)
- Salary trend analysis
- IT labor market research
- Skill demand forecasting
- Job recommendation systems
- NLP and Information Extraction research
- Machine Learning applications
- Career pathway analysis

---

# Limitations

- Small dataset size (250 records)
- High missing salary rate
- Static temporal snapshot
- Limited platform coverage
- Possible LLM extraction edge-case errors

---

# Authors

- Dinh Hoang Phong
- Nguyen Dinh Tuan Phuc

Faculty of Information Science and Engineering  
University of Information Technology (UIT)  
Vietnam National University - Ho Chi Minh City

---