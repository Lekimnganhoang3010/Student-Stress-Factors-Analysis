# 🎓 Student Stress Factors Analysis

**Which parts of student life drive stress, and can we predict who is at risk?**
A group data analysis project using survey data to give the University of Illinois evidence for where stress-management programs would have the most impact.

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![R](https://img.shields.io/badge/R-276DC3?style=flat&logo=r&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?style=flat&logo=pandas&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikitlearn&logoColor=white)

📄 Full methodology and results: see the **Final Report** in this repository.

---

## 📌 Key Findings at a Glance

| | Finding |
|---|---|
| 📊 **Prevalence** | ~2 in 3 students report at least moderate stress; ~1 in 3 report high stress |
| 🔍 **Drivers** | All 21 measured factors differ significantly across stress levels (p < 0.001). Psychological and academic factors make up 60% of the top 10 predictors |
| 🤖 **Prediction** | Logistic Regression **88.18%** and Random Forest **87.73%** accuracy, F1 **0.87–0.89** across all classes |
| 👥 **Segments** | 3 distinct student profiles: *Low-stress*, *Balanced*, and *Overloaded* |
| ✂️ **Feature selection** | A smaller, targeted feature set kept or improved accuracy, so stress can be screened with fewer survey questions |

---

## ❓ Business Questions

1. **Prevalence:** What share of students experience no, moderate, or high stress?
2. **Drivers:** How are sleep, workload, social life, and other factors linked to stress?
3. **Prediction:** Can we reliably predict a student's stress level from these factors?
4. **Segmentation:** What student profiles emerge from lifestyle factors and stress?
5. **Efficiency:** Does focusing on the most important factors improve predictions?

---

## 🗂️ Data

| Attribute | Detail |
|---|---|
| **Source** | [Student Stress Monitoring Datasets (Kaggle)](https://www.kaggle.com/datasets/mdsultanulislamovi/student-stress-monitoring-datasets/data) |
| **Size** | 1,100 students × 21 features |
| **Target** | `stress_level` (0 = none, 1 = moderate, 2 = high) |
| **Feature domains** | Psychological · Physiological · Environmental · Academic · Social |
| **Type** | Mostly quantitative survey ratings |

---

## 🔬 Analysis Workflow

```
Exploratory Data Analysis  →  Feature Selection  →  Modeling & Validation  →  Model Comparison  →  Segmentation
   distributions,              ANOVA F-test,         Logistic Regression,      all vs. selected     K-Means clustering,
   class balance               p-values,             Random Forest,            features             Elbow method → k = 3
                               feature importance    K-Fold cross-validation
```

---

## 📈 Results

### 1. Prevalence: two-thirds of students are under at least moderate stress

Roughly two-thirds of respondents report at least moderate stress, and about one-third fall into the high-stress group. The three classes are close to balanced, so the models are not biased toward one majority class and accuracy reflects real model quality.

<img width="800" height="350" alt="Distribution of student stress levels" src="https://github.com/user-attachments/assets/d6cd13ab-5df2-4bf2-930c-4242953cb4dd" />

### 2. Drivers: every part of student life is linked to stress

An ANOVA F-test ranked each factor by how well it separates the stress levels. The top 10 factors break down as:

| Domain | Share of top 10 |
|---|---|
| Psychological | 30% |
| Academic | 30% |
| Physiological | 20% |
| Social | 20% |

Every factor showed a statistically significant difference across stress levels (very small p-values). In other words, stress is not driven by a single cause: it is tied to students' whole lives.

<img width="800" height="450" alt="ANOVA feature importance ranking" src="https://github.com/user-attachments/assets/c6ef5ba2-8314-494a-92c8-4b6e20855f49" />

### 3. Prediction: stress level can be predicted with ~88% accuracy

| Model | Accuracy | F1 score (per class) |
|---|---|---|
| Logistic Regression | **88.18%** | 0.87–0.89 |
| Random Forest | **87.73%** | 0.87–0.89 |

F1 scores are consistent across all three classes, so the models balance precision and recall well and do not just get the easy cases right.

<img width="267" height="403" alt="Logistic Regression classification report" src="https://github.com/user-attachments/assets/5d7ee005-c87f-4d1c-b049-6230c7c6db00" />
<img width="278" height="401" alt="Random Forest classification report" src="https://github.com/user-attachments/assets/f1eb5832-3a23-44db-8de6-a08636a79554" />

### 4. Segmentation: three distinct student profiles

K-Means clustering on the selected factors (k = 3, chosen with the Elbow method) found:

| Segment | Profile | Stress |
|---|---|---|
| 🟢 **Low-stress** | High sleep quality, good living conditions (low noise, basic needs well met) | Lowest |
| 🟡 **Balanced** | Moderate scores across lifestyle measures | Moderate |
| 🔴 **Overloaded** | Poor sleep, noisy living conditions, basic needs not well met | Highest |

<img width="435" height="247" alt="Cluster profiles" src="https://github.com/user-attachments/assets/6d260da4-646c-4aeb-bf7b-5487cf6604e3" />
<img width="630" height="115" alt="Cluster summary table" src="https://github.com/user-attachments/assets/1caf15af-ed9b-4571-b7cc-43db5cce5705" />

### 5. Feature selection: fewer, better factors

| Step | Logistic Regression | Random Forest |
|---|---|---|
| Top 10 ANOVA features | ⬆️ Accuracy improved | ⬇️ Accuracy decreased |
| Further reduced using model feature importance | ⬆️ Accuracy improved, but lower recall for classes 0 and 2 | ⬆️ Accuracy improved, with higher recall for all 3 classes |

<img width="554" height="395" alt="Accuracy with top 10 ANOVA features" src="https://github.com/user-attachments/assets/194a1150-0a46-4ccf-a5be-ae8de2ecb5e8" />

<img width="350" height="404" alt="Logistic Regression with reduced features" src="https://github.com/user-attachments/assets/38f7e249-e501-4986-8d21-c4d544a58cae" />
<img width="294" height="404" alt="Random Forest with reduced features" src="https://github.com/user-attachments/assets/ff9860e4-88b2-45ad-853c-57345f58350a" />

**Takeaway:** a reduced Random Forest model is the best choice for screening. It needs fewer survey questions and catches more students in every stress group.

---

## 💡 Recommendations for the University

1. **Target the "Overloaded" segment first:** prioritize sleep support and housing conditions (noise, basic needs), since these separate the highest-stress group most clearly.
2. **Use a short screening survey:** the reduced feature set predicts stress accurately, so a brief check-in survey could flag at-risk students early.
3. **Treat stress as a whole-life issue:** psychological and academic factors lead, but physiological and social factors matter too, so support programs should work across departments.

---

## ⚠️ Limitations

- The data is a public Kaggle dataset, not a sample of U of I students, so results should be confirmed with local data.
- Survey ratings are self-reported and may carry response bias.
- The data is cross-sectional, so it shows association, not cause.

## 🛠️ Tools

Python (pandas, NumPy, scikit-learn, Matplotlib, Seaborn) · R · ANOVA · Logistic Regression · Random Forest · K-Means · K-Fold Cross-Validation
