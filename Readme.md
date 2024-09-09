🚀🌌 Predicting Hazardous NEOs (Nearest Earth Objects) – A NASA Data Challenge 🌌🚀

![back](readmebackimage.jpg)

📌 Project Overview:

The Predicting Hazardous NEOs (Nearest Earth Objects) project addresses a crucial challenge in space science and planetary defense. Utilizing a comprehensive dataset from NASA, covering observations of NEOs from 1910 to 2024, this project focuses on predicting whether these celestial objects pose a potential threat to Earth.

*****************************************

📊 Dataset Description:

![cleaning](datacleaning_background.jpg)

Shape: The dataset has a shape of (338,199, 9), meaning it contains 338,199 records and 9 features.

Data Types:

bool(1): Boolean feature indicating if an object is hazardous (is_hazardous).

float64(5): Floating-point features for numerical values.

int64(1): Integer feature for object IDs.
object(2): Categorical features.

Columns:

* neo_id (int64): Unique identifier for each NEO 🌟.

* name (object): Name of the NEO ✨. Note that many names may be duplicates.

* absolute_magnitude (float64): Measure of the NEO's brightness, adjusted to a standard distance 🌟.

* estimated_diameter_min (float64): Minimum estimated diameter of the NEO in meters 📏.

* estimated_diameter_max (float64): Maximum estimated diameter of the NEO in meters 📏.

* orbiting_body (object): Body around which the NEO orbits 🌍 (e.g., Earth). 
All rows reference Earth in this dataset.
relative_velocity (float64): Speed of the NEO relative to Earth, measured in km/s 🚀.

* miss_distance (float64): Closest distance between the NEO and Earth, measured in kilometers 🌌.

* is_hazardous (bool): Boolean flag indicating whether the NEO is classified as hazardous to Earth ⚠️.

*****************************************

🔍 Data Cleaning Insights:

* Duplicate Values: Many features had duplicate entries. These duplicates were removed to ensure the dataset’s accuracy and uniqueness.

* Uniformity: The orbiting_body feature was uniform across all entries, reflecting Earth as the sole orbiting body in this dataset.

* Null Values: The dataset had 28 rows with null values. Given their small quantity, these rows were removed to maintain dataset integrity without significant data loss.

* Outliers: Outliers were minimal in this dataset, so they were removed to ensure high-quality data for modeling.

***************************************

📊 Exploratory Data Analysis (EDA) 🔍

![eda](edaback.png)

In this section, we explore the dataset to understand its characteristics, identify patterns, and uncover insights that will guide our data preprocessing and model development.

1. Class Distribution Analysis 📈

To understand the distribution of our target variable is_hazardous, we created a donut chart showing the percentage of hazardous vs. non-hazardous NEOs. The chart reveals that:

* 90% of the NEOs are classified as non-hazardous.

* 10% of the NEOs are classified as hazardous.

--> This indicates a significant class imbalance that needs to be addressed in our modeling approach.

Donut Chart:

2. Name Feature Analysis 🗣️

We analyzed the name feature, which represents the name of each NEO. A word cloud visualization shows the frequency of NEO names, and a bar plot reveals the top and least frequent names:

* The most frequent name is '277810 (2006 FV35)' with 211 occurrences.

* The least frequent name is '(2021 TR10)' with 1 occurrence.

However, there are more than 10 names with only 1 occurrence. A donut chart displays their percentage:

--> Number of names with a single occurrence: 9252
Percentage of names with a single occurrence: 3.13%

Word Cloud and Bar Plot:

3. Numeric Features Analysis 📏
a. Absolute Magnitude 🌟
The absolute_magnitude feature shows how bright an NEO appears from a standard distance. We created a bar plot to illustrate its distribution:

* Most frequent range: (20.639, 21.858] with 51104 occurrences.

* Least frequent range: (30.391, 31.61] with 705 occurrences.

A separate plot shows the distribution of hazardous vs. non-hazardous NEOs within these ranges.

Bar Plot of Absolute Magnitude:

b. Estimated Diameter Min 📏

The estimated_diameter_min feature represents the minimum estimated diameter of the NEO. Distribution analysis shows:

* Most frequent range: (0.00092, 0.0359] with 112448 occurrences.

* Least frequent range: (0.313, 0.347] with 5815 occurrences.

A similar plot clarifies the distribution of hazardous vs. non-hazardous NEOs.

Bar Plot of Estimated Diameter Min:

c. Estimated Diameter Max 📏

The estimated_diameter_max feature represents the maximum estimated diameter of the NEO. Distribution analysis shows:

* Most frequent range: (0.00206, 0.0802] with 112448 occurrences.

* Least frequent range: (0.699, 0.776] with 5815 occurrences.
Bar Plot of Estimated Diameter Max:

d. Relative Velocity 🚀

The relative_velocity feature measures how fast the NEO is moving relative to Earth:

* Most frequent range: (23231.078, 34744.944] with 56824 occurrences.

* Least frequent range: (103828.139, 115342.005] with 4313 occurrences.
Bar Plot of Relative Velocity:


e. Miss Distance 🌌

The miss_distance feature represents the closest approach distance of the NEO to Earth:

* Most frequent range: (59839847.134, 67318984.834] with 34000 occurrences.

* Least frequent range: (-68045.844, 7485883.233] with 22117 occurrences.

*********************************

Preparing for Modeling 🧠:

![ml](mll.jpg)

Feature Selection:

Removed features: orbiting_body (same for all), neo_id, and name (could mislead models).

Data Scaling & Splitting:

Three versions of the dataset were prepared:

* Original Data (with standard scaling and splitting).

* SMOTE Method (for handling class imbalance).

* Random Undersampling.

Model Trials:

**_Decision Trees:_** 

Tried with Grid Search tuning:

One with original data using class weight adjustment.

One with SMOTE and one with undersampling.

Results showed weak AUC scores and overfitting in learning curves.

**_Logistic Regression:_**

-->Showed less overfitting but weaker accuracy and AUC scores.

**_XGBoost:_**

Tried with default parameters and then tuned with Optuna.
Higher scores but learning curve showed slight overfitting.

**_Random Forest:_**

Achieved good accuracy with slight overfitting.
Tuned with Optuna and class weight adjustment, yielding the best performance.

**_KNN:_**

Showed good accuracy but higher overfitting.

Final Model Selection: 🌟

The Random Forest model, tuned with Optuna and class weight adjustment for handling class imbalance, emerged as the final choice due to its balance of accuracy and manageable overfitting.

a learning score of 93, a testing score of 91, an AUC of 94, an F1 score of 95 for class 0, and 47 for class 1, along with a suitable learning curve. 🌟📈