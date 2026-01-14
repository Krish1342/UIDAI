# Geospatial Equity Analysis - Detailed Methodology

## Overview

This document outlines the technical approach for analyzing Aadhaar service delivery equity using geospatial methods.

---

## Phase 1: Geospatial Data Preparation

### 1.1 Data Integration

- **Combine datasets**: Merge biometric, demographic, and enrolment data
- **Aggregate by pincode**: Group all activity by geographic unit (pincode)
- **Calculate metrics**:
  - Total enrollments per pincode
  - Total biometric updates per pincode
  - Latest activity date
  - Geographic pincode status (active/inactive)

### 1.2 Coordinate Mapping

- **External data source**: Use pincode-to-coordinates mapping (India Post, Google, or pincode database)
- **Enrichment**: Add latitude/longitude to each pincode
- **Validation**: Remove records with invalid/missing coordinates

### 1.3 Preparation Outputs

```
Pincode-level dataset with columns:
- pincode (string)
- state (string)
- district (string)
- latitude (float)
- longitude (float)
- total_enrollments (int)
- total_biometric_updates (int)
- last_activity_date (datetime)
- status (active/inactive)
```

---

## Phase 2: Equity Analysis

### 2.1 Identify Underserved Regions

**Method 1: Activity-Based Classification**

```
For each pincode:
  IF enrollments == 0 OR last_activity > 2 years ago
    Classification = "Severely Underserved" (RED)
  ELIF enrollments < district_median * 0.5
    Classification = "Underserved" (ORANGE)
  ELIF enrollments < district_median
    Classification = "Moderately Served" (YELLOW)
  ELSE
    Classification = "Well-Served" (GREEN)
```

**Method 2: Service Density (enrollments/km²)**

- Calculate district area (sum of pincode areas or use boundary data)
- Compute density = total_enrollments / district_area_km2
- Classify pincodes relative to district average

**Method 3: Geographic Distance Analysis**

- For each underserved pincode, calculate distance to nearest "well-served" center
- Flag pincodes >50km from active centers as "access gaps"
- Generate priority list for intervention

### 2.2 Calculate Inequality Metrics

**Gini Coefficient** (0 = perfect equality, 1 = complete inequality)

```
Algorithm:
1. Sort pincodes by enrollment count (ascending)
2. Calculate cumulative sum
3. Use Gini formula: G = (2*Σ(i*xi)) / (n*Σxi) - (n+1)/n
   where xi = enrollment in pincode i, n = number of pincodes
```

**Urban vs. Rural Disparity**

- Classify pincodes as urban/rural (using population density or census data)
- Compare:
  - Enrollment rate urban vs rural
  - Update frequency urban vs rural
  - Avg time-to-first-update urban vs rural

**State-Level Equity Scores**

```
For each state:
  Equity_Score = (Avg_pincode_enrollment / State_avg) * (1 - Gini_coeff)
  Range: 0 (inequitable) to 1 (equitable)
```

### 2.3 Clustering & Anomaly Detection

**K-Means Clustering** (k=4: high/medium/low activity + inactive)

```
Features for clustering:
- total_enrollments (normalized)
- update_frequency (normalized)
- time_since_last_activity (normalized)
- pincode_population_estimate (if available)
```

**DBSCAN** (density-based anomaly detection)

```
Purpose: Identify isolated communities (pincodes with unique patterns)
Parameters:
- eps = 50 km (distance threshold)
- min_samples = 3 pincodes
Outliers: Single pincodes with zero enrollment in isolated areas
```

---

## Phase 3: Route Optimization

### 3.1 Mobile Unit Routing (Traveling Salesman Problem Approach)

**Objective**: Minimize distance while maximizing underserved population reached

**Algorithm: Nearest Neighbor Heuristic** (for hackathon speed)

```
1. Start at district capital or population center
2. FOR each iteration:
     a. From current location, find nearest unvisited underserved pincode
     b. Add to route
     c. Update current location
3. Return to starting point
4. REPEAT process with different starting points and pick best route
```

**Optimization Parameters**:

- Maximum pincodes per route: 10-15 (daily capacity)
- Preferred stop types: Mix of severely underserved + moderately served
- Time budget: 8 hours/day = ~500-600 km/day

**Output**:

