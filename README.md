# Heart failure prediction model
DSI - Cohort 5 - Team 0 project
## Members:
 + Tatiana Uemura
 + Evgenia Kveliashvili
 + Aqib Khan
 + Roslyn Bryan

## Overview

This project explores the Heart Failure Prediction Dataset to predict the likelihood of heart failure based on clinical parameters. The aim is to showcase the power of data science in healthcare, enabling early interventions and reducing healthcare costs.

## Business case

Cardiovascular diseases (CVDs) remain a leading global health concern, with significant impacts on both mortality rates and economic stability.
According to the report provided by American Heart Association, CVD, listed as the underlying cause of death, accounted for 931,578 deaths in the United States in 2021. The economic burden of cardiovascular risk factors and overt cardiovascular disease is projected to increase substantially in the coming decades. Annual health care costs are projected to almost quadruple, from $393 billion to $1490 billion, and productivity losses are
projected to increase by 54%, from $234 billion to $361 billion.(https://www.ahajournals.org/doi/10.1161/CIR.0000000000001258)
Early detection of the people under cardiovascular risk can help to mitigate the financial burden on the healthcare system and improve preventive measures to manage this widespread condition. Preventive strategies should rely on screening for CVD risks in asymptomatic individuals. In this project we aim in determining factors(variables) that can predict CVD before the person with heart failure will be admitted in the hospital in life-thretening condition.

## Objective
Conduct exploratory data analyses, create visualization and build predictive model of demographic, clinical, and exercise-related features that are the most significant predictors of heart disease.

## Target audience
 + Healthcare policy makers  - to help them roll out preventive programs for early detection screenings, better allocate financial resources and implement targeted campaigns
 
## Methodology
1. Data Understanding
2. Exploratory Data Analysis
3. Predictive Modeling
4. Insights and Visualizations

## Project task
 + Analyze the downloaded dataset
 + Examine different visualizations to draw new insights
 + Build Machine Learning classification model to predict heart failure based on clinical, demographic and exersize-related features and determine what features have bigger impact on prediction

## Dataset review
The dataset our team will be working on:
https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction

This dataset contains combined data from 5 independent sources and has a total of 918 observations (after 272 duplicates had been deleted). There are 12 attributes in this dataset:
 #### Each row represents a single person:
- **`Age`** : age of the patient [years]
- **`Sex`** : sex of the patient [M: Male, F: Female]
- **`ChestPainType`** : chest pain type [TA: Typical Angina, ATA: Atypical Angina, NAP: Non-Anginal Pain, ASY: Asymptomatic]
- **`RestingBP`** : resting blood pressure [mm Hg]
- **`Cholesterol`** : serum cholesterol [mm/dl]
- **`FastingBS`** : fasting blood sugar [1: if FastingBS > 120 mg/dl, 0: otherwise]
- **`RestingECG`** : resting electrocardiogram results [Normal: Normal, ST: having ST-T wave abnormality (T wave inversions and/or ST elevation or depression of > 0.05 mV), LVH: showing probable or definite left ventricular hypertrophy by Estes' criteria]
- **`MaxHR`** : maximum heart rate achieved [Numeric value between 60 and 202]
- **`ExerciseAngina`** : exercise-induced angina [Y: Yes, N: No]
- **`Oldpeak`** : oldpeak = ST [Numeric value measured in depression]
- **`ST_Slope`** : the slope of the peak exercise ST segment [Up: upsloping, Flat: flat, Down: downsloping]
- **`HeartDisease`** : output class [1: heart disease, 0: Normal]

In order to execute the project we plan to use following libraries:
 + Numpy
 + pandas
 + matplotlib
 + sklearn
 + seaborn

## Data preprocessing

 + In order to understand the dataset we checked it's basic structure and content.
 + Before performing any preprocessing, we reviewed the dataset to check for missing values. Ensuring data completeness is crucial for building reliable models or vizualizations. After inspecting the dataset, we confirmed that there are no missing values.
 + To ensure a consistent dataset, we checked if any columns have 0 values and if it does, whether 0 values are possible records. Only one column contained 0 values with we considered as wrong data. We replaced all occurrences of 0 (there are 172 records in dataset) in numerical column Cholesterol with the mean of that column.
 + In order to work with only numerical values we converted categorical variables into numerical format using one-hot encoding or label encoder, depending on the use case.


   
## Exploratory data analysis
 + Created correlation heatmap to analyze how features correlate to  each other. Darker and more intense colours represent stronger relationships(positive or negative). Neutral colours indicate weaker or no relationships.

![alt text](images/correlation-heatmap.png)

*Observations from the above visualization:*
*1. ST_Slope and Oldpeak (-0.50):*
*A moderate negative correlation of -0.50 indicates that as ST_Slope decreases, Oldpeak tends to increase.*
*In medical terms, ST_Slope describes the slope of the ST segment in an ECG, and Oldpeak refers to ST depress relative to rest, often linked to heart stress or ischemia.* 
*This negative correlation suggests that patients with more severe ST depression (higher Oldpeak) may also have downward or less favourable ST slopes.*
*2. HeartDisease and ST_Slope (-0.56):*
*The negative correlation of -0.56 is stronger, showing a more pronounced inverse relationship. As ST_Slope values decrease, the likelihood of HeartDisease increases.*
*In the medical field, certain ST slope patterns are considered significant indicators of heart disease. A flatter or downward slope is often linked to poorer heart function*

 + A scatterplot was constructed to investigate deeper the potential correlation between SL_Slope (representing the ST segment slope as recorded on an ECG) and Oldpeak (a numerical measurement indicating ST depression relative to rest). The scatterplot provides a visual representation of the relationship between these two variables, helping to identify patterns, trends, or potential linear associations.

![alt text](images/St-slope-Oldpeak-correlation.png)

### The visual representation of ST slope and St depression info from ECG readings
![alt text](images/ST-segment-depression-upsloping-downsloping-horizontal.png)

*We can see that significant number of heart failure cases occur with ST_slope reading flat or down, also oldpeak values associated with heart disease are spread far from 0 values, with 0 values being more representative for healthy condition*
*This finding also support the fact that mild ST depression (less than 0.5 mm) is often considered a normal variant and may occur during physical exercise or in the absence of other abnormalities.* 
*While significant ST depression (0.5 mm or more) can indicate myocardial ischemia (reduced blood flow to the heart muscle) and warrants further evaluation.*

 + Created statistical summaries:
Average Age (Heart Disease): 55.90 | Male: 55.87 | Female: 56.18  
Males with Heart Disease: 90.16% | Females: 9.84%  
RestingBP: 134.19, Cholesterol: 175.94, FastingBS: 0.33, MaxHR: 127.66  
Total Average: 109.53  
RestingBP Contribution: 122.51%  
Cholesterol Contribution: 160.63%  
FastingBS Contribution: 0.31%  
MaxHR Contribution: 116.55%  
The percentage of males with Heart Disease is: 90.16%  
The percentage of females with Heart Disease is: 9.84%  

![alt text](images/distribution-features-over-age.png)

*Some observations from the above visualization:*

*1.People in the 20-29 age group are less likely to have HeartDisease.*
*2.Cholesterol levels are higher in individuals with No HeartDisease compared to those with HeartDisease.*
*3.People without HeartDisease have higher MaxHR compared to those with HeartDisease.*
*4.Oldpeak values for people with HeartDisease are >0.9 in all population, whereas those without are <=0.8*

## Insights and visualizations

 + Early detection protocols focusing on high-risk individuals could sighnificantly improve patient outcomes.
 +

## Conclusion

This project demonstrates the application of data science in healthcare. By combining exploratory analysis, predictive modeling, and visual storytelling, we can derive meaningful insights and inform early interventions for heart failure.
