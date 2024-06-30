### Day 8: Advanced Machine Learning Concepts

#### Advanced ML Techniques: Feature Selection, Model Evaluation, Cross-Validation

**Feature Selection:**
Feature selection involves selecting the most important features (variables) in your dataset that contribute to the predictive power of your machine learning model. It helps in reducing overfitting, improving model performance, and reducing training time.

**Techniques for Feature Selection:**
1. **Filter Methods:** Use statistical techniques to score the relevance of features (e.g., correlation coefficients, chi-square test).
2. **Wrapper Methods:** Use a subset of features to train a model and evaluate performance (e.g., recursive feature elimination).
3. **Embedded Methods:** Perform feature selection as part of the model training process (e.g., Lasso regression).

**Example:**
```python
from sklearn.datasets import load_boston
from sklearn.feature_selection import SelectKBest, f_regression

# Load dataset
data = load_boston()
X = data.data
y = data.target

# Select top 5 features
selector = SelectKBest(score_func=f_regression, k=5)
X_new = selector.fit_transform(X, y)

print(f"Selected Features Shape: {X_new.shape}")
```

**Model Evaluation:**
Model evaluation involves assessing the performance of a machine learning model. Common evaluation metrics include accuracy, precision, recall, F1 score, and ROC-AUC score.

**Evaluation Metrics:**
1. **Accuracy:** Proportion of correctly predicted instances.
2. **Precision:** Proportion of true positive instances among the predicted positive instances.
3. **Recall:** Proportion of true positive instances among the actual positive instances.
4. **F1 Score:** Harmonic mean of precision and recall.
5. **ROC-AUC Score:** Area under the receiver operating characteristic curve.

**Example:**
```python
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score, roc_auc_score

# Load dataset
data = load_boston()
X = data.data
y = data.target

# Split dataset
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Train model
model = LogisticRegression(max_iter=1000)
model.fit(X_train, y_train)

# Make predictions
y_pred = model.predict(X_test)

# Evaluate model
accuracy = accuracy_score(y_test, y_pred)
precision = precision_score(y_test, y_pred, average='weighted')
recall = recall_score(y_test, y_pred, average='weighted')
f1 = f1_score(y_test, y_pred, average='weighted')
roc_auc = roc_auc_score(y_test, model.predict_proba(X_test), multi_class='ovr')

print(f"Accuracy: {accuracy}")
print(f"Precision: {precision}")
print(f"Recall: {recall}")
print(f"F1 Score: {f1}")
print(f"ROC-AUC Score: {roc_auc}")
```

**Cross-Validation:**
Cross-validation is a technique for assessing the generalizability of a machine learning model by splitting the dataset into multiple folds and training/testing the model on different subsets of the data. The most common method is k-fold cross-validation.

**Example:**
```python
from sklearn.model_selection import cross_val_score
from sklearn.ensemble import RandomForestClassifier

# Load dataset
data = load_boston()
X = data.data
y = data.target

# Initialize model
model = RandomForestClassifier()

# Perform 5-fold cross-validation
scores = cross_val_score(model, X, y, cv=5, scoring='accuracy')

print(f"Cross-Validation Scores: {scores}")
print(f"Mean Score: {scores.mean()}")
```

#### Practical Session: Implementing Advanced ML Techniques in Python

**Feature Selection Example:**
```python
from sklearn.datasets import load_boston
from sklearn.feature_selection import SelectKBest, f_regression
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

# Load dataset
data = load_boston()
X = data.data
y = data.target

# Select top 5 features
selector = SelectKBest(score_func=f_regression, k=5)
X_new = selector.fit_transform(X, y)

# Split dataset
X_train, X_test, y_train, y_test = train_test_split(X_new, y, test_size=0.2, random_state=42)

# Train model
model = LinearRegression()
model.fit(X_train, y_train)

# Make predictions
y_pred = model.predict(X_test)

# Evaluate model
mse = mean_squared_error(y_test, y_pred)
print(f"Mean Squared Error: {mse}")
```