```
Route dataframe:
- route_id (1, 2, 3, ...)
- stop_sequence (1, 2, 3, ...)
- pincode
- latitude
- longitude
- distance_from_prev_stop (km)
- cumulative_distance (km)
- estimated_population_reached
```

### 3.2 New Center Location Recommendations

**Method: Centroid Analysis**

```
FOR each cluster of underserved pincodes:
  1. Calculate weighted centroid:
     - Weight by pincode population or enrollment potential
     - lat_center = Σ(pincode_lat * population) / Σ(population)
     - lon_center = Σ(pincode_lon * population) / Σ(population)

  2. Ensure location is accessible:
     - NOT in inaccessible terrain (optional: use elevation data)
     - Near road network (optional: use road data)

  3. Calculate coverage benefit:
     - Pincodes within 25km of proposed center
     - Estimated population to gain access
```

**Priority Scoring** for new centers:

```
Priority = (Population_within_25km / State_avg_pop_per_center)
         * (1 - Current_coverage_in_region)
         * (1 / Distance_to_nearest_existing_center)
Rank and recommend top 5-10 locations
```

---

## Phase 4: Visualization & Dashboards

### 4.1 Static Maps (Output: PNG/PDF)

- **Heatmap**: Enrollment density by pincode
- **Equity Map**: Color-coded regions (red=underserved, green=well-served)
- **Route Map**: Mobile unit routes overlaid on district boundaries
- **Gap Analysis Map**: Pincodes >50km from nearest active center

### 4.2 Interactive Dashboard (Output: HTML/Streamlit)

```
Layout:
┌─────────────────────────────────────┐
│  State Selector | District Selector │
├─────────────────────────────────────┤
│                                       │
│  Interactive Folium Map              │
│  (click pincode for details)          │
│                                       │
├─────────────────────────────────────┤
│ Equity Metrics | Routes | Rec's     │
└─────────────────────────────────────┘

Features:
- Zoom to district/state level
- Click pincode → show enrollments, updates, status
- Toggle layers: equity zones, routes, proposed centers
- Download route CSVs
```

### 4.3 Visualization Libraries

- **Folium**: Interactive maps with lat/long data
- **Plotly**: 3D scatter, bar charts, comparisons
- **Streamlit**: Web dashboard for exploration
- **Matplotlib/Seaborn**: Static publication-quality charts

---

## Phase 5: Impact Assessment

### 5.1 Intervention Quantification

**For Mobile Unit Deployment**:

```
Coverage before = % of population >50km from center
Coverage after  = % of population >50km from center (new unit deployed)
Population reached = (Coverage_before - Coverage_after) * State_population

Cost per enrollment = Total_unit_cost / Expected_enrollments_per_year
ROI = (Value_of_enrollments / Total_cost) * 100%
```

**For New Center Location**:

```
Same calculations but consider permanent infrastructure costs
Break-even analysis: payback period based on enrollment targets
```

### 5.2 Prioritization Framework

```
FOR each recommendation (route or center):
  Priority_Score =
      (Population_reached / Max_pop)                    * 0.4
    + (Underserved_pincodes / Total_underserved)      * 0.3
    + (Implementation_feasibility / Max_feasibility)   * 0.2
    + (Cost_effectiveness / Max_effectiveness)        * 0.1

  Range: 0 to 1
  Rank all recommendations by priority_score
```

---

## Technical Implementation Details

### Libraries & Tools

- **geopandas**: Geospatial data manipulation
- **shapely**: Geometric operations (distance, centroid calculations)
- **folium**: Interactive mapping
- **scikit-learn**: K-means, DBSCAN clustering
- **scipy**: Optimization, distance calculations
- **pandas**: Data manipulation
- **matplotlib/seaborn**: Visualization

### Data Quality Checks

1. ✅ No duplicate pincodes in final dataset
2. ✅ Valid lat/long coordinates (bounds: India)
3. ✅ Enrollment > 0 for "active" pincodes
4. ✅ No negative distances or time values
5. ✅ Consistent date formats

---

## Success Criteria

✅ **Data Analysis**: Multi-stage geospatial analysis with 5+ equity metrics  
✅ **Originality**: Novel lifecycle + geospatial combination  
✅ **Technical Depth**: K-means, DBSCAN, TSP optimization  
✅ **Visualization**: Interactive maps + static heatmaps + dashboards  
✅ **Impact**: Actionable recommendations with ROI calculations

**Target**: 24-25/25 points ⭐⭐⭐⭐⭐
