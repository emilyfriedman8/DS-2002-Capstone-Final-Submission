# DS-2002-Capstone-Final-Submission

## Overview
This project analyzes electric vehicle (EV) charging station usage using a full ETL (Extract, Transform, Load) pipeline. We integrate multiple datasets, clean and standardize inconsistent data, and generate insights through five analytical questions focused on demand patterns, vehicle usage, weather impacts, geographic trends, and connector types.

The goal is to demonstrate how real-world data pipelines support meaningful analysis and decision-making.

---

## Project Structure

```
DS-2002-Capstone-Final-Submission/
│
├── 5_Analytical_Questions.ipynb        # Main analysis notebook (all 5 questions + visualizations)
├── GCS_Authentication_and_Data_Cleaning_Pipeline.ipynb  # ETL pipeline (GCS + cleaning + transformation)
├── DS 2002 Capstone_ Reflection Write-Up.pdf  # Written reflection
├── DS 2002 Final Project Slides.pdf   # Presentation slides
├── README.md                          # Project documentation
```

---

## Data Sources

This project uses multiple datasets stored in Google Cloud Storage:

- `charging_sessions.csv` — session-level charging data  
- `station_locations.csv` — station metadata (location, region)  
- `vehicle_types.csv` — vehicle ID reference table  
- `grid_operators.csv` — operator and capacity information  
- `energy_and_demand.db` — SQLite database with demand and grid tables  

Additionally, weather data is pulled from the Open-Meteo API.

---

## Pipeline Overview

### 1. Extract
- Authenticate with Google Cloud Storage (GCS)
- Download raw datasets into the local environment
- Pull weather data via API

### 2. Transform (Data Cleaning)
Key cleaning steps include:
- Removing duplicate records
- Standardizing datetime formats
- Fixing mixed data types and currency formatting
- Handling missing values
- Converting negative `kwh_delivered` values to positive
- Vehicle ID consolidation:
  - Standardizing inconsistent IDs
  - Mapping to clean vehicle names

### 3. Load
- Store cleaned datasets in SQLite database (`ev_analytics.db`)
- Export cleaned CSV for reproducibility
- Upload outputs back to GCS

---

## Analytical Questions

The notebook `5_Analytical_Questions.ipynb` answers:

1. **Demand Surge Identification**  
   Identifies peak charging periods relative to baseline usage

2. **Vehicle Consolidation Problem**  
   Shows how cleaning vehicle IDs changes demand insights

3. **Weather and Grid Correlation**  
   Analyzes relationship between temperature and charging demand

4. **Station-Level Geographic Patterns**  
   Compares usage across locations and identifies top/bottom stations

5. **Connector Type Investigation**  
   Evaluates trends in connector usage (e.g., CHAdeMO vs others)

---

## Key Insights

- Charging demand shows clear seasonal and surge patterns  
- Vehicle ID inconsistencies significantly distort analysis if not cleaned  
- Temperature has weak direct correlation with charging demand  
- Station performance varies more by location than by general trends  
- Connector usage remains relatively stable over time  

---

## How to Run the Project

### 1. Open in Google Colab
This project is designed to run in Google Colab.

### 2. Install Dependencies
```python
!pip install google-cloud-storage pandas numpy matplotlib seaborn requests
```

### 3. Authenticate GCS
```python
from google.colab import auth
auth.authenticate_user()
```

### 4. Run Pipeline Notebook
Execute:
- `GCS_Authentication_and_Data_Cleaning_Pipeline.ipynb`

This will:
- Download raw data
- Clean and transform datasets
- Save outputs to SQLite and CSV
- Upload results to GCS

### 5. Run Analysis Notebook
Execute:
- `5_Analytical_Questions.ipynb`

---

## Technologies Used

- Python (pandas, numpy)
- SQLite
- Google Cloud Storage (GCS)
- Google Colab
- Matplotlib & Seaborn
- Open-Meteo API

---

## Key Takeaways

- Data cleaning is critical and small inconsistencies can significantly distort results  
- Cloud pipelines improve collaboration but require careful path management  
- Real-world data is messy, and building robust pipelines is essential for reliable analysis  
