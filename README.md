# Shark Attacks | Mini Project Overview
This project focuses on exploratory data analysis and data cleaning, transforming the Global Shark Attack File (GSAF5.xls) into a structured, reliable, and analysis‑ready dataset to support strategic decisions for the fictional company Second Tide.<br><br>
The initial inspection revealed 7,090 rows and 23 columns, containing inconsistent formats, missing values, and noisy variables. From there, we performed a full data‑wrangling workflow to clean, normalize, and prepare the data for deeper statistical exploration.

### Mini Project Goals
- Explore the dataset's original structure <br>
- Identify and correct inconsistencies and missing values <br>
- Normalize key variables <br>
- Reduce the dataset to relevant columns <br>
- Prepare the data for future modeling <br>

### Main Analytical Questions
- Which countries report the highest number of shark attacks?<br>
- How fatality rates vary by country?<br>
- Which age groups are most affected?<br>
- How gender distribution differs across countries?<br>
- What is the most common victim profile?<br>
- What patterns emerge from the overall dataset?<br>

### Data Wrangling Methods
- Data cleaning<br>
- Dropping irrelevant columns<br>
- Standardizing column names<br>
- Creating dataframe copies to avoid mutation<br>
- Temporal filtering (records from year 2000 onwards)<br>
- Duplicate removal with `drop_duplicates()`<br>
- Null imputation with fallback logic (Year → 1900; Sex → "Unknown"; Fatal Y/N → derived from Injury text)<br>
- String normalization (`.str.title()`, `.str.strip()`) applied to Country column<br>
- Regex-based whitespace cleaning inside normalization functions<br>
- Custom docstring-documented classification functions<br>
- Groupby analysis (Country, Gender, Age, Fatality)<br>
- Exploratory Data Analysis (EDA)<br>
- Building summary tables<br>

### Variable Transformation (Feature Engineering)
- Age grouping into Child, Teenager, Adult, Senior<br>
- Extraction of Top 5 countries based on attack frequency<br>
- `injury_normalized` — free-text Injury descriptions mapped to 17 standardized categories (Fatal, Laceration, Amputation subtypes, etc.)<br>
- `injury_group` — broader grouping of `injury_normalized` into 4 buckets: Amputation, Severe Injury, Minor Injury, and Fatal/No Injury/Unknown<br>
- `activity_normalized` — Activity column normalized into standard categories (Surfing, Swimming, Diving, etc.)<br>
- `Species_normalized` — Species column normalized into standardized shark type labels<br>
- `Fatal Y/N` re-classification — null values filled using a `classify_fatal()` function based on injury text keywords<br>

### Columns Retained in Final Dataset
After cleaning, the working DataFrame includes the following columns:

| Column | Description |
|---|---|
| `Year` | Year of incident (2000 onwards, cast to int) |
| `Country` | Normalized country name (title case, stripped) |
| `Activity` | Original activity description |
| `activity_normalized` | Standardized activity category |
| `Sex` | Gender of victim (nulls replaced with "Unknown") |
| `Age` | Numeric age (imputed from text values) |
| `Age_Group` | Derived group: Child, Teenager, Adult, Senior |
| `Injury` | Original injury description |
| `injury_normalized` | Standardized injury category |
| `injury_group` | Broad injury category for business analysis |
| `Fatal Y/N` | Fatality status (Y / N / Unknown) |
| `Species` | Original species description |
| `Species_normalized` | Standardized shark species label |
| `Location` | Retained for potential future campaigns |

### Libraries Used
```python
import pandas as pd
import numpy as np
import re
import matplotlib.pyplot as plt
```

### Analysis Techniques Used
```python
groupby().size().unstack()
value_counts()
Filtering with .isin()
Aggregations and pivot‑style tables
Custom keyword-matching normalization functions (classify_fatal, normalize_injury, injury_category, normalize_activity)
Horizontal bar charts with matplotlib
```

### Key Business Findings
- **USA and Australia** are the strongest target markets by volume, with 110 and 55 potential prosthetic clients respectively — 85% of all severe injury and amputation cases combined.
- Both countries show high survival rates (USA: 82.5%, Australia: 74.8%), meaning more survivors who may need prosthetic support.
- **Bahamas and Brazil** show higher injury rates but lower case volumes — better suited as secondary test markets.
- **Arm and leg amputations** are the most frequent amputation types (20 cases each), followed by hand amputations (12).
- **Surfing** has the highest overall incident count (996 total, 790 non-fatal); **swimming** has the most fatalities (105).
- The most common victim profile is **males in their 30s**.

### How to Open This Project
- Open the project folder in Google Drive
- Open the notebook `Shark_attack_final.ipynb`
- Run the cells sequentially
- Ensure the dataset `GSAF5.xls` is in the same folder

### Authors
Ana Claudia Paniagua Russo <br>
Juan Francisco Calvo Sánchez <br>
Winifred Paul Thattil <br>
