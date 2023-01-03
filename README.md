# Analysis Details
This is a model of depression treatment outcomes for a single drug, desvenlafaxine. 2,607 patients were sampled, stratified by the remission variable into a split of 2,111 in the training group and 235 in the held-out test group. We used the SGD optimizer and a single layer model architecture with a dropout value of 0.5 from the open source Vulcan project [https://github.com/Aifred-Health/VulcanAI]. This was a non-optimized model aimed at probing differences in performance introduced by adding data from later in the treatment cycle. As this was a toy model aimed at probing mostly the impact of adding the treatment variables from later in treatment, baseline features were selected based on completeness (i.e. features with the least missingness, rather than those best at predicting the outcome; features with the least missingness did not, unfortunately, line up with features we have previously found to be predictive at baseline). In the first model, we predict outcome (remission, binary) with baseline variables; in the second model we predict outcome with baseline variables with the addition of the second visit depression severity score. Model features included in each model are provided in a list below 

baseline model: remission, anhedonia_general, psychomotor_retardation,  sex_Female, Sadness, somatic_gastro_intestinal, depression severity score, sex_Male, age, race_Asian, race_Black, race_Hispanic or Latino, race_White, race_Other


trajectory model: remission, anhedonia_general, psychomotor_retardation,  sex_Female, Sadness, somatic_gastro_intestinal, depression severity score, sex_Male, age, race_Asian, race_Black, race_Hispanic or Latino, race_White, race_Other, visit two depression severity score

As can be seen, adding data from later in the treatment cycle did not improve outcome prediction, as opposed to what we hypothesized and what has been demonstrated in other work, but overall model performance is poor, suggesting the need for improved optimization with a neural network architecture and rigorous checks of data quality. The former may be provided by Bayesian optimization techniques, which we have used in previous work and which has yielded improved results. Imputation techniques would also make more data available; they were not used here purely because of the focus on adding in post-baseline variables and focusing on their impact. This will be trialed in future analyses using multiple drugs. The overall poor results here essentially demonstrate that to leverage a neural network properly in these kinds datasets, we cannot rely on single data points but must properly optimize the model over the entire dataset. This is intended as a teaching point for further work; the results themselves are not intended to have clinical meaning. Future models will help use determine if subgroups of patients who show early improvement are different at baseline than those who do not, and in what way this relates to ultimate treatment outcome.

# Model Results
1. Baseline Model
    - Accuracy: 0.6436
    - AUC: 0.5304
    - F1-Score: 0.2439
    - NPV: 0.7320
    - PPV: 0.2884
    - Sensitivity: 0.2112
    - Specificity: 0.805
2. Trajectory Model
    - Accuracy: 0.209
    - AUC: 0.3338
    - F1-Score: 0.346
    - NPV: 0.0
    - PPV: 0.2195
    - Sensitivity: 0.8181
    - Specificity: 0.0

# File Descriptions

1. hyperparameters.txt - Details outlining the structure of the neural network used for the models and the features. 
2. baseline/ - .pkl Files containing trained baseline model information that can be loaded using our Vulcan package. 
4. initial_trajectory/ - .pkl Files containing trained trajectory model information that can be loaded using our Vulcan package. 
