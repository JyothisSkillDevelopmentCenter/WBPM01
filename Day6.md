### Day 6: Introduction to Machine Learning

#### Machine Learning Introduction: Differences between ML and Traditional Programming

**Machine Learning (ML):**
Machine Learning is a subset of artificial intelligence (AI) that involves training algorithms to make predictions or decisions based on data. Instead of being explicitly programmed to perform a task, ML models learn from historical data and improve their performance over time.

**Traditional Programming:**
In traditional programming, developers write explicit instructions (rules) for the computer to follow. The program's output is determined by these predefined rules.

**Key Differences:**
1. **Rule-Based vs. Data-Driven:**
   - **Traditional Programming:** Rules are explicitly coded by programmers.
   - **Machine Learning:** Models learn patterns and rules from data.

2. **Adaptability:**
   - **Traditional Programming:** Limited adaptability; changes require rewriting code.
   - **Machine Learning:** Models can adapt to new data and improve accuracy without changing the code.

3. **Handling Complexity:**
   - **Traditional Programming:** Difficult to handle complex patterns and large datasets.
   - **Machine Learning:** Capable of handling complex relationships and large amounts of data efficiently.

4. **Use Cases:**
   - **Traditional Programming:** Simple and deterministic tasks (e.g., calculators, basic automation).
   - **Machine Learning:** Complex and probabilistic tasks (e.g., image recognition, natural language processing).

**Example:**
- **Traditional Programming:** Writing rules to identify spam emails.
- **Machine Learning:** Training a model on a dataset of spam and non-spam emails to identify spam emails.

#### ML Concepts: Supervised and Unsupervised Learning, Regression, Classification, Clustering

**Supervised Learning:**
Supervised learning involves training a model on a labeled dataset, where the input data is paired with the correct output. The model learns to map inputs to outputs and can make predictions on new, unseen data.
- **Examples:** Linear regression, logistic regression, decision trees, support vector machines.
- **Use Cases:** Predicting house prices, classifying emails as spam or not spam.

**Unsupervised Learning:**
Unsupervised learning involves training a model on an unlabeled dataset. The model tries to find patterns and relationships in the data without any explicit instructions on what to predict.
- **Examples:** Clustering, dimensionality reduction.
- **Use Cases:** Customer segmentation, anomaly detection.

**Regression:**
Regression is a type of supervised learning used to predict continuous values.
- **Example:** Predicting house prices based on features like size, location, and number of bedrooms.
- **Algorithm:** Linear regression.

**Classification:**
Classification is a type of supervised learning used to predict categorical labels.
- **Example:** Classifying emails as spam or not spam.
- **Algorithm:** Logistic regression, decision trees.

**Clustering:**
Clustering is a type of unsupervised learning used to group similar data points together.
- **Example:** Grouping customers based on purchasing behavior.
- **Algorithm:** K-means clustering.

**Examples of ML Algorithms:**
1. **Linear Regression (Supervised Learning - Regression):**
   - Used to predict a continuous target variable.
   - **Example:** Predicting house prices.
2. **Logistic Regression (Supervised Learning - Classification):**
   - Used to predict binary outcomes.
   - **Example:** Classifying emails as spam or not spam.
3. **K-Means Clustering (Unsupervised Learning - Clustering):**
   - Used to group similar data points into clusters.
   - **Example:** Customer segmentation.

#### Practical Session: Simple ML Programs using Python

**Setting Up the Environment:**
1. **Install Necessary Libraries:**
   - Use pip to install libraries like `numpy`, `pandas`, `scikit-learn`, and `matplotlib`:
     ```sh
     pip install numpy pandas scikit-learn matplotlib
     ```

**Linear Regression Example:**
```python
import numpy as np
import pandas as pd
from sklearn.linear_model import LinearRegression
import matplotlib.pyplot as plt

# Sample dataset
data = {
    'Size': [1500, 1600, 1700, 1800, 1900],
    'Price': [300000, 320000, 340000, 360000, 380000]
}
df = pd.DataFrame(data)

# Feature and target variable
X = df[['Size']]
y = df['Price']

# Creating and training the model
model = LinearRegression()
model.fit(X, y)

# Making predictions
predicted_prices = model.predict(X)

# Plotting the results
plt.scatter(X, y, color='blue', label='Actual Prices')
plt.plot(X, predicted_prices, color='red', label='Predicted Prices')
plt.xlabel('Size (sq ft)')
plt.ylabel('Price ($)')
plt.legend()
plt.show()
```

