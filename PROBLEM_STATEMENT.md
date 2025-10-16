# Credit card default prediction

#### Dataset source: https://www.kaggle.com/datasets/uciml/default-of-credit-card-clients-dataset/data

## Problem statement
### 1. Research Question
The research question is: Can a model accurately estimate the probability of a credit card client defaulting on their payment in the next month?

### 2. Expected Data Source(s)
The data source for this project is a public dataset from the UCI Machine Learning Repository, available on Kaggle: Default of Credit Card Clients Dataset Links to an external site.. It includes data from 30,000 credit card clients in Taiwan.
https://www.kaggle.com/datasets/uciml/default-of-credit-card-clients-dataset/data

### 3. Analysis Techniques
Since this is classification problem below are the approaches I plan to take for credit card default prediction

- Use all 24 features for the prediction

#### **Models to be used**
1. Logistic Regression
2. K-Nearest Neighbors
3. Decision Tree
4. Support Vector Machine

#### **Model will be evaluated based on the below factors**
1. Precision
2. Recall
3. F1 Score
4. Accuracy
5. Confusion matrix - Minimizing False Positives and False Negatives

#### **If the above factors are not satisfied improve the model with the below technics**
1. Hyper parameter tuning with GridSearchCV and RandomizedSearchCV will be performed
2. Applying class_weight='balanced'
3. Applying class_weight='balanced' along with other configs for the model
4. Ensemble methods for better prediction reducing bias and reduce variance (Bagging - High Variance - choose Random Forest, High bias - Boosting - choose AdaBoost/GradientBooster trees)

### 4. Expected Results
The final selected model will be selected based on the following performance metrics:

1. Precision score
2. Recall
3. F1-score
4. Training and testing accuracy

### 5. Importance of the Question
Answering this question is critical because it directly supports a bank's risk management efforts. By predicting the likelihood of default, the model provides valuable insights that enable risk teams to proactively make data-driven decisions. These decisions, such as adjusting credit limits, prioritizing collections, or setting up monitoring strategies, can help reduce financial losses and minimize risk for the institution.

### Business Objective
Estimate the probability that a credit card client will default on their payment in the next month, enabling risk teams to make decisions such as adjusting credit limits, prioritizing collections, or setting monitoring strategies to reduce expected loss.

#### Target Variable
The target variable is "**default.payment.next.month**", which indicates whether a client will default on their credit card payment in the next month. It is a binary variable where 1 indicates default and 0 indicates no default.

#### Input data
- **Dataset size**: 30,000 clients from a Taiwanese bank (UCI/Kaggle dataset).
- **Features**:  23, excluding ID and target variable.
1. **Client demographics** (SEX, EDUCATION, MARRIAGE, AGE).
    - **SEX**: 1 = Male, 2 = Female
    - **EDUCATION**: 1 = Graduate School, 2 = University, 3 = High School, 4 = Others
    - **MARRIAGE**: 1 = Married, 2 = Single, 3 = Others
2. **Financial standing** (LIMIT_BAL).
3. **History of past payments** (PAY_0, PAY_2 to PAY_6). The repayment status is on a scale from -2 to 9, where:
    - -2: No consumption
    - -1: Paid in full
    - 0: The use of revolving credit (paid minimum due)
    - 1-9: Payment delay for 1-9 months or more
4. **Bill statement amounts** (BILL_AMT1 to BILL_AMT6).
5. **Previous payment amounts** (PAY_AMT1 to PAY_AMT6).

#### Output
Calibrated probability of default within the next month per client.

### Data understanding
To understand the dataset, I would take the following steps:

- **Load the data**: Read the UCI_Credit_Card.csv file into a pandas DataFrame.
- **Initial Exploration**: Examine the first few rows, column names, and data types.
- **Descriptive Statistics**: Generate summary statistics for numerical columns to understand their distribution (e.g., mean, median, min, max).
- **Meaningful names** for columns
- **Missing Values**: Check for missing values in each column to identify data quality issues.
- **Target Variable Analysis**: Analyze the distribution of the 'default.payment.next.month' column to spot outliers or skewness.
- **Feature Analysis**:
1. **For categorical features**, I'll examine the unique values and their frequencies.
2. **For numerical features**, I'll look at their distributions using histograms.
- **Correlation Analysis**: Investigate relationships between features and the target variable, 'default.payment.next.month'.

### Data preparation
After our initial exploration and fine-tuning of the business understanding, it is time to construct our final dataset prior to modeling. Here, we want to make sure to handle any integrity issues and cleaning, the engineering of new features, any transformations that we believe should happen (scaling, logarithms, normalization, etc.), and general preparation for modeling with sklearn.
- Drop ID column as it is not needed for prediction.
- For Education, 1=graduate school, 2=university, 3=high school, 4=others. Values 0, 5, and 6 are not documented and can be grouped into 'others' (4).
- For Marital Status, 1=married, 2=single, 3=others. The value 0 is not documented and can be grouped into 'others' (3).
- Rename the column titles for readability
- Verify the unique values after cleaning.
- Save the cleaned data to a new CSV file(credit_card_cleaned.csv).
- Load the cleaned data to verify null values, number of columns and rows.