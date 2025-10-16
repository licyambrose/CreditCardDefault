# Credit card default prediction

#### Dataset source: https://www.kaggle.com/datasets/uciml/default-of-credit-card-clients-dataset/data

## Cross-Industry Standard Process for Data Mining (CRISP-DM) methodology
### 1. Business Understanding
- **Objective**: To predict the likelihood of a credit card client defaulting on their next month's payment.
- **Goal**: Enable the financial institution to proactively manage credit risk. This involves making informed decisions like adjusting credit limits, personalizing collection strategies, or flagging high-risk accounts to minimize financial losses.
- **Success Criteria**: A model that provides a reliable probability of default, which can be integrated into the bank's risk management workflow to reduce the rate of actual defaults.

### 2. Data Understanding
- **Data Source**: The project uses the 'UCI Credit Card' dataset, containing information on 30,000 clients from a Taiwanese bank.
- **Initial Data Collection**: The data is loaded from data/UCI_Credit_Card.csv into a pandas DataFrame.
- **Data Exploration**: The dataset includes 25 columns. The target variable is default.payment.next.month. The features consist of:
1. **Client demographics** (SEX, EDUCATION, MARRIAGE, AGE).
2. **Financial standing** (LIMIT_BAL).
3. **History of past payments** (PAY_0, PAY_2 to PAY_6).
4. **Bill statement amounts** (BILL_AMT1 to BILL_AMT6).
5. **Previous payment amounts** (PAY_AMT1 to PAY_AMT6).
- **Initial Data Quality Check**: The data.info() and data.shape commands are used to get an overview of data types, non-null counts, and the dimensions of the dataset.

#### I have performed the following steps for data understanding:
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

### 3. Data Preparation
After our initial exploration and fine-tuning of the business understanding, it is time to construct our final dataset prior to modeling. Here, we want to make sure to handle any integrity issues and cleaning, the engineering of new features, any transformations that we believe should happen (scaling, logarithms, normalization, etc.), and general preparation for modeling with sklearn.

- **Load the data**: Read the UCI_Credit_Card.csv file into a pandas DataFrame.
- **Initial Exploration**: Examine the first few rows, column names, and data types.
- **Meaningful names** for columns
- **Missing Values**: Check for missing values in each column to identify data quality issues.
- **Target Variable Analysis**: Analyze the distribution of the 'default.payment.next.month' column to spot outliers or skewness.
- **Feature Analysis**:
1. **For categorical features**, I'll examine the unique values and their frequencies.
2. **For numerical features**, I'll look at their distributions using histograms.

![images/img.png](images/img.png)

#### Exploratory Data Analysis (EDA)
##### Summary of Bar Plots

The bar plots reveal several key trends about the factors influencing credit card defaults:

##### Categorical Features:
- **Repayment Status**: This is clearly the most significant predictor. The default rate rises sharply as the payment delay increases from one month to two or more. Clients who pay in full or have no consumption have a very low risk of default.
- **Gender**: There is a slight difference in default rates between genders, with one gender showing a marginally higher tendency to default.
- **Education**: Default rates vary across education levels. Typically, higher levels of education (like graduate school) are associated with a lower default rate compared to lower levels (like high school).
- **Marital Status**: The default rate differs between married and single clients, with one group showing a slightly higher propensity to default.

##### Numerical Features (Binned):
- **Credit Limit**: There is a strong inverse relationship. Clients in the lowest credit limit bracket have the highest default rate, and the rate consistently decreases as the credit limit increases.
- **Age**: The default rate shows some variation across different age groups. It is often observed that younger clients might have a slightly higher default rate.
- **Bill Amounts**: The trend for bill amounts is not always linear. However, it can sometimes be seen that clients with very low or very high bill amounts relative to their credit limit have different default behaviors.
- **Previous Payments**: Similar to credit limit, there's a noticeable trend here. Clients who make smaller previous payments (relative to their bill amount) tend to have a higher default rate.