**Logistic Regression Example:**
```python
import numpy as np
import pandas as pd
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# Sample dataset
data = {
    'Hours_Studied': [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
    'Passed': [0, 0, 0, 0, 1, 1, 1, 1, 1, 1]
}
df = pd.DataFrame(data)

# Feature and target variable
X = df[['Hours_Studied']]
y = df['Passed']

# Splitting the dataset
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Creating and training the model
model = LogisticRegression()
model.fit(X_train, y_train)

# Making predictions
y_pred = model.predict(X_test)

# Evaluating the model
accuracy = accuracy_score(y_test, y_pred)
print(f'Accuracy: {accuracy}')
```

**K-Means Clustering Example:**
```python
import numpy as np
import pandas as pd
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt

# Sample dataset
data = {
    'Annual Income (k$)': [15, 16, 17, 18, 19, 35, 36, 37, 38, 39],
    'Spending Score (1-100)': [39, 81, 6, 77, 40, 76, 6, 94, 3, 72]
}
df = pd.DataFrame(data)

# Creating and training the model
kmeans = KMeans(n_clusters=2, random_state=42)
df['Cluster'] = kmeans.fit_predict(df)

# Plotting the results
plt.scatter(df['Annual Income (k$)'], df['Spending Score (1-100)'], c=df['Cluster'], cmap='viridis')
plt.xlabel('Annual Income (k$)')
plt.ylabel('Spending Score (1-100)')
plt.title('Customer Segmentation')
plt.show()
```

### Assignment Questions

**Question 1: Write a Python program to demonstrate a simple linear regression model using a sample dataset.**
```python
import numpy as np
import pandas as pd
from sklearn.linear_model import LinearRegression
import matplotlib.pyplot as plt

# Sample dataset
data = {
    'Size': [1500, 1600, 1700, 1800, 1900],
    'Price': [300000, 320000, 340000, 360000, 380000]
}
df = pd.DataFrame(data)

# Feature and target variable
X = df[['Size']]
y = df['Price']

# Creating and training the model
model = LinearRegression()
model.fit(X, y)

# Making predictions
predicted_prices = model.predict(X)

# Plotting the results
plt.scatter(X, y, color='blue', label='Actual Prices')
plt.plot(X, predicted_prices, color='red', label='Predicted Prices')
plt.xlabel('Size (sq ft)')
plt.ylabel('Price ($)')
plt.legend()
plt.show()
```

**Question 2: Create a Python program to classify data using a simple classification algorithm.**
```python
import numpy as np
import pandas as pd
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# Sample dataset
data = {
    'Hours_Studied': [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
    'Passed': [0, 0, 0, 0, 1, 1, 1, 1, 1, 1]
}
df = pd.DataFrame(data)

# Feature and target variable
X = df[['Hours_Studied']]
y = df['Passed']

# Splitting the dataset
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Creating and training the model
model = LogisticRegression()
model.fit(X_train, y_train)

# Making predictions
y_pred = model.predict(X_test)

# Evaluating the model
accuracy = accuracy_score(y_test, y_pred)
print(f'Accuracy: {accuracy}')
```

### IPython Notebook Example

Create a new Jupyter Notebook and include the following content:

```markdown
# Day 6: Introduction to Machine Learning

## Machine Learning Introduction: Differences between ML and Traditional Programming

### Machine Learning (ML)
- **Definition:** Subset of AI that involves training algorithms to make predictions or decisions based on data.
- **Learning Process:** Models learn from historical data and improve performance over time .

### Traditional Programming
- **Rule-Based:** Developers write explicit instructions for the computer to follow.
- **Deterministic:** Output is determined by predefined rules.

### Key Differences
1. **Rule-Based vs. Data-Driven:**
   - **Traditional Programming:** Rules are explicitly coded.
   - **Machine Learning:** Models learn patterns from data.
2. **Adaptability:**
   - **Traditional Programming:** Limited adaptability.
   - **Machine Learning:** Models adapt to new data.
3. **Handling Complexity:**
   - **Traditional Programming:** Handles simple tasks.
   - **Machine Learning:** Handles complex tasks.
4. **Use Cases:**
   - **Traditional Programming:** Simple tasks (e.g., calculators).
   - **Machine Learning:** Complex tasks (e.g., image recognition).

## ML Concepts: Supervised and Unsupervised Learning, Regression, Classification, Clustering

### Supervised Learning
- **Definition:** Training a model on a labeled dataset.
- **Examples:** Linear regression, logistic regression.
- **Use Cases:** Predicting house prices, classifying emails.

### Unsupervised Learning
- **Definition:** Training a model on an unlabeled dataset.
- **Examples:** Clustering, dimensionality reduction.
- **Use Cases:** Customer segmentation, anomaly detection.

### Regression
- **Definition:** Predicting continuous values.
- **Example:** Predicting house prices.
- **Algorithm:** Linear regression.

### Classification
- **Definition:** Predicting categorical labels.
- **Example:** Classifying emails.
- **Algorithm:** Logistic regression.

### Clustering
- **Definition:** Grouping similar data points.
- **Example:** Customer segmentation.
- **Algorithm:** K-means clustering.

## Practical Session: Simple ML Programs using Python

### Setting Up the Environment
1. **Install Necessary Libraries:**
   - Use pip to install libraries like `numpy`, `pandas`, `scikit-learn`, `matplotlib`:
     ```sh
     pip install numpy pandas scikit-learn matplotlib
     ```

### Linear Regression Example
```python
import numpy as np
import pandas as pd
from sklearn.linear_model import LinearRegression
import matplotlib.pyplot as plt