**Model Evaluation Example:**
```python
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score, roc_auc_score

# Load dataset
data = load_iris()
X = data.data
y = data.target

# Split dataset
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Train model
model = LogisticRegression(max_iter=1000)
model.fit(X_train, y_train)

# Make predictions
y_pred = model.predict(X_test)

# Evaluate model
accuracy = accuracy_score(y_test, y_pred)
precision = precision_score(y_test, y_pred, average='weighted')
recall = recall_score(y_test, y_pred, average='weighted')
f1 = f1_score(y_test, y_pred, average='weighted')
roc_auc = roc_auc_score(y_test, model.predict_proba(X_test), multi_class='ovr')

print(f"Accuracy: {accuracy}")
print(f"Precision: {precision}")
print(f"Recall: {recall}")
print(f"F1 Score: {f1}")
print(f"ROC-AUC Score: {roc_auc}")
```

**Cross-Validation Example:**
```python
from sklearn.datasets import load_iris
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import cross_val_score

# Load dataset
data = load_iris()
X = data.data
y = data.target

# Initialize model
model = RandomForestClassifier()

# Perform 5-fold cross-validation
scores = cross_val_score(model, X, y, cv=5, scoring='accuracy')

print(f"Cross-Validation Scores: {scores}")
print(f"Mean Score: {scores.mean()}")
```

### Assignment Questions

**Question 1: Write a Python program to demonstrate feature selection and model evaluation.**
```python
from sklearn.datasets import load_boston
from sklearn.feature_selection import SelectKBest, f_regression
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

# Load dataset
data = load_boston()
X = data.data
y = data.target

# Select top 5 features
selector = SelectKBest(score_func=f_regression, k=5)
X_new = selector.fit_transform(X, y)

# Split dataset
X_train, X_test, y_train, y_test = train_test_split(X_new, y, test_size=0.2, random_state=42)

# Train model
model = LinearRegression()
model.fit(X_train, y_train)

# Make predictions
y_pred = model.predict(X_test)

# Evaluate model
mse = mean_squared_error(y_test, y_pred)
print(f"Mean Squared Error: {mse}")
```

**Question 2: Create a Python program to perform cross-validation on a machine learning model.**
```python
from sklearn.datasets import load_iris
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import cross_val_score

# Load dataset
data = load_iris()
X = data.data
y = data.target

# Initialize model
model = RandomForestClassifier()

# Perform 5-fold cross-validation
scores = cross_val_score(model, X, y, cv=5, scoring='accuracy')

print(f"Cross-Validation Scores: {scores}")
print(f"Mean Score: {scores.mean()}")
```

### IPython Notebook Example

Create a new Jupyter Notebook and include the following content:

```markdown
# Day 8: Advanced Machine Learning Concepts

## Advanced ML Techniques: Feature Selection, Model Evaluation, Cross-Validation

### Feature Selection
- **Definition:** Selecting the most important features that contribute to the predictive power of the model.
- **Techniques:**
  1. **Filter Methods:** Statistical techniques to score the relevance of features.
  2. **Wrapper Methods:** Use a subset of features to train a model and evaluate performance.
  3. **Embedded Methods:** Feature selection as part of the model training process.
- **Example:**
```python
from sklearn.datasets import load_boston
from sklearn.feature_selection import SelectKBest, f_regression

# Load dataset
data = load_boston()
X = data.data
y = data.target

# Select top 5 features
selector = SelectKBest(score_func=f_regression, k=5)
X_new = selector.fit_transform(X, y)

print(f"Selected Features Shape: {X_new.shape}")
```

### Model Evaluation
- **Definition:** Assessing the performance of a machine learning model.
- **Metrics:**
  1. **Accuracy:** Proportion of correctly predicted instances.
  2. **Precision:** Proportion of true positive instances among the predicted positive instances.
  3. **Recall:** Proportion of true positive instances among the actual positive instances.
  4. **F1 Score:** Harmonic mean of precision and recall.
  5. **ROC-AUC Score:** Area under the receiver operating characteristic curve.
- **Example:**
```python
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score, roc_auc_score

# Load dataset
data = load_boston()
X = data.data
y = data.target

# Split dataset
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Train model
model = LogisticRegression(max_iter=1000)
model.fit(X_train, y_train)

# Make predictions
y_pred = model.predict(X_test)

# Evaluate model
accuracy = accuracy_score(y_test, y_pred)
precision = precision_score(y_test, y_pred, average='weighted')
recall = recall_score(y_test, y_pred, average='weighted')
f1 = f1_score(y_test, y_pred, average='weighted')
roc_auc = roc_auc_score(y_test, model.predict_proba(X_test), multi_class='ovr')

