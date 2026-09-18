# Analyzing International Students' Mental Health 📊🧠

## 📌 Project Overview
This data science project investigates how the length of stay (`stay`) impacts the mental health indicators of international students at an international university. 

Using data collected from a 2019 survey, the analysis tracks three major psychometric tests against students' time spent abroad to uncover trends in depression, social connectedness, and acculturative stress.

---

## 🛠️ The Data & Schema
The dataset contains survey metrics using three primary scales:
*   **PHQ-9 (Patient Health Questionnaire)**: Measures depression severity (Column: `todep`, higher is more severe).
*   **SCS (Social Connectedness Scale)**: Measures a student's sense of belonging (Column: `tosc`, higher is more connected).
*   **ASISS (Acculturative Stress Index for International Students)**: Measures stress associated with adapting to a new culture (Column: `toas`, higher is more stressed).

---

## 💻 SQL Query Solution
The final aggregated table isolates only international students, groups them by their length of stay, calculates their diagnostic averages, and sorts them sequentially to uncover behavioral trends.

```sql
SELECT 
    stay, 
    COUNT(*) AS count_int, 
    ROUND(AVG(todep), 2) AS average_phq, 
    ROUND(AVG(tosc), 2) AS average_scs, 
    ROUND(AVG(toas), 2) AS average_as
FROM students
WHERE inter_dom = 'Inter'
GROUP BY stay
ORDER BY stay DESC;
```

---

## 📈 Analysis & Key Findings

| stay (Years) | count_int (Sample Size) | average_phq (Depression) | average_scs (Belonging) | average_as (Stress) |
| :---: | :---: | :---: | :---: | :---: |
| **10** | 1 | 13.00 | 32.00 | 50.00 |
| **8** | 1 | 10.00 | 44.00 | 65.00 |
| **7** | 1 | 4.00 | 48.00 | 45.00 |
| **6** | 3 | 6.00 | 38.00 | 58.67 |
| **5** | 1 | 0.00 | 34.00 | 91.00 |
| **4** | 14 | 8.57 | 33.93 | 87.71 |
| **3** | 46 | 9.09 | 37.13 | 78.00 |
| **2** | 39 | 8.28 | 37.08 | 77.67 |
| **1** | 110 | 9.28 | 37.45 | 72.85 |

### 🔍 Core Insights:
1. **The 4-to-5 Year Culture Shock Peak**: Acculturative stress reaches its absolute highest points during years 4 (`87.71`) and 5 (`91.00`). This is a critical statistical finding, showing that long-term international students may face a delayed, acute strain as graduation approaches or visa pressures mount.
2. **The Year 1 Population Influx**: The vast majority of the data sits in Year 1 (`count_int = 110`). Students arriving in their first year show moderate depression scores (`9.28`) and baseline culture stress, setting the benchmark for the rest of the study.
3. **Long-term Resilience and Drop-off**: By years 6 through 10, the sample size drops significantly. The surviving data points suggest a general stabilizing of mental health metrics (such as a perfect depression score of `0.00` in Year 5 and a low score of `4.00` in Year 7), reflecting either graduation filtering or long-term coping adaptation.

---

## 🧰 Tech Stack & Concepts Demonstrated
*   **Language**: PostgreSQL
*   **Aggregations**: `COUNT(*)`, `AVG()`, `ROUND()`
*   **Data Wrangling**: `GROUP BY`, `ORDER BY DESC`, `WHERE` filtering
*   **Domain**: Healthcare Analytics / Behavioral Data Science