These insights are crucial for feature engineering and for understanding the final model's behavior. The repayment status, in particular, stands out as a dominant feature.
![images/img_1.png](images/img_1.png)
![images/img_2.png](images/img_2.png)
![images/img_3.png](images/img_3.png)
![images/img_4.png](images/img_4.png)
![images/img_5.png](images/img_5.png)
![images/img_6.png](images/img_6.png)
![images/img_7.png](images/img_7.png)
![images/img_8.png](images/img_8.png)
![images/img_9.png](images/img_9.png)

### 4. Modeling
#### Modeling approaches
- **Use all 24 features for the prediction**

1. **Models to be used**
- Logistic Regression
- K-Nearest Neighbors
- Decision Tree
- Support Vector Machine

2. **Model will be evaluated based on the below factors**
- Precision
- Recall
- F1 Score
- Accuracy
- Confusion matrix - Minimizing False Positives and False Negatives

3. **If the above factors are not satisfied improve the model with the below technics**
- Hyper parameter tuning with GridSearchCV and RandomizedSearchCV will be performed
- Applying class_weight='balanced'
- Applying class_weight='balanced' along with other configs for the model
- Ensemble methods for better prediction reducing bias and reduce variance (Bagging - High Variance - choose Random Forest, High bias - Boosting - choose AdaBoost/GradientBooster trees)

#### Overall model comparison Summary

| Feature Set  | Tuning   | Ensemble   | Class Weighting | Model               | precision | Recall | F1-score | Training accuracy | Testing accuracy |
|--------------|----------|------------|-------------|---------------------|--------|--------|--------|-----------|--------|
| All Features | NONE     | NONE       | NONE        | Logistic Regression | 0.690323   | 0.241899 | 0.358259 |  0.811833 | 0.808333 |
| All Features | NONE     | NONE       | NONE        | K-Nearest Neighbors | 0.547368   | 0.352675 | 0.428964 |  0.840958 | 0.792333 |
| All Features | NONE     | NONE   | NONE        | Decision Tree       | 0.370779   | 0.405426 | 0.387329 |  0.999458 | 0.716333 |
| All Features | NONE     | NONE   | NONE        | Support Vector Machine | 0.666172   | 0.338357 | 0.448776 | 0.825208 | 0.816167 |
| All Features | GridSearchCV | NONE   | NONE        | Logistic Regression | 0.686567   |0.242653|0.358575|0.811833|0.808000|
| All Features | GridSearchCV | NONE   | NONE        | K-Nearest Neighbors | 0.579618   |0.342879|0.430871|0.834042|0.799667|
| All Features | GridSearchCV | NONE   | NONE        | Decision Tree       | 0.621693   |0.354182|0.451272|0.844833|0.809500|
| All Features | GridSearchCV | NONE   | NONE        | Support Vector Machine | 0.661120   |0.329314|0.439638|0.834458|0.814333|
| All Features | RandomizedSearchCV | NONE   | NONE        | Logistic Regression | 0.686567   |0.242653|0.358575|0.811833|0.808000|
| All Features | RandomizedSearchCV | NONE   | NONE        | K-Nearest Neighbors | 0.571608   |0.342879|0.428639|0.834250|0.797833|
| All Features | RandomizedSearchCV | NONE   | NONE        | Decision Tree       | 0.627346   |0.352675|0.451520|0.843458|0.810500|
| All Features | RandomizedSearchCV | NONE   | NONE        | Support Vector Machine | 0.661120   |0.329314|0.439638|0.834458|0.814333|
| All Features | NONE     | NONE       | Balanced    | Logistic Regression |0.367083|0.620196|0.461194|0.694042|0.679500|
| All Features | NONE     | NONE       | Balanced    | K-Nearest Neighbors |0.547368|0.352675|0.428964|0.840958|0.792333|
| All Features | NONE     | NONE   | NONE        | Decision Tree       |0.386086|0.380558|0.383302|0.999375|0.729167|
| **All Features** | **NONE**     | **NONE**   | **Balanced**    | **Support Vector Machine** |**0.494997**|**0.559156**|**0.525124**|**0.789208**|**0.776333**|
| All Features | NONE     | NONE       | Balanced +  | Logistic Regression |0.367083|0.620196|0.461194|0.693958|0.679500|
| All Features | NONE     | NONE       | Balanced +  | K-Nearest Neighbors |0.547368|0.352675|0.428964|0.840958|0.792333|
| All Features | NONE     | NONE   | NONE        | Decision Tree       |0.386086|0.380558|0.383302|0.999375|0.729167|
| All Features | NONE     | NONE   | Balanced +  | Support Vector Machine |0.467347|0.517709|0.491241|0.770083|0.762833|
| All Features | NONE     | AdaBoost | NONE        | Logistic Regression |0.771429|0.040693|0.077309| 0.782042  |0.785167|
| **All Features** | **NONE**     | **AdaBoost** | **NONE**        | **Decision Tree**                |**0.669151**|**0.338357**|**0.449449**| **0.820458**  |**0.816667**|
| **All Features** | **NONE**     | **GradientBoostTrees** | **NONE**        | **Decision Tree**                |**0.610697**|**0.370008**|**0.460817**|**0.84575**|**0.8085**|


