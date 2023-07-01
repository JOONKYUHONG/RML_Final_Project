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

* **Business Value**: The best remediated model will contribute to the lender's long-term success, profitability, and sustainability in the mortgage lending industry.
* **Objective**: The best remediated model can be used as an essential method or approach for identifying potential predatory lending practices, protecting consumers, promoting fair lending, ensuring market transparency, and facilitating accurate risk assessment for investors.
* **Intended Users** : The best remediated model can be customized to cater to the diverse needs of stakeholders across the mortgage industry, encompassing lenders, regulators, borrowers, and investors.
* **Any Additional** : GWU Students pursuing research projects or theses related to housing finance, consumer protection, or lending practices can utilize the model's predictions as a valuable data source. They can analyze the deviations in APRs, assess the impact on borrowers, and explore potential solutions to address unfair lending practices

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

### Evaluation (test) Data
* **Source of test data**: GWU Blackboard, email `jphall@gwu.edu` for more information
* **Number of rows in test data**: 19831 rows.
* **State any differences in columns between training and test data**: Training data contains 23 rows, while Test data contains 22 rows since we need to predict the target variable and probabiltiy when we test the best remediated model. 

### Model details
* **Columns used as inputs in the final model**: ['property_value_std','debt_to_income_ratio_missing','debt_to_income_ratio_std','income_std','intro_rate_period_std']
* **Column(s) used as target(s) in the final model**: 'DELINQ_NEXT'
* **Type of model**: Decision Tree 
* **Software used to implement the model**: Python, scikit-learn
* **Version of the modeling software**: 0.22.2.post1
* **Hyperparameters or other settings of your model**: 
```
DecisionTreeClassifier(ccp_alpha=0.0, class_weight=None, criterion='gini',
                       max_depth=6, max_features=None, max_leaf_nodes=None,
                       min_impurity_decrease=0.0, min_impurity_split=None,
                       min_samples_leaf=1, min_samples_split=2,
                       min_weight_fraction_leaf=0.0, presort='deprecated',
                       random_state=12345, splitter='best')
```
### Quantitative Analysis

* Models were assessed primarily with AUC and AIR. See details below:

| Train AUC | Validation AUC | Test AUC |
| ------ | ------- | -------- |
| 0.3456 | 0.7891  | 0.7687* |

| Group | Validation AIR |
|-------|-----|
| Black vs. White | 0.8345 |
| Hispanic vs. White | 0.8765 |
| Asian vs. White | 1.098 |
| Female vs. Male | 1.245 |


(*Test AUC taken from https://github.com/jphall663/GWU_rml/blob/master/assignments/model_eval_2023_06_21_12_52_47.csv)

#### Correlation Heatmap
![Correlation Heatmap](download.png)

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
