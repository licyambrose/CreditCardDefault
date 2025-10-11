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
- Drop ID column as it is not needed for prediction.
- For Education, 1=graduate school, 2=university, 3=high school, 4=others. Values 0, 5, and 6 are not documented and can be grouped into 'others' (4).
- For Marital Status, 1=married, 2=single, 3=others. The value 0 is not documented and can be grouped into 'others' (3).
- Verify the unique values after cleaning.
- Save the cleaned data to a new CSV file.
- Load the cleaned data to verify.