# Sample dataset
data = {
    'Size': [1500, 1600, 1700, 1800, 1900],
    'Price': [300000, 320000, 340000, 360000, 380000]
}
df = pd.DataFrame(data)

# Feature and target variable
X = df[['Size']]
y = df['Price']

# Creating and training the model
model = LinearRegression()
model.fit(X, y)

# Making predictions
predicted_prices = model.predict(X)

# Plotting the results
plt.scatter(X, y, color='blue', label='Actual Prices')
plt.plot(X, predicted_prices, color='red', label='Predicted Prices')
plt.xlabel('Size (sq ft)')
plt.ylabel('Price ($)')
plt.legend()
plt.show()
```

### Logistic Regression Example
```python
import numpy as np
import pandas as pd
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# Sample dataset
data = {
    'Hours_Studied': [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
    'Passed': [0, 0, 0, 0, 1, 1, 1, 1, 1, 1]
}
df = pd.DataFrame(data)

# Feature and target variable
X = df[['Hours_Studied']]
y = df['Passed']

# Splitting the dataset
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Creating and training the model
model = LogisticRegression()
model.fit(X_train, y_train)

# Making predictions
y_pred = model.predict(X_test)

# Evaluating the model
accuracy = accuracy_score(y_test, y_pred)
print(f'Accuracy: {accuracy}')
```

### K-Means Clustering Example
```python
import numpy as np
import pandas as pd
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt

# Sample dataset
data = {
    'Annual Income (k$)': [15, 16, 17, 18, 19, 35, 36, 37, 38, 39],
    'Spending Score (1-100)': [39, 81, 6, 77, 40, 76, 6, 94, 3, 72]
}
df = pd.DataFrame(data)

# Creating and training the model
kmeans = KMeans(n_clusters=2, random_state=42)
df['Cluster'] = kmeans.fit_predict(df)

# Plotting the results
plt.scatter(df['Annual Income (k$)'], df['Spending Score (1-100)'], c=df['Cluster'], cmap='viridis')
plt.xlabel('Annual Income (k$)')
plt.ylabel('Spending Score (1-100)')
plt.title('Customer Segmentation')
plt.show()
```

## Assignments
1. Write a Python program to demonstrate a simple linear regression model using a sample dataset.
```python
import numpy as np
import pandas as pd
from sklearn.linear_model import LinearRegression
import matplotlib.pyplot as plt

# Sample dataset
data = {
    'Size': [1500, 1600, 1700, 1800, 1900],
    'Price': [300000, 320000, 340000, 360000, 380000]
}
df = pd.DataFrame(data)

# Feature and target variable
X = df[['Size']]
y = df['Price']

# Creating and training the model
model = LinearRegression()
model.fit(X, y)

# Making predictions
predicted_prices = model.predict(X)

# Plotting the results
plt.scatter(X, y, color='blue', label='Actual Prices')
plt.plot(X, predicted_prices, color='red', label='Predicted Prices')
plt.xlabel('Size (sq ft)')
plt.ylabel('Price ($)')
plt.legend()
plt.show()
```

2. Create a Python program to classify data using a simple classification algorithm.
```python
import numpy as np
import pandas as pd
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# Sample dataset
data = {
    'Hours_Studied': [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
    'Passed': [0, 0, 0, 0, 1, 1, 1, 1, 1, 1]
}
df = pd.DataFrame(data)

# Feature and target variable
X = df[['Hours_Studied']]
y = df['Passed']

# Splitting the dataset
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Creating and training the model
model = LogisticRegression()
model.fit(X_train, y_train)

# Making predictions
y_pred = model.predict(X_test)

# Evaluating the model
accuracy = accuracy_score(y_test, y_pred)
print(f'Accuracy: {accuracy}')
```
```

In the code cells of the notebook, include the Python code provided above for each section.
