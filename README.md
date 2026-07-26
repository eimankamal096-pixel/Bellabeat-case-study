# 🌸 Bellabeat Case Study: How Can a Wellness Technology Company Play It Smart?

📄 **[Click here to view the full PDF Report](./Bellabeat_project_Report_and_Findings.pdf)**

---

## 📌 Project Overview
This case study is part of the **Google Data Analytics Professional Certificate**. The primary objective is to analyze smart device usage data from non-Bellabeat devices (specifically FitBit data) to uncover consumer habits, usage trends, and activity patterns. 

The focus of this analysis is applied directly to the **Bellabeat Leaf**—a smart wellness tracker designed for women that monitors activity, sleep, and stress. The insights gained are used to provide high-level, data-driven marketing recommendations to guide Bellabeat’s growth strategy.

---

## 📑 Data Analysis Process
This project follows the 6-phase Google Data Analytics methodology:
[1. Ask] ➔ [2. Prepare] ➔ [3. Process] ➔ [4. Analyze] ➔ [5. Share] ➔ [6. Act]
---

### 1. ❓ The Ask Phase
* **Business Task:** Analyze consumer smart device usage to identify growth opportunities for Bellabeat.
* **Core Questions:**
  1. What are some key trends in smart device usage?
  2. How could these trends apply to Bellabeat customers?
  3. How can these trends influence Bellabeat’s marketing strategy?
* **Selected Product:** **Bellabeat Leaf** (aligns with step, activity, and sleep monitoring features).

---

### 2. 📂 The Prepare Phase
* **Data Source:** Public dataset available on Kaggle via Mobius containing personal tracker data from FitBit users.
* **Data Integrity (ROCCC Analysis):**
  * **Reliable:** *Medium* (Small sample size of ~33 users).
  * **Original:** *Low* (Third-party Amazon Mechanical Turk data).
  * **Comprehensive:** *Medium* (Tracks steps, calories, and sleep; lacks gender/demographic data).
  * **Current:** *Low* (Collected in 2016).
  * **Cited:** *High* (Well-documented and public domain).

---

### 3. 🛠 The Process Phase
* **Tools Used:** 
  * **SQL (BigQuery):** Data cleaning, transformation, and analysis.
  * **Tableau:** Data visualization and dashboard creation.
  * **Google Docs / PDF:** Report documentation.
* **Cleaning & Integrity Steps:**
  * Checked for `NULL` / missing values across critical identifiers.
  * Removed duplicate entries.
  * Transformed `ActivityDate` from string format to `DATE` data type.
  * Verified unique user counts (`COUNT(DISTINCT Id)`).

---

### 4. 🔍 The Analyze Phase & Key Insights

#### A. User Participation & Daily Averages:
* Verified **33 unique users** in the `daily_activity` dataset.
* **Average Daily Steps:** `7,638 steps` (below the recommended 10,000 steps/day target).
* **Average Daily Distance:** `5.49 km`.
* **Average Daily Calories:** `2,303 kcal`.

```sql
-- Query: Daily Activity Summary Statistics
SELECT
  COUNT(DISTINCT Id) AS total_users,
  ROUND(AVG(TotalSteps), 0) AS avg_steps,
  ROUND(AVG(TotalDistance), 2) AS avg_distance,
  ROUND(AVG(Calories), 0) AS avg_calories
FROM
  `my-project-2-492717.fit_bit_data.daily_activity`;

### B. Weekly Activity Patterns & "The Sunday Slump"
Peak Days: Users are most active on Tuesdays (8,125 steps) and Saturdays (8,153 steps).

Lowest Day: A noticeable drop in activity occurs on Sundays (6,933 steps) — a ~15% drop from peak days.

-- Query: Average Steps by Day of Week
SELECT
  FORMAT_DATE('%A', ActivityDate) AS day_of_week,
  ROUND(AVG(TotalSteps), 0) AS avg_steps
FROM
  `my-project-2-492717.fit_bit_data.daily_activity`
GROUP BY
  day_of_week
ORDER BY
  avg_steps DESC;


## 📊 Phase 5: Share (Data Visualization)

The chart highlights the **Sunday Slump**, showcasing the drop in average steps over the weekend rest period:

*(Note: Visualized in Tableau with Y-axis scaled between 6,000 - 8,500 steps to clearly emphasize weekly behavioral variances).*

---

## 🎯 Phase 6: Act (Final Recommendations)

Based on the findings, the following marketing strategies are recommended for the **Bellabeat Leaf**:

1. **Targeted "Sunday Motivation" Push Notifications:**
   * *Insight:* Significant activity drop on Sundays (6,933 steps).
   * *Action:* Configure the Bellabeat App to send friendly Sunday morning reminders or mini-challenges to encourage users to stay active on rest days.

2. **Inactivity & Sedentary Alerts:**
   * *Insight:* Users spend a majority of their day in sedentary minutes.
   * *Action:* Highlight the **Leaf's vibration alert feature** in marketing campaigns, positioning it as a tool to break long sitting hours for improved health.

3. **The "Bridge the Gap to 10K" Campaign:**
   * *Insight:* Average user steps (7,638) fall short of the 10,000 daily goal.
   * *Action:* Introduce gamified app badges and digital rewards for users making the leap from 7,000 to 10,000 steps.

4. **Personalized Sleep-Activity Correlations:**
   * *Insight:* Higher physical activity directly impacts deep sleep cycles.
   * *Action:* Deliver meaningful in-app summaries (e.g., *"Walking 2,000 more steps today improved your deep sleep quality by 15%!"*).

---

## ✍️ Author
**Eiman Kamal Hassan**  
*Data Analyst*
