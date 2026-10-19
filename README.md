# STUDENT STRESS FACTORS ANALYSIS

## Introduction
This is a group project, aim to examine student stress using publicly available dataset from Kaggle to develop data-driven insights that may inform stress-management initiatives at the U of I.
Details of result is presented in the Final Report, attached in this repository. 

## Data Overview 
Our dataset is sourced from the comprehensive [Student Stress Monitoring Datasets from Kaggle](https://www.kaggle.com/datasets/mdsultanulislamovi/student-stress-monitoring-datasets/data).
It contains 1,100 observations, 21 features, aiming to predict the dependent variable, “stress_level”.
The predictors are structured across five scientifically identified domains: Psychological,
Physiological, Environmental, Academic, and Social, which primarily consist of quantitative ratings.

## Experiment Pipeline

 * EDA
 * Feature selection : based on Features Distribution, Feature Importance Ranking (ANOVA) and P-value analysis
 * Model Selection, Training and Testing: K-Fold Cross Validation, Logistic Regression and Random Forest
 * Predictive Analysis and Comparision: Compare predictive accuracy between models, and between using all factors and selected factors
 * Clustering with Selected Factors: Using Elbow method, resulted in 3 clusters

## Results and Insights 

### RQ1: What proportion of students experience no stress at all, some stress, and high stress?

Our EDA result indicates that roughly two-thirds of respondents report at least moderate stress, and
about one-third fall into the high-stress category. The balanced class distribution is beneficial for later
classification models because it reduces the risk that algorithms will be biased toward a majority class
and allows performance metrics to reflect model quality rather than class imbalance.

<img width="800" height="350" alt="image" src="https://github.com/user-attachments/assets/d6cd13ab-5df2-4bf2-930c-4242953cb4dd" />


### RQ2: How are different parts of student life—like sleep, workload, or social life—linked to stress levels?

From section 3.2, the ANOVA results highlighted a hierarchy of feature importance based on their
ability to separate stress categories, with the top 10 F-statistics including 30% psychological factors,
30% academic factors, 20% physiological factors, and 20% social factors. Moreover, since our
p-values are extremely small, it proves that every single aspect of student life we measured shows a
statistically significant change as stress increases. This indicates that different parts of student life are
linked to stress universally and significantly.

<img width="800" height="450" alt="image" src="https://github.com/user-attachments/assets/c6ef5ba2-8314-494a-92c8-4b6e20855f49" />


### RQ3: Can we predict the student stress level from the given factors?
According to section 3.3, the results indicate that the LR and RF models could predict the student
stress level with high accuracy (88,18% and 87,73%) respectively. Moreover, when we examine F1
score, it shows balance across classes with a solid score around 0.87-0.89, indicating that the model
achieves a strong balance between precision and sensitivity. This demonstrates that the classifier is
robust and effective at distinguishing between stress levels.

<img width="267" height="403" alt="image" src="https://github.com/user-attachments/assets/5d7ee005-c87f-4d1c-b049-6230c7c6db00" />
<img width="278" height="401" alt="image" src="https://github.com/user-attachments/assets/f1eb5832-3a23-44db-8de6-a08636a79554" />


### RQ4: What types of student profiles can be identified based on their lifestyle factors and stress levels?
According to section 3.5, three student profiles can be concluded from the table:
(1) Balanced lifestyle students: Moderate scores across lifestyle measures and moderate stress
levels
(2) Low-stress students: High sleep quality, perfect living conditions (low noise, well-met basic
needs), and the lowest stress level)
(3) Overloaded students: Poor sleep, inadequate living conditions (suffered from noise, limited
basic needs,) and the highest stress level)

<img width="435" height="247" alt="Screenshot 2026-10-19 at 10 36 07" src="https://github.com/user-attachments/assets/6d260da4-646c-4aeb-bf7b-5487cf6604e3" />
<img width="630" height="115" alt="Screenshot 2026-10-19 at 10 36 19" src="https://github.com/user-attachments/assets/1caf15af-ed9b-4571-b7cc-43db5cce5705" />

### RQ5: If we only look at the most important causes of stress, does it make our predictions more accurate?
As shown in the figures, LR’s accuracy is improved after selecting only the top 10 features from the
ANOVA test while the RF model experiences a decrease in accuracy. 

<img width="554" height="395" alt="Screenshot 2026-10-19 at 10 46 39" src="https://github.com/user-attachments/assets/194a1150-0a46-4ccf-a5be-ae8de2ecb5e8" />

After excluding even more features with the LR & RF feature importance, the accuracy of both models improved, even though,
as for LR, it also exhibits lower recall for classes 0 and 2, and as for the RF model, it further improved
the recall for all classes 0, 1 and 2.

<img width="350" height="404" alt="Screenshot 2026-10-19 at 10 53 42" src="https://github.com/user-attachments/assets/38f7e249-e501-4986-8d21-c4d544a58cae" />
<img width="294" height="404" alt="Screenshot 2026-10-19 at 10 53 33" src="https://github.com/user-attachments/assets/ff9860e4-88b2-45ad-853c-57345f58350a" />

