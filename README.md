Project Title: Predicting House Prices
Objective
The objective of this project is to develop a predictive model that can accurately estimate house prices based on various features such as the size of the house, the number of bedrooms, the location, and other relevant factors.

Data Source
The data for this project is sourced from the Kaggle House Prices dataset.

Import Libraries

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score

Import Data

data = pd.read_csv('house_prices.csv')

Describe Data

data.info()
data.describe()
data.head()

Data Visualization
Distribution of Target Variable

plt.figure(figsize=(10, 6))
sns.histplot(data['SalePrice'], kde=True)
plt.title('Distribution of House Prices')
plt.xlabel('Sale Price')
plt.ylabel('Frequency')
plt.show()

Correlation Heatmap

plt.figure(figsize=(12, 8))
corr_matrix = data.corr()
sns.heatmap(corr_matrix, annot=True, cmap='coolwarm')
plt.title('Correlation Heatmap')
plt.show()

Pairplot of Selected Features

selected_features = ['OverallQual', 'GrLivArea', 'GarageCars', 'TotalBsmtSF', 'FullBath', 'YearBuilt']
sns.pairplot(data[selected_features + ['SalePrice']])
plt.show()

Data Preprocessing
Handling Missing Values

data = data.fillna(data.mean()) # Simple imputation for missing values

Encoding Categorical Variables

data = pd.get_dummies(data, drop_first=True)

Define Target Variable (y) and Feature Variables (X)

X = data.drop('SalePrice', axis=1)
y = data['SalePrice']

Train Test Split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

Modeling
model = LinearRegression()
model.fit(X_train, y_train)

Model Evaluation
Training Performance
y_train_pred = model.predict(X_train)
mse_train = mean_squared_error(y_train, y_train_pred)
r2_train = r2_score(y_train, y_train_pred)
print(f'Training MSE: {mse_train}')
print(f'Training R2 Score: {r2_train}')

Testing Performance

y_test_pred = model.predict(X_test)
mse_test = mean_squared_error(y_test, y_test_pred)
r2_test = r2_score(y_test, y_test_pred)
print(f'Test MSE: {mse_test}')
print(f'Test R2 Score: {r2_test}')

Prediction

Predicting house prices for the test set
predictions = model.predict(X_test)
predictions[:5] # Display first 5 predictions

Explanation
In this project, we developed a predictive model to estimate house prices using various features. After preprocessing the data, we trained a linear regression model and evaluated its performance using mean squared error and R-squared metrics. The model showed a decent fit on the training data and provided reasonable predictions on the test data. Further improvements could include trying more sophisticated models, feature engineering, and hyperparameter tuning to enhance predictive performance.
