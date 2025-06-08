
# Simple Linear Regression model

```python

#Splitting dataset into training and test set
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state=1)

#Simple Linear Regression model
from sklearn.linear_model import LinearRegression
regressor = LinearRegression()
regressor.fit(X_train, y_train)

#Predict the test set results
#y_test consists the real salary
#y_pred consists the predict salary
y_pred = regressor.predict(X_test)

#Visualizing the Training set Results
plt.scatter(X_train, y_train, color = 'red')
plt.plot(X_train, regressor.predict(X_train), color = 'blue')
plt.title('Salary Vs Exp (Training Set)')
plt.xlabel('Years of Exp')
plt.ylabel('Salary')
plt.show()

#Visualize the Test set results
plt.scatter(X_test, y_test, color = 'red')
plt.plot(X_train, regressor.predict(X_train), color = 'blue')
plt.title('Salary Vs Exp (Training Set)')
plt.xlabel('Years of Exp')
plt.ylabel('Salary')
plt.show()
```