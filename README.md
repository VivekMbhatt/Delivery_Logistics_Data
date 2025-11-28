# Delivery_Logistics_Data
This project builds a Machine Learning model to predict actual delivery time (in hours) for logistics shipments using historical delivery, operational, and weather data.
# Dataset Description
The dataset contains delivery-level records with the following categories:
1. Shipment Attributes
   distance_km
   package_weight_kg
   package_type
   Operational Attributes
   delivery_partner
   vehicle_type
   delivery_mode
   region
   delivery_status

2. Environmental Attributes
   weather_condition
   bad_weather_flag
   Performance Attributes
   expected_time_hours
   delivery_time_hours
   delivery_cost
   delivery_rating

3. Target Variable
   actual_hours

# Data Preprocessing & Feature Engineering
Key Cleaning Steps
   Converted delivery time timestamps to numeric hours
   Removed invalid / missing time entries
   Replaced infinities from division
   Filled numeric NaNs using medians
   Filled categorical NaNs with “Unknown”
   Ensured final data contained 0 missing values

Engineered Features
Feature	Description
   speed_kmph	distance / actual_hours
   delay_hours	actual_hours – expected_hours
   cost_per_km	delivery_cost / distance
   heavy_package_flag	1 if weight > 20 kg
   bad_weather_flag	rainy / foggy / stormy
   region_partner	region + delivery_partner

These features significantly improved model performance and interpretability.

# Modeling Approach

The following ML models were trained and compared:
1. Linear Regression
   Extremely accurate due to synthetic nature of data

2. Random Forest Regressor
   Non-linear
   Strong generalization
   Clear feature importance

3. XGBoost Regressor
   High performance
   Effective for structured data

A preprocessing pipeline (StandardScaler + OneHotEncoder) was used for all models.

# Model Performance
Model	MAE (hrs)	RMSE (hrs)	R² Score
  (a). Linear Regression	0.0000278	0.0000343	0.99999999988
  (b).Random Forest	0.0254	0.0850	0.9992539
  (c).XGBoost	0.0795	0.1201	0.9985108

# Final Model: Random Forest
  Although Linear Regression achieved near-perfect scores, this is due to the highly structured (synthetic) nature of the dataset.
  Random Forest was chosen as the final model for deployment because:
  It generalizes better
    More robust to real-world noise
    Provides clearer, actionable feature importance

# Feature Importance & Insights
  Top Predictors of Delivery Time
    distance_km (strongest influence)
    speed_kmph
    bad_weather_flag
    weather_condition_foggy
    delay_hours

# Key Insights
  Distance and speed dominate ETA predictions
  Fog and rain significantly slow down deliveries
  Only 3–5 features explain ~97–99% of variance (per cumulative plot)

# Visualizations
  Top 20 feature importance (bar plot)
  Cumulative importance curve (shows dominance of top few features)

# Business Impact & Recommendations
  Improve ETA Accuracy
  Use model predictions for real-time customer updates.
  Weather-Based Adjustments
  Increase ETA buffers for rainy/foggy regions.
  Long-Distance Optimization
  Prioritize faster vehicles
  Allocate reliable partners
  Adjust delivery windows
  Real-Time Speed Monitoring
  If driver speed < predicted → trigger ETA recalculation.
  Lightweight Deployment


🧭 9. Technologies Used

Python
Pandas
NumPy
Scikit-learn
XGBoost
Matplotlib
Seaborn
