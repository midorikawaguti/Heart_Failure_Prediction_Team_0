# Heart failure prediction model

DSI - Cohort 5 - Team 0 project

## Members:

- [Tatiana Kawaguti](https://github.com/midorikawaguti)
- [Evgenia Kveliashvili](https://github.com/ekveliasvili)
- [Aqib Khan](https://github.com/aqibkhan3)
- [Roslyn Bryan](https://github.com/RMB2025)

## Overview

This project explores the Heart Failure Prediction Dataset to predict the likelihood of heart failure based on clinical parameters. The aim is to showcase the power of data science in healthcare, enabling early interventions and reducing healthcare costs.

## Business case

Cardiovascular diseases (CVDs) remain a leading global health concern, with significant impacts on both mortality rates and economic stability.

According to the report provided by American Heart Association, CVD, listed as the underlying cause of death, accounted for 931,578 deaths in the United States in 2021. The economic burden of cardiovascular risk factors and overt cardiovascular disease is projected to increase substantially in the coming decades. Annual health care costs are projected to almost quadruple, from $393 billion to $1490 billion, and productivity losses are projected to increase by 54%, from $234 billion to $361 billion.
([Source](https://www.ahajournals.org/doi/10.1161/CIR.0000000000001258))

Early identification of individuals at risk of cardiovascular disease is crucial for reducing the financial strain on healthcare systems and improving preventive measures to manage this widespread condition. Preventive strategies should rely on screening for CVD risks in asymptomatic individuals. In this project we aim to determine factors(variables) that can predict CVD before the person with heart failure will be admitted in the hospital in life-thretening condition.

## Target audience

- **Healthcare policy makers** - to help them roll out preventive programs for early detection screenings, better allocate financial resources and implement targeted campaigns.
- **Researchers** - to understand the impact of the different features on potential risks of heart disease.

## Project Methodology and Tasks

1. **Data Understanding**
   - _Task:_ Analyze the downloaded dataset
   - _Methodology:_ examine the structure of the dataset, types of variables, and quality issues, such as missing values (e.g. Cholesterol).
2. **Exploratory Data Analysis and Visualizations**
   - _Task:_ Examine different visualizations to draw new insights
   - _Methodology:_ Perform exploratory data analysis and create visualizations to explore the relationship between the feature and the target variable (Presence or not of heart disease)
3. **Predictive Modeling**
   - _Task:_ Build a machine learning classification model to predict heart failure.
   - _Methodology:_
     - Split the data into training and test sets, and experiment with different classification models (e.g., logistic regression and KNN classification).
     - Tune the model's hyperparameters and use cross-validation.
     - Evaluate the model using metrics, such as, accuracy, precision, recall, and F1-score.
4. **Insights and Feature importance Visualizations**
   - _Task:_ Determine the features with biggest impact on predictions and visualize the insights.
   - _Methodology:_ Analyze the model's predictions with SHAP values and visualizations to interpret the feature importance, and which contribute the most for heart disease prediction.

## Dataset Overview

The dataset our team will be working on: [Heart Failure Prediction Dataset](https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction) from Kaggle.

This dataset contains combined data from 5 independent sources and has a total of 918 observations (after 272 duplicates had been deleted). There are 12 attributes in this dataset:

#### Each row represents a single person:

- **`Age`** : age of the patient [years]
- **`Sex`** : sex of the patient [M: Male, F: Female]
- **`ChestPainType`** : chest pain type [
  TA: Typical Angina, or common heart related chest pain;
  ATA: Atypical Angina, or chest discomfort that does not fit any type of pain;
  NAP: Non-Anginal Pain, pain not related to heart;
  ASY: Asymptomatic, or lack of pain but not nessesarily absence of heart issues]
- **`RestingBP`** : resting blood pressure [mm Hg]
- **`Cholesterol`** : serum cholesterol [mm/dl]
- **`FastingBS`** : fasting blood sugar [1: if FastingBS > 120 mg/dl, 0: otherwise]
- **`RestingECG`** : resting electrocardiogram results [
  Normal: Normal,
  ST: having ST-T wave abnormality (T wave inversions and/or ST elevation or depression of > 0.05 mV),
  LVH: showing probable or definite left ventricular hypertrophy by Estes' criteria]
- **`MaxHR`** : maximum heart rate achieved [Numeric value between 60 and 202]
- **`ExerciseAngina`** : exercise-induced angina, or chest pain during physical activity [Y: Yes, N: No]
- **`Oldpeak`** : oldpeak = ST [Numeric value measured in depression]
  _ST depression refers to a finding on an electrocardiogram, wherein the_ _trace in the ST segment is abnormally low below the baseline._
  ![link](/Users/evgeniakveliashvili/Desktop/DSI_projects/Heart_Failure_Prediction_Team_0/images/ST_depression_illustration.png)
- **`ST_Slope`** : the slope of the peak exercise ST segment [Up: upsloping, Flat: flat, Down: downsloping] from ECG readings
- **`HeartDisease`** : output class [1: heart disease, 0: Normal]

<figure align="center">
  <img src="images/Raw_data_Overview.png" width="85%" height="85%">
   <figcaption><strong><em>Figure 1: Raw Data Overview</em></strong></figcaption>
</figure>

### **Observations**

#### Demographic

- Age distribution seems to be normal with most people centered around 45-60 y.o
- There are more males than females in dataset, suggesting that we might need to consider stratification when building the predictive model.

#### Clinical

- Most people have either asymptomatic or non-anginal pain which leads us to think that this particular features might not be a good indicator of heart failure risks.
- Cholesterol values at 0 is unrealistic, and as it has been previously adressed as possible risks/unknowns affecting the quality and presicion of analysis.
- Fasting sugar level in most cases is 0 (means the values are below 120 mg/dL), possibly suggesting that it does not have strong correlation with heart disease diagnosis.
- Resting ESG records are predominately normal with significantly less cases of abnormal ST waves and left ventricular hypertrophy.
- Maximum Heart rate is normally distributed with some outliers.

#### Exercise Related

- Almost evenly split value counts between people who experience exercise induced angina and those who don't.
- Distrubtion of OldPeak data confirmes that about 45% of the records have normal oldpeak values and about 55% of the records significantly skewed to the right.
- ST Slope values mainly split between Up and Flat categories and as these two categories are often associated with the heart disease, therefore are of big interest.
- Dataset contains 508 records of heart disease and 410 records of absense of heart disease.

## Libraries

In order to execute the project we plan to use following libraries:

- Numpy
- pandas
- matplotlib
- sklearn
- seaborn

## Data preprocessing

**Missing Values**

- In order to understand the dataset we checked its basic structure and content.
- Before performing any preprocessing, we reviewed the dataset to check for missing values. Ensuring data completeness is crucial for building reliable models or vizualizations. After inspecting the dataset, we confirmed that there were no missing values.

**Data Consistency**

- To ensure a consistent dataset, we checked if all columns and found that the Cholesterol variable contained 0 values, which is unlikely in a clinical context. Our approach was to drop all records with cholesterol = 0 (172 records in dataset, which means 18.7% of the dataset).
- This approach was chosen instead of imputing average cholesterol because doing so create a false representation of the data, as cholesterol levels are not uniformly distributed. This was confirmed by running the models, where imputing average cholesterol resulted in a worst scenario in terms of F1-score ( F1-Score for KNN Classification - Replacing with average: 0.82 | Dropping records : 0.84)
- Additionaly, we observed that 88% of records with cholesterol =0 were associated with heart disease. Keeping these values as zero or replacing them with the average cholesterol for Cholesterol > 0 (244.6 mm/dL) could affect the relationship between cholesterol and the occurence of heart disease, leading the model to identify misleading patterns. Notably, 244.6 mm/dL is below the average cholesterol for individuals with heart disease (251.06 mm/dL).

  **Data Standardization**

- In order to work with only numerical values we converted categorical variables into numerical format using one-hot encoding or label encoder, depending on the use case.

## Risks and Unknowns

During internal discussion with the team we uncovered the following risks:

- Column "Cholesterol" contains 0 values, and while rare genetic condirtions might cause cholesterol level be very low, it's extremely unlikely to be measured at 0. That means, that we need either to impute some values instead of 0 or delete 172 records from the dataset.If we choose to delete these records, we may risk losing valuable information, potentially affecting the robustness and accuracy of our analysis. On the other hand, imputing mean values comes with its own challenges, such as introducing bias or assumptions that may not accurately reflect the true distribution of cholesterol levels.

## Exploratory Data Analysis

The exploratory data analysis allow us to understand patterns and relationship in the data. We built visualizations of individual features, and correlation between features, and evaluated statistical summaries. This helps us to determine key features to focus on.

### 1. **Statistical Summary:**

- The following visualizations provide an overview of the data, to better understand the distribution, tendencies and variability.

<figure align="center">
  <img src="images/distributions_features_over_age.png" width="70%" height="70%">
   <figcaption><strong><em>Figure 2: Features Distributions Over Age</em></strong></figcaption>
</figure><br><br><br><br>

<figure align="center">
  <img src="images/proportions_categorical_features.png" width="70%" height="70%">
   <figcaption><strong><em>Figure 3: Probability of Heart Disease for Categorical Features </em></strong></figcaption>
</figure><br><br>

### _Observations:_

#### Demographic Trends

- Older groups have more probability of heart disease. There is a 20% increase in the likelihood of heart disease when comparing individuals aged 50-59 to those in the 60-69 age group. 
- People in the 20-29 age group are less likely to have HeartDisease. In the analyzed data set, there was no record of a patient with heart disease in this age group.
- The proportion of women (22%) who develop heart disease are lower than men (56%)

#### Clinical

- Cholesterol levels are higher in individuals with heart disease aged 20-59, with similar averages across these groups. However, in the 60-79 age group, cholesterol is not a strong predictor, as those with heart disease have lower average cholesterol than those without. This suggests other factors may play a larger role in heart disease risk for older adults, such as age-related metabolic changes or the impact of cholesterol-lowering treatments.
- The average maxHR (Maximun Heart Rate) decreases across group ages. Additionally, higher MaxHR is associated with lower likelihood of heart disease risk, decreasing with age.
- Oldpeak values greater than 0.9 are common in heart disease cases, while non-disease cases tend to have values ≤ 0.8
- 74% of people who have heart disease had asymptomatic chest pain (ASY), which means that routine check-ups are important for those with other risk factors.
- Most cases with Flat and Down ST_Slope are linked to heart disease, while only 12.9% of individuals with an Up ST_Slope have heart disease.
- Elevated fasting blood sugar (FastingBS) levels increase the likelihood of developing heart disease. In the data, high FastingBS levels are associated with a 65.6% probability of heart disease, while low levels correspond to a 44.1% probability. Although there is a difference in these probabilities, the fact that they are relatively close suggests that FastingBS alone may not be a strong predictor of heart disease risk. Combining FastingBS with other factors could provide a better assessment of heart disease risk.

#### Exercise related

- Most individuals who experience angina during exercise  - 82.6% (Exercise Angina = 'Y') were diagnosed with heart disease. And vice versa, most people whithout angina during exercise are less likely to have it (25.9%).

---

#### While these initial insights reveal associations, they do not explain the relationships between features. To better understand how variables interact, we examine correlations.

### 2. **Correlation Heatmap**

The correlation heatmap allows to analyze how features correlate to each other. Darker and more intense colours represent stronger relationships (positive or negative). Neutral colours indicate weaker or no relationships.

<figure align="center">
  <img src="images/Heatmap.png" width="70%" height="70%">
   <figcaption><strong><em>Figure 4: Correlation Heatmap</em></strong></figcaption>
</figure><br><br>

### _Observations:_

**ST_Slope and Oldpeak (-0.61):**

- A moderate negative correlation of -0.61 indicates that as ST_Slope decreases, Oldpeak tends to increase.
- In medical terms, ST_Slope describes the slope of the ST segment in an ECG, and Oldpeak refers to ST depress relative to rest, often linked to heart stress or ischemia.
- This negative correlation suggests that patients with more severe ST depression (higher Oldpeak) may also have downward or less favourable ST slopes.

**HeartDisease and ST_Slope (-0.60):**

- The negative correlation of -0.60 is stronger, showing a more pronounced inverse relationship. As ST_Slope values decrease, the likelihood of HeartDisease increases.
- In the medical field, certain ST slope patterns are considered significant indicators of heart disease. A flatter or downward slope is often linked to poorer heart function

<figure align="center">
  <img src="images/ST-segment-depression-upsloping-downsloping-horizontal.png" width="60%" height="60%">
   <figcaption><strong><em>Figure 5: Visual representation of ST slope and St depression info from ECG readings</em></strong></figcaption>
</figure><br><br>

---

#### Given the strong link between ST_Slope and Oldpeak, we further investigate their relationship through visualization.

- The following plot was constructed to investigate deeper the potential correlation between SL_Slope (representing the ST segment slope as recorded on an ECG) and Oldpeak (a numerical measurement indicating ST depression relative to rest). It provides a visual representation of the relationship between these two variables, helping to identify patterns, trends, or potential associations.

<figure align="center">
  <img src="images/ST_slope_Old_peak.png" width="60%" height="60%">
   <figcaption><strong><em>Figure 6: ST_Slope vs OldPeak</em></strong></figcaption>
</figure><br><br>

### _Observations:_

- Significant number of heart failure cases occur with ST_slope reading flat or down.
- Oldpeak values associated with heart disease are spread far from 0 values, with 0 values being more representative for healthy condition
- This finding also support the fact that mild ST depression (less than 0.5 mm) is often considered a normal variant and may occur during physical exercise or in the absence of other abnormalities.
- While significant ST depression (0.5 mm or more) can indicate myocardial ischemia (reduced blood flow to the heart muscle) and warrants further evaluation.

---

#### To quantify the features impact on model predictions, we analyze SHAP values.

### 3. **Shap Summary for Feature Importance**

To interpret the influence of each feature on the model's predictions, SHAP (SHapley Additive exPlanations) values were used to assess feature importance. SHAP values provide insights into how individual features contribute to the predicted likelihood of heart disease for each observation, offering a more interpretable breakdown of model decisions.

The SHAP values were calculated based on the results of a K-Nearest Neighbors (KNN) Classification model, with the following parameters and performance metrics:

| Model              | Params                             | Accuracy | Precision | Recall   | F1       |
| ------------------ | ---------------------------------- | -------- | --------- | -------- | -------- |
| KNN Classification | n_neighbors: 15, weights: distance | 0.855672 | 0.832539  | 0.862468 | 0.846944 |

The model was refitted using F1-score as the primary optimization metric. Since F1-score balances precision (minimizing false positives) and recall (minimizing false negatives), it is particularly great in health-related predictions, where both false alarms and missed diagnoses can have serious consequences.

<figure align="center">
  <img src="images/GlobalBarPlot.png" width="60%" height="60%">
   <figcaption><strong><em>Figure 7: Global Bar Plot - Shap Values</em></strong></figcaption>
</figure><br><br>

<figure align="center">
  <img src="images/ShapSummary.png" width="60%" height="60%">
   <figcaption><strong><em>Figure 8: Summary Shap Values</em></strong></figcaption>
</figure><br><br>

### _Observations:_

These values reinforce most of what have been observed in the previous visualizations.

- As shown in Figure 2, Oldpeak (+0.14) emerges as a crucial predictor, confirming that individuals with significant ST depression on an ECG are highly likely to have heart disease.
- Exercise Angina (+0.12) strongly contributes to positive predictions, aligning with the data in Figure 3, where 82.6% of individuals who experienced Exercise Angina were diagnosed with heart disease.
- Flat or Down ST slopes significantly increase the likelihood of heart disease, consistent with observations in Figures 3 and 6.
- MaxHR (+0.06) suggests that lower peak heart rates during stress tests are associated with heart disease.
- Age (+0.04) has a moderate effect.It can be better observed in Figure 2, where the percentages shows that older individuals tend to develop more cardiovascular issues.

### 4. Conclusion

In conclusion, the exploratory data analysis revealed several critical insights into cardiovascular health indicators. The correlation heatmap highlighted significant relationships, such as the negative correlation between ST_Slope and HeartDisease (-0.56). Our findings show the importance of ST segment patterns and ST depression (Oldpeak) as potential predictors of heart disease, particularly in identifying more severe cases. The scatterplot and visualizations further emphasized the link between ST slope readings and heart disease, as well as the distribution of Oldpeak values, which tend to deviate from zero in individuals with heart disease.

Statistical summaries revealed demographic trends, such as an average age of 55.90 for individuals with heart disease and a pronounced gender disparity, with males comprising 90.16% of cases. Additionally, other variables like cholesterol, MaxHR, and Oldpeak showed distinct differences between individuals with and without heart disease.

This project demonstrates the application of data science in healthcare. By combining exploratory analysis, predictive modeling, and visual storytelling, we can derive meaningful insights and inform early interventions for heart failure.