### **Best by F1-score and recall**

| Feature Set  | Tuning   | Ensemble   | Class Weighting | Model               | precision | Recall | F1-score | Training accuracy | Testing accuracy |
|--------------|----------|------------|-------------|---------------------|--------|--------|--------|-----------|--------|
| **All Features** | **NONE**     | **NONE**   | **Balanced**    | **Support Vector Machine** |**0.494997**|**0.559156**|**0.525124**|**0.789208**|**0.776333**|

### **Best by testing accuracy. If we want slightly higher testing accuracy**

| Feature Set  | Tuning   | Ensemble   | Class Weighting | Model               | precision | Recall | F1-score | Training accuracy | Testing accuracy |
|--------------|----------|------------|-------------|---------------------|--------|--------|--------|-----------|--------|
| **All Features** | **NONE**     | **AdaBoost** | **NONE**        | **Decision Tree**                |**0.669151**|**0.338357**|**0.449449**| **0.820458**  |**0.816667**|

### **Best by recall. If we prioritize F1-score and balanced performance**

| Feature Set  | Tuning   | Ensemble   | Class Weighting | Model               | precision | Recall | F1-score | Training accuracy | Testing accuracy |
|--------------|----------|------------|-------------|---------------------|--------|--------|--------|-----------|--------|
| **All Features** | **NONE**     | **GradientBoostTrees** | **NONE**        | **Decision Tree**                |**0.610697**|**0.370008**|**0.460817**|**0.84575**|**0.8085**|

### **Final Decision - Going with Balanced SVM**

| Feature Set  | Tuning   | Ensemble   | Class Weighting | Model               | precision | Recall | F1-score | Training accuracy | Testing accuracy |
|--------------|----------|------------|-------------|---------------------|--------|--------|--------|-----------|--------|
| **All Features** | **NONE**     | **NONE**   | **Balanced**    | **Support Vector Machine** |**0.494997**|**0.559156**|**0.525124**|**0.789208**|**0.776333**|

![images/img_10.png](images/img_10.png)

### 5. Evaluation

- The trained model is evaluated to assess its performance based on the business objective.

- **Metrics**: The evaluation focuses on metrics such as precision, recall, and F1-score, which are especially important for imbalanced datasets. Accuracy is also measured for both training and testing datasets.

- **Final Decision**: The evaluation results show that a **balanced SVM model** achieves a **precision of 0.495**, a **recall of 0.559**, and an **F1-score of 0.525**, making it the final selected model.

- **The most influential features** in predicting credit card default are related to the **repayment status in recent months**.

- **Most Important Features**: The **top three most important features** are the client's repayment status in **September (Repayment_Status_Sept), August (Repayment_Status_Aug), and June (Repayment_Status_Jun)**. This indicates that recent payment behavior is the **most critical factor for the model's decision-making**.

- **Least Important Features**: The features with the least influence on the model's predictions include **Previous_Payment_Aug, Bill_Amount_Apr, and Gender**. The importance scores for these **features are very close to zero**, suggesting they do not significantly impact the model's ability to predict default.

### 6. Deployment

- svm_pipeline.pkl - This file contains the trained SVM model pipeline, which includes all preprocessing steps and the final model. It can be used to make predictions on new data.
