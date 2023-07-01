# RML_Final_Project

## Model Card

### Basic Information

* **Person or organization developing model**: Joon kyu Hong, `joonhong96@gwu.edu`
* **Model date**: July 1st, 2023
* **Model version**: 1.0
* **License**: MIT
* **Model implementation codes**:

[RML_Assignment1_Joonkyu_Hong.ipynb](https://github.com/JOONKYUHONG/DNSC6290_RML/blob/main/RML_Assignment%201_%20Joonkyu%20Hong.ipynb)

[RML_Assignment2_Joonkyu_Hong.ipynb](https://github.com/JOONKYUHONG/DNSC6290_RML/blob/main/RML_Assignment%202_Joonkyu%20Hong-Copy1.ipynb)

[RML_Assignment3_Joonkyu_Hong.ipynb](https://github.com/JOONKYUHONG/DNSC6290_RML/blob/main/RML_Assignment%203_Joonkyu%20Hong.ipynb)

[RML_Assignment4_Joonkyu_Hong.ipynb](https://github.com/JOONKYUHONG/DNSC6290_RML/blob/main/RML_Assignment%204_Joonkyu%20Hong.ipynb)

[RML_Assignment5_Joonkyu_Hong.ipynb](https://github.com/JOONKYUHONG/DNSC6290_RML/blob/main/RML_Assignment%205_Joonkyu%20Hong.ipynb) 


### Intended Use

* **Business Value**: Enhancing educational value for students studying mortgage lending in an academic setting.
* **Objective**: Providing practical experience in responsible machine learning projects for educational purposes.
* **Intended Users** : MSBA students and educators in the academic context of responsible machine learning.
* **Additional Information** : Valuable educational resource for GWU students.
  
### Training Data

* Data dictionary: 

| Name                      | Modeling Role | Measurement Level | Description                                                                                     |
|---------------------------|---------------|-------------------|-------------------------------------------------------------------------------------------------|
| high priced               | target        | binary            | Binary target indicating whether the APR charged for a mortgage is 1.5% or more above the survey-based estimate of similar mortgages    |
| conforming                | input         | binary            | Binary numeric input indicating whether the mortgage conforms to normal standards (1) or is different (0)                              |
| debt to income ratio std  | input         | numeric           | Standardized debt-to-income ratio for mortgage applicants                                        |
| debt to income ratio missing  | input         | binary        | Binary numeric input serving as a missing marker (1) for debt-to-income ratio std                 |
| income std                | input         | numeric           | Standardized income for mortgage applicants                                                     |
| loan amount std           | input         | numeric           | Standardized amount of the mortgage for applicants                                              |
| intro rate period std     | input         | numeric           | Standardized introductory rate period for mortgage applicants                                   |
| loan to value ratio std   | input         | numeric           | Ratio of the mortgage size to the value of the property for mortgage applicants                 |
| no intro rate period std  | input         | binary            | Binary numeric input indicating whether a mortgage does not include an introductory rate period |
| property value std        | input         | numeric           | Value of the mortgaged property                                                                 |
| term 360                  | input         | binary            | Binary numeric input indicating whether the mortgage is a standard 360-month mortgage (1) or a different type (0)                  |


* **Source of training data**: GWU Blackboard, email `jphall@gwu.edu` for more information
* **How training data was divided into training and validation data**: 70% training, 30% validation
* **Number of rows in training and validation data**:
  * Training rows: 112253 rows
  * Validation rows: 48085 rows


* **Source of test data**: GWU Blackboard, email `jphall@gwu.edu` for more information
* **Number of rows in test data**: 19831 rows.
* **State any differences in columns between training and test data**: Training data contains 23 rows, while Test data contains 22 rows since we need to predict the target variable and probabiltiy when we test the best remediated model. 

### Evaluation (test) Data

* **Source of test data**: GWU Blackboard, email `jphall@gwu.edu` for more information
* **Number of rows in test data**: 19831 rows.
* **Differences in columns between training and test data**: The training data contains 23 columns, while the test data contains 22 columns since we need to predict the target variable and probability when testing the best remediated model.
### Model details
* **Columns used as inputs in the final model**:
```

rem_x_names = ['term_360',
 'no_intro_rate_period_std',
 'property_value_std',
 'intro_rate_period_std',
 'income_std',
 'debt_to_income_ratio_std',
 'conforming']

```
* **Column(s) used as target(s) in the final model**: 'high_priced'
* **Type of model**: XGBoost
* **Software used to implement the model**: Python, xgboost
* **Version of the modeling software**: 3.10.9, 1.7.5
* **Hyperparameters or other settings of your model**: 
```
rem_params = {'max_depth': 9,
 'learning_rate': 0.05,
 'subsample': 1.0,
 'colsample_bytree': 0.6,
 'min_child_weight': 5,
 'gamma': 0.1,
 'reg_alpha': 0.1,
 'reg_lambda': 1.0,
 'n_jobs': -1,
 'random_state': 12345}
```
### Quantitative Analysis

* **Metrics used to evaluate the best remediated model**:
  
| Group | Validation AIR |
|-------|-----|
| Asian vs. White | 1.148|
| Black vs. White | 0.806 |
| Hispanic vs. White | 0.875|
| Female vs. Male | 0.945 |

* Values of the metrics for training, validation, and evaluation (or test) data
 
| Train AUC | Validation AUC | Test AUC |
| ------ | ------- | -------- |
| 0.3456 | 0.7891  | 0.7687|


(*Test AUC taken from https://github.com/jphall663/GWU_rml/blob/master/assignments/model_eval_2023_06_21_12_52_47.csv)

#### Correlation Heatmap
![Correlation Heatmap](correlation.png)


∗ **Alternative models considered** : Among the three models trained, namely Elastic Net, EBM, and XGBoost, the XGBoost model demonstrates superior performance in terms of test AUC when compared to the AUC obtained from the other two models.


– Intended use (2 pts.)

∗ Describe the business value of your group’s best remediated model
∗ Describe how your group’s best remediated model is designed to be used
∗ Describe the intended users for your group’s best remediated model
∗ State whether your group’s best remediated model can or cannot be used for any additional
purposes
– Training data (2 pts.)
∗ State the source of training data
∗ State how training data was divided into training and validation data
∗ State the number of rows in training and validation data
∗ Define the meaning of all training data columns
∗ Define the meaning of all engineered columns
– Evaluation data (2 pts.)
∗ State the source of evaluation (or test) data
∗ State the number of rows in evaluation (or test) data
∗ State any differences in columns between training and evaluation (or test) data
– Model details (2 pts.)
∗ State the columns used as inputs in your group’s best remediated model
∗ State the columns used as targets in your group’s best remediated model
∗ State the type of your group’s best remediated model
∗ State the software used to implement your group’s best remediated model
∗ State the version of the modeling software for your group’s best remediated model
∗ State the hyperparameters or other settings of your group’s best remediated model
– Quantitative analysis (3 pts.)
∗ State the metrics used to evaluate your group’s best remediated model
∗ State the values of the metrics for training, validation, and evaluation (or test) data – evaluation (or test) metrics come from the most recent class full evaluation results, link under
Assignment 1.
∗ Provide at least one plot or table from each weekly assignment for a total of at least six plots,
that must include the global variable importance and partial dependence of your group’s best
remediated model.
∗ Address other alternative models considered
– Ethical considerations (2 pts.)
2
∗ Describe potential negative impacts of using your group’s best remediated model:
· Consider math or software problems
· Consider real-world risks: who, what, when and how?
∗ Describe potential uncertainties relating to the impacts of using your group’s best remediated
model:
· Consider math or software problems
· Consider real-world risks: who, what, when and how?
∗ Describe any unexpected or results encountered during training
