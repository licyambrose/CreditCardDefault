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