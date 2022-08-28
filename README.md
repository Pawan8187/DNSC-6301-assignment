# Credit Line Increase Model Card

### Basic Information

* **Person or organization developing model**: Pawan Kumar, `pawanmarine81@gwu.edu`
* **Model date**: 27 August, 2021
* **Model version**: 1.1
* **License**: MIT
* **Model implementation code**: [DNSC_6301_Example_Project.ipynb](https://github.com/Pawan8187/DNSC-6301-assignment/blob/main/DNSC_6301_P.ipynb)

### Intended Use
* **Primary intended uses**: This model is an *example* probability of default classifier, with an *example* use case for determining eligibility for a credit line increase.
* **Primary intended users**: : Mostly by the Graduate student, especially the data and Business analysts’ students 
* **Out-of-scope use cases**: Used in context other than educational purpose. 

### Training Data

* Data dictionary: 

| Name | Modeling Role | Measurement Level| Description|
| ---- | ------------- | ---------------- | ---------- |
|**ID**| ID | int | unique row indentifier |
| **LIMIT_BAL** | input | float | amount of previously awarded credit |
| **SEX** | demographic information | int | 1 = male; 2 = female
| **RACE** | demographic information | int | 1 = hispanic; 2 = black; 3 = white; 4 = asian |
| **EDUCATION** | demographic information | int | 1 = graduate school; 2 = university; 3 = high school; 4 = others |
| **MARRIAGE** | demographic information | int | 1 = married; 2 = single; 3 = others |
| **AGE** | demographic information | int | age in years |
| **PAY_0, PAY_2 - PAY_6** | inputs | int | history of past payment; PAY_0 = the repayment status in September, 2005; PAY_2 = the repayment status in August, 2005; ...; PAY_6 = the repayment status in April, 2005. The measurement scale for the repayment status is: -1 = pay duly; 1 = payment delay for one month; 2 = payment delay for two months; ...; 8 = payment delay for eight months; 9 = payment delay for nine months and above |
| **BILL_AMT1 - BILL_AMT6** | inputs | float | amount of bill statement; BILL_AMNT1 = amount of bill statement in September, 2005; BILL_AMT2 = amount of bill statement in August, 2005; ...; BILL_AMT6 = amount of bill statement in April, 2005 |
| **PAY_AMT1 - PAY_AMT6** | inputs | float | amount of previous payment; PAY_AMT1 = amount paid in September, 2005; PAY_AMT2 = amount paid in August, 2005; ...; PAY_AMT6 = amount paid in April, 2005 |
| **DELINQ_NEXT**| target | int | whether a customer's next payment is delinquent (late), 1 = late; 0 = on-time |

* **Source of training data**: GWU Blackboard, email `jphall@gwu.edu` for more information
* **How training data was divided into training and validation data**: 50% training, 25% validation, 25% test
* **Number of rows in training and validation data**:
  * Training rows: 15,000
  * Validation rows: 7,500

### Test Data
* **Source of test data**: GWU Blackboard, email `jphall@gwu.edu` for more information
* **Number of rows in test data**: 15000 rows, 20 columns in training data, whereas in validation there are 7500 rows, 20 Columns. 
* **State any differences in columns between training and test data**: None

### Model details
* **Columns used as inputs in the final model**: 'LIMIT_BAL',
       'PAY_0', 'PAY_2', 'PAY_3', 'PAY_4', 'PAY_5', 'PAY_6', 'BILL_AMT1',
       'BILL_AMT2', 'BILL_AMT3', 'BILL_AMT4', 'BILL_AMT5', 'BILL_AMT6',
       'PAY_AMT1', 'PAY_AMT2', 'PAY_AMT3', 'PAY_AMT4', 'PAY_AMT5', 'PAY_AMT6'
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

| Tr AUC | Val AUC | Test AUC |
| ------ | ------- | -------- |
| 0.3456 | 0.7891  | 0.7687 |

#### Correlation Heatmap
![Correlation Heatmap](download.png)

#### Iteration Plot Tree Depth vs AUC
![Iteration Plot](Iteration_Plot.png)

#### Ethical considerations:
##### Describe potential negative impacts of using your model:

Math/Software Problems: There is always a high risk of attaining inconsistent results if results are based on recent payment trend while the long-term trends of are overlooked. One of the software problems. In this model also the variable is carrying significant importance too. 

Real world risks: Because of inconsistent result, it is likely that the customers’ credit limit may remain plateau, if not dipped, i.e., increase in credit limits of customer’s’ are almost unlikely. Here the AIR value of Hispanic-to-white is 0.82 which is quite reasonable. 


###### Describe potential uncertainties relating to the impacts of using your model:

Math/Software Problems: A classic example of software problem is that It is quite possible because of one or few low metrics among several high scoring metrics may cause the a unjustified result, eventually causing low credit limit for customers. 

Real world risks: If the output of model will be implemented by the users, then the customers will not be granted additional credit what they deserve. In bigger prospect it will not only hamper the an Individual but also will adversely impact the economy, a negative aftermath of bias model. 

