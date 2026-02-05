# delhivery-logistics-case-study

📌 **Project Overview**
- This project analyzes a logistics dataset from Delhivery to understand operational efficiency, validate routing models, and identify key areas for process improvement. The analysis focuses on comparing OSRM (Open Source Routing Machine) estimates against actual trip data to detect discrepancies in time and distance predictions.
- The study involves extensive data cleaning, feature engineering, exploratory data analysis (EDA), and statistical hypothesis testing to derive actionable business insights.

 🛠️ **Tech Stack**
- **Language:** Python
- **Libraries:**
    - pandas, numpy (Data Manipulation)
    - matplotlib, seaborn (Visualization)
    - scipy.stats (Hypothesis Testing)
    - sklearn.preprocessing (Normalization)

📂 **Dataset Description**
- The dataset contains trip-level details including timestamps, route types, source/destination centers, and comparison metrics for predicted (OSRM) vs. actual operational performance.
- **Key Features:**
  - trip_uuid: Unique identifier for trips.
  - route_type: Transportation mode (FTL vs. Carting).
  - od_start_time / od_end_time: Trip start and end timestamps.
  - actual_time vs. osrm_time: Comparative metrics for travel duration.
  - actual_distance_to_destination vs. osrm_distance: Comparative metrics for travel distance.

📊**Key Analysis Steps**  
 **1. Data Cleaning & Preprocessing**
  - **Handling Missing Values:** Cleaned source_name and destination_name columns to remove nulls.
  - **Feature Extraction:** Split complex strings to extract City, State, and Place from source and destination identifiers.
  - **Time Calculation:** Derived od_time_diff to calculate total trip duration in minutes.    

**2.Exploratory Data Analysis (EDA)**
  - **Route Distribution:** Identified that FTL (Full Truck Load) orders constitute the majority of trips, being more than double the volume of Carting orders.
  - **Geographic Concentration:** Found that Karnataka, Haryana, and Maharashtra have the highest traffic, indicating strong intra-state connectivity requirements.
  - **Outlier Detection:** Used the IQR (Interquartile Range) method to identify and handle outliers in speed and distance metrics.  

**3. Hypothesis Testing**
  Statistical tests (Paired T-tests) were conducted to validate OSRM accuracy:
  - **OSRM vs. Actual Time:** Validated that actual travel times are statistically significantly higher than OSRM estimates ($p < 0.05$), likely due to traffic and operational delays.
  - **OSRM vs. Actual Distance:** Found that actual distances travelled are slightly lower than OSRM predictions.
  - **Segment vs. Trip Distance:** Confirmed a discrepancy where the aggregated segment OSRM distances do not match the total trip OSRM distance.

💡 **Key Insights & Recommendations**
- Based on the data, the following recommendations were proposed:
  - **Calibrate OSRM Models:** The routing engine consistently underestimates travel time and overestimates distance. The model requires recalibration to account for real-world traffic and operational bottlenecks.
  - **Optimize Intra-State Fleets:** Since state-level analysis shows high density in specific regions (e.g., Karnataka), deploying smaller trucks (Tempos) for intra-state connectivity could reduce costs and wait times.
  - **Delay Analysis:** Implementation of granular tracking to capture specific reasons for delays (e.g., roadblocks, breakdowns) is necessary to improve future time estimates.
