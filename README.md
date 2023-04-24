# capstone1_hospital_resource_mgmt
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

| <span style='background:orange'>Model # | <span style='background:orange'>Model Description | <span style='background:orange'>Purpose | <span style='background:orange'># of Dimensions | <span style='background:orange'>Train/Dev/Test Accuracies | <span style='background:orange'>F1 Scoreon Testset |
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
|<span style='background:yellow'> Model 11 | RandomForests with deep trees to compensate fo... | 100 | 30 | 99.81/33.98/33.79 | 33.79 |

