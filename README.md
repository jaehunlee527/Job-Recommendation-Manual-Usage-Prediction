## Job Care Manual Usage Classification
### Competition Summary
[Korea Employment Information Service](http://www.keis.or.kr) currently operates an AI platform that analyzes potential employees' traits and provides them with proper trainings, consultings and support. The organization hosted an open competition on [DACON(AI Hackathon Platform)](https://dacon.io/competitions/official/235863/overview/description), where participants are expected to build classification models that predict whether people accessing their platform would decide to use the educational materials. The competition is part of their effort to eventually develop an individualized contents recommender system.

### Data
(Be aware that since this is a local competition in Korea, some of the texts are originally written in Korean.)
* train.csv
* test.csv
* Property_D_code.csv: Template for sub-categories value matching for each value in the D attribute 
* Property_H_code.csv: Template for sub-categories value matching for each value in the H attribute
* Property_L_code.csv: Template for sub-categories value matching for each value in the L attribute

Each column in the train & test set represents either user or content attribute by each user. Each column name is labeled in alphabet codes (in order to conceal actual questionnaire), so we have no idea what each feature actually represents. The pdf guide only provides extra information whether the values for columns are ordinal or nominal. Based on this information, we will engineer features. 

### Feature Engineering
First extract hour from the content_open_dt and add it as a new column. All the other columns were in int values. For ordinal columnns, so particular adjustment has to be made. For nominal columns, since the scale of numbers does not reflect the magnitude, I had to target encode each column value based on the ratio of 1 to 0. For some columns that did not show much differentiability, I had to drop them to prevent overfitting on train data. 

Before training, the feature values had to be scaled for some models like Logistic Regression and SVC.

### Models
The following models were used:
* Random Forest Classifier
* Logistic Regression
* SVC
* XGB Classifier
* LDA
* Catboost Classifier

Catboost outperformed by far. I used Optuna library for hyperparameter tuning.