print(f"Accuracy: {accuracy}")
print(f"Precision: {precision}")
print(f"Recall: {recall}")
print(f"F1 Score: {f1}")
print(f"ROC-AUC Score: {roc_auc}")
```

### Cross-Validation
- **Definition:** Assessing the generalizability of a machine learning model by splitting the dataset into multiple folds and training/testing the model on different subsets of the data.
- **Method:** k-fold cross-validation.
- **Example:**
```python
from sklearn.model_selection import cross_val_score
from sklearn.ensemble import RandomForestClassifier

# Load dataset
data = load_boston()
X = data.data
y = data.target

# Initialize model
model = RandomForestClassifier()

# Perform 5-fold cross-validation
scores = cross_val_score(model, X, y, cv=5, scoring='accuracy')

print(f"Cross-Validation Scores: {scores}")
print(f"Mean Score: {scores.mean()}")
```

## Practical Session: Implementing Advanced ML Techniques in Python

### Feature Selection Example
```python
from sklearn.datasets import load_boston
from sklearn.feature_selection import SelectKBest, f_regression
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

# Load dataset
data = load_boston()
X = data.data
y = data.target

# Select top 5 features
selector = SelectKBest(score_func=f_regression, k=5)
X_new = selector.fit_transform(X, y)

# Split dataset
X_train, X_test, y_train, y_test = train_test_split(X_new, y, test_size=0.2, random_state=42)

# Train model
model = LinearRegression()
model.fit(X_train, y_train)

# Make predictions
y_pred = model.predict(X_test)

# Evaluate model
mse = mean_squared_error(y_test, y_pred)
print(f"Mean Squared Error: {mse}")
```

### Model Evaluation Example
```python
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score, roc_auc_score

# Load dataset
data = load_iris()
X = data.data
y = data.target

# Split dataset
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Train model
model = LogisticRegression(max_iter=1000)
model.fit(X_train, y_train)

# Make predictions
y_pred = model.predict(X_test)

# Evaluate model
accuracy = accuracy_score(y_test, y_pred)
precision = precision_score(y_test, y_pred, average='weighted')
recall = recall_score(y_test, y_pred, average='weighted')
f1 = f1_score(y_test, y_pred, average='weighted')
roc_auc = roc_auc_score(y_test, model.predict_proba(X_test), multi_class='ovr')

print(f"Accuracy: {accuracy}")
print(f"Precision: {precision}")
print(f"Recall: {recall}")
print(f"F1 Score: {f1}")
print(f"ROC-AUC Score: {roc_auc}")
```

### Cross-Validation Example
```python
from sklearn.datasets import load_iris
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import cross_val_score

# Load dataset
data = load_iris()
X = data.data
y = data.target

# Initialize model
model = RandomForestClassifier()

# Perform 5-fold cross-validation
scores = cross_val_score(model, X, y, cv=5, scoring='accuracy')

print(f"Cross-Validation Scores: {scores}")
print(f"Mean Score: {scores.mean()}")
```

## Assignments
1. Write a Python program to demonstrate feature selection and model evaluation.
```python
from sklearn.datasets import load_boston
from sklearn.feature_selection import SelectKBest, f_regression
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

# Load dataset
data = load_boston()
X = data.data
y = data.target

# Select top 5 features
selector = SelectKBest(score_func=f_regression, k=5)
X_new = selector.fit_transform(X, y)

# Split dataset
X_train, X_test, y_train, y_test = train_test_split(X_new, y, test_size=0.2, random_state=42)

# Train model
model = LinearRegression()
model.fit(X_train, y_train)

# Make predictions
y_pred = model.predict(X_test)

# Evaluate model
mse = mean_squared_error(y_test, y_pred)
print(f"Mean Squared Error: {mse}")
```

2. Create a Python program to perform cross-validation on a machine learning model.
```python
from sklearn.datasets import load_iris
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import cross_val_score

# Load dataset
data = load_iris()
X = data.data
y = data.target

# Initialize model
model = RandomForestClassifier()

# Perform 5-fold cross-validation
scores = cross_val_score(model, X, y, cv=5, scoring='accuracy')

print(f"Cross-Validation Scores: {scores}")
print(f"Mean Score: {scores.mean()}")
```
```

In the code cells of the notebook, include the Python code provided above for each section.
