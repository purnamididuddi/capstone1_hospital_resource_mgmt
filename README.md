# Capstone1: Hospital Resource Management
Capstone-1 submission: A predictive analysis for Resource Management in hospitals

Link to Jupyter notebook with analysis:
https://github.com/purnamididuddi/capstone1_hospital_resource_mgmt/blob/main/healthcare_analysis.ipynb


Problem Description:
Resource management is very critical in any business/vertical. Often times, businesses lose money due to un-informed resource allocation. It is even more important in hospitals as it impacts how many patients the hospital can serve and thus the health/life of patients.
In this project, I have chosen the below dataset from Kaggle:
https://www.kaggle.com/datasets/nehaprabhavalkar/av-healthcare-analytics-ii

The goal is to help hospital management to predict the length-of-stay of a patient. This knowledge will help the management streamline necessary resources and better manage their overall resources

Excerpts of the analysis from the Jupyter notebook:
##### Many models were built in an effort to give best results to our customer (i.e., hospital management). Below is a summary of each of their performance

| <span style='background:orange'>Model # | <span style='background:orange'>Model Description | <span style='background:orange'>Parameters | <span style='background:orange'># of Dimensions | <span style='background:orange'>Train/Dev/Test Accuracies | <span style='background:orange'>F1 Score on Testset |
| :-: | :-: | :-: | :-: | :-: | :-: |
|<span style='background:yellow'> Model 0 | Random guessing | For a baseline | --- | 9.09 | --- |
|<span style='background:yellow'> Model 1 | Logistic Regr | Initial logistic regr model | --- | 38.91/38.85/38.65 | 38.65 |
|<span style='background:yellow'> Model 2 | Basic Logistic Regr with OneHot on all categ | Baseline | 130 | 38.97/38.89/38.87 | 38.87 |
|<span style='background:yellow'> Model 3 | GridSearch Logistic Regr hyper params | {'lgr__C': 0.18957356524063793, 'lgr__max_iter... | 130 | 40.13/40.14/40.13 | 40.13 |
|<span style='background:yellow'> Model 4 | GridSearch kNN hyper params | {'knn__n_neighbors': 50} | 130 | 41.89/39.04/39.24 | 39.24 |
|<span style='background:yellow'> Model 5 | Decision Tree 1 | Moderate depth of 10 | 130 | 42.14/41.22/41.22 | 41.22 |
|<span style='background:yellow'> Model 6 | Decision Tree 2 | Deeper tree (max-depth=100) | 130 | 99.96/30.07/30.04 | 30.04 |
|<span style='background:yellow'> Model 7 | Gridsearch on Decision tree | {'dt__max_depth': 10, 'dt__min_impurity_decrea... | 130 | 39.58/40.04/39.98 | 39.98 |
|<span style='background:yellow'> Model 8 | Gridsearch on Feature extraction alpha | {'selector__estimator__alpha': 0.01} | 30 | 41.7/40.65/40.42 | 40.42 |
|<span style='background:yellow'> Model 9 | Adaboost to compensate for high bias | {'boost__n_estimators': 25} | 30 | 36.96/37.32/37.38 | 37.38 |
|<span style='background:yellow'> Model 10 | Gradientboost to compensate for high bias | {'gboost__n_estimators': 200} | 30 | 41.58/41.3/41.19 | 41.19 |
|<span style='background:yellow'> Model 11 | RandomForests with deep trees to compensate for high variance | {'max_depth': 100} | 30 | 99.81/33.98/33.79 | 33.79 |

### Summary of the findings:
#### From the Data Understanding stage:
1. The Admission_deposit has a very nice normal distribution curve. No fine tuning needed for this column

2. A given patientid has multiple entries. This could be because the patient got admitted more than once. However, the case_ids of a patient are consecutive; this looks a bit weird and hinting that only for one admission, multiple entries got added (due to clerical error or different departments, etc). This might skew the results.

3. Very high percentage of patients were admitted into Gynaecology department. 

4. Another observation is that "anesthesia" is a department by itself. A patient wouldn't get admitted just for getting anesthesia. I strongly believe these patients were actually admitted in regular departments who happened to need anesthesia for the treatment. Need to see if this 'superficial' department will impact the predictions. Let's keep this in mind for any fine-tuning the results

5. Bulk of the Stays are between 11 days to 40days. 
     a. Of these Stays, there are more 'Moderate' Severity-of-illness cases than 'Extreme' Severity
     b. Of these Stays, the patients with Bed_grades 3 and 4 are more than Bed_grades 1 and 2
     c. Of these Stays, most patients are from Gynaecology Department. This is not new information as the total patients admitted are in that department anyway
    
### Summary of the Models:
I have built several models, as shown in the table above, in the goal of improving the prediction performance while keeping the model complexity in check.
Overall, the models have performed much better in comparison with someone doing random guessing of predicting the Stay of a patient. 
However, most models had tough time raising the prediction accuracy beyond 45%. 
    
This is a challenging dataset, for the following reasons:
    
1. There are 11 classes in the target variable. In general with datasets like this, the odds of predicting the correct class slims down in comparison with datasets with fewer classes in the target variable. Also, the distribution of classes in target variable is very uneven.
    
2. Only, the very deep Decision trees have exhibited very high training accuracy. The rest of the models had 40-45% accuracy even with the training data, pointing that there was high bias. Even the deep decision trees had accuracy on the lower side with the dev and test data, again pointing that there was high bias.
    
3. The ensemble techniques did not improve the performance either. One potential reason for this could be because of (2) listed in the Data Understanding stage. The inherent requirement of Ensemble techiniques, which is: the crowd should have independent opinions. In this dataset, there are many Case_ids per Patient_id; this might be intuitively violating the above inherent requirement, as there are multiple records for a single patient.
    
Model 5 and Model 10 in the above table, have the highest predictive capability of all the models. If I were to recommend using a model, I would prefer using Model 10, because of the fact that it is an ensemble technique and a better diverse model compared to a single decision tree.
    
Next steps:
1. In Module 24 submission, I will explain more the reasons for choosing Accuracy and F1 scores as the evaluation metrics. Also, I will plot the ROC curves of various target classes in each of the models