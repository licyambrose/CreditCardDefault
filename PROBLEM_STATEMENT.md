# Credit card default prediction

### Dataset source: https://www.kaggle.com/datasets/uciml/default-of-credit-card-clients-dataset/data

### Problem statement
#### Business Objective
Estimate the probability that a credit card client will default on their payment in the next month, enabling risk teams to make decisions such as adjusting credit limits, prioritizing collections, or setting monitoring strategies to reduce expected loss.

##### Target Variable
The target variable is "**default.payment.next.month**", which indicates whether a client will default on their credit card payment in the next month. It is a binary variable where 1 indicates default and 0 indicates no default.

##### Input data
- **Dataset size**: 30,000 clients from a Taiwanese bank (UCI/Kaggle dataset).
- **Features**:  23, excluding ID and target variable.
1. **Demographics and account**: LIMIT_BAL, SEX, EDUCATION, MARRIAGE, AGE.
2. **Repayment status history (ordinal delinquency indicators)**: PAY_0, PAY_2, PAY_3, PAY_4, PAY_5, PAY_6.
3. **Statement amounts**: BILL_AMT1–BILL_AMT6.
4. **Payment amounts**: PAY_AMT1–PAY_AMT6.

##### Output
Calibrated probability of default within the next month per client.





