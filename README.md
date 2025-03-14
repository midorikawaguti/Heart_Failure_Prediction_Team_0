# Heart failure prediction model
DSI - Cohort 5 - Team 0 project
## Members:
 + Tatiana Uemura
 + Evgenia Kveliashvili
 + Aqib Khan
 + Roslyn Bryan


## Business case

Cardiovascular diseases (CVDs) remain a leading global health concern, with significant impacts on both mortality rates and economic stability.
According to the report provided by American Heart Association, CVD, listed as the underlying cause of death, accounted for 931,578 deaths in the United States in 2021. The economic burden of cardiovascular risk factors and overt cardiovascular disease is projected to increase substantially in the coming decades. Annual health care costs are projected to almost quadruple, from $393 billion to $1490 billion, and productivity losses are
projected to increase by 54%, from $234 billion to $361 billion.(https://www.ahajournals.org/doi/10.1161/CIR.0000000000001258)
Early detection of the people under cardiovascular risk can help to mitigate the financial burden on the healthcare system and improve preventive measures to manage this widespread condition. Preventive strategies should rely on screening for CVD risks in asymptomatic individuals. In this project we aim in determining factors(variables) that can predict CVD before the person with heart failure will be admitted in the hospital in life-thretening condition

## Objective
Conduct exploratory data analyses, create visualization and build predictive model of demographic, clinical, and exercise-related features that are the most significant predictors of heart disease.

## Target audience
 + Healthcare policy makers  - to help them roll out preventive programs for early detection screenings, better allocate financial resources and implement targeted campaigns
 

## Project task
 + Analyze the downloaded dataset
 + Examine different visualizations to draw new insights
 + Build Machine Learning classification model to predict heart failure based on clinical, demographic and exersize-related features

## Dataset review
The dataset our team will be working on:
https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction

This dataset contains combined data from 5 independent sources and has a total of 918 observations (after 272 duplicates had been deleted). There are 12 attributes in this dataset:
 #### Each row represents a single people:
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

 + Reviewed dataset to make sure that missing values are addressed properly, if any
 + 
 + 

   
## Exploratory data analysis

 + Build scatterplot to examine possible correlations between SL_Slope (reading on ECG of ST segment) and Oldpeak (numeric measurements of the ST slope on ECG)
 + 
 + 

