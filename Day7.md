### Day 7: Statistics for Machine Learning

#### Understanding Data: Mean, Median, Mode, Standard Deviation, Percentiles, Data Distribution

**Mean:**
The mean (average) is the sum of all values divided by the number of values.
**Formula:**
\[ \text{Mean} = \frac{\sum_{i=1}^{n} x_i}{n} \]
**Example:**
```python
data = [10, 20, 30, 40, 50]
mean = sum(data) / len(data)
print(f"Mean: {mean}")
```

**Median:**
The median is the middle value when the data is sorted in ascending or descending order. If the number of values is even, the median is the average of the two middle numbers.
**Example:**
```python
data = [10, 20, 30, 40, 50]
data.sort()
n = len(data)
if n % 2 == 0:
    median = (data[n//2 - 1] + data[n//2]) / 2
else:
    median = data[n//2]
print(f"Median: {median}")
```

**Mode:**
The mode is the value that appears most frequently in a dataset.
**Example:**
```python
from collections import Counter

data = [10, 20, 20, 30, 40, 50]
mode_data = Counter(data)
mode = mode_data.most_common(1)[0][0]
print(f"Mode: {mode}")
```

**Standard Deviation:**
Standard deviation measures the amount of variation or dispersion in a dataset.
**Formula:**
\[ \sigma = \sqrt{\frac{\sum_{i=1}^{n} (x_i - \mu)^2}{n}} \]
**Example:**
```python
import math

data = [10, 20, 30, 40, 50]
mean = sum(data) / len(data)
variance = sum((x - mean) ** 2 for x in data) / len(data)
std_dev = math.sqrt(variance)
print(f"Standard Deviation: {std_dev}")
```

**Percentiles:**
Percentiles indicate the value below which a given percentage of observations fall.
**Example:**
```python
import numpy as np

data = [10, 20, 30, 40, 50]
percentile_25 = np.percentile(data, 25)
percentile_50 = np.percentile(data, 50)  # This is the median
percentile_75 = np.percentile(data, 75)
print(f"25th Percentile: {percentile_25}")
print(f"50th Percentile (Median): {percentile_50}")
print(f"75th Percentile: {percentile_75}")
```

**Data Distribution:**
Data distribution describes the frequencies of values or ranges of values in a dataset. Common types of distributions include normal distribution, uniform distribution, and skewed distribution.

**Example of Normal Distribution:**
```python
import numpy as np
import matplotlib.pyplot as plt

data = np.random.normal(loc=50, scale=10, size=1000)
plt.hist(data, bins=30, edgecolor='black')
plt.title('Normal Distribution')
plt.xlabel('Value')
plt.ylabel('Frequency')
plt.show()
```

#### Practical Session: Statistical Analysis Using Python

**Setting Up the Environment:**
1. **Install Necessary Libraries:**
   - Use pip to install libraries like `numpy`, `pandas`, and `scipy`:
     ```sh
     pip install numpy pandas scipy matplotlib
     ```

**Calculating Mean, Median, and Mode:**
```python
import numpy as np
import pandas as pd
from scipy import stats

# Sample dataset
data = [10, 20, 30, 40, 50, 20, 20]

# Calculating mean
mean = np.mean(data)
print(f"Mean: {mean}")

# Calculating median
median = np.median(data)
print(f"Median: {median}")

# Calculating mode
mode = stats.mode(data)[0][0]
print(f"Mode: {mode}")
```

**Calculating Standard Deviation and Percentiles:**
```python
import numpy as np

# Sample dataset
data = [10, 20, 30, 40, 50, 20, 20]

# Calculating standard deviation
std_dev = np.std(data)
print(f"Standard Deviation: {std_dev}")

# Calculating percentiles
percentile_25 = np.percentile(data, 25)
percentile_50 = np.percentile(data, 50)  # This is the median
percentile_75 = np.percentile(data, 75)
print(f"25th Percentile: {percentile_25}")
print(f"50th Percentile (Median): {percentile_50}")
print(f"75th Percentile: {percentile_75}")
```

**Visualizing Data Distribution:**
```python
import numpy as np
import matplotlib.pyplot as plt

# Sample dataset
data = np.random.normal(loc=50, scale=10, size=1000)

# Plotting histogram
plt.hist(data, bins=30, edgecolor='black')
plt.title('Normal Distribution')
plt.xlabel('Value')
plt.ylabel('Frequency')
plt.show()
```

### Assignment Questions

**Question 1: Write a Python program to calculate the mean, median, and mode of a dataset.**
```python
import numpy as np
from scipy import stats

# Sample dataset
data = [15, 20, 35, 40, 50, 50, 50, 60, 70, 80, 80, 95]

# Calculating mean
mean = np.mean(data)
print(f"Mean: {mean}")

# Calculating median
median = np.median(data)
print(f"Median: {median}")

# Calculating mode
mode = stats.mode(data)[0][0]
print(f"Mode: {mode}")
```

**Question 2: Create a Python program to calculate standard deviation and percentiles of a dataset.**
```python
import numpy as np

# Sample dataset
data = [15, 20, 35, 40, 50, 50, 50, 60, 70, 80, 80, 95]

# Calculating standard deviation
std_dev = np.std(data)
print(f"Standard Deviation: {std_dev}")

# Calculating percentiles
percentile_25 = np.percentile(data, 25)
percentile_50 = np.percentile(data, 50)  # This is the median
percentile_75 = np.percentile(data, 75)
print(f"25th Percentile: {percentile_25}")
print(f"50th Percentile (Median): {percentile_50}")
print(f"75th Percentile: {percentile_75}")
```

### IPython Notebook Example

Create a new Jupyter Notebook and include the following content:

```markdown
# Day 7: Statistics for Machine Learning

## Understanding Data: Mean, Median, Mode, Standard Deviation, Percentiles, Data Distribution

### Mean
- **Definition:** The average value of a dataset.
- **Formula:** \[ \text{Mean} = \frac{\sum_{i=1}^{n} x_i}{n} \]
- **Example:**
```python
data = [10, 20, 30, 40, 50]
mean = sum(data) / len(data)
print(f"Mean: {mean}")
```

### Median
- **Definition:** The middle value of a sorted dataset.
- **Example:**
```python
data = [10, 20, 30, 40, 50]
data.sort()
n = len(data)
if n % 2 == 0:
    median = (data[n//2 - 1] + data[n//2]) / 2
else:
    median = data[n//2]
print(f"Median: {median}")
```

### Mode
- **Definition:** The most frequent value in a dataset.
- **Example:**
```python
from collections import Counter

data = [10, 20, 20, 30, 40, 50]
mode_data = Counter(data)
mode = mode_data.most_common(1)[0][0]
print(f"Mode: {mode}")
```

### Standard Deviation
- **Definition:** Measures the amount of variation in a dataset.
- **Formula:** \[ \sigma = \sqrt{\frac{\sum_{i=1}^{n} (x_i - \mu)^2}{n}} \]
- **Example:**
```python
import math

data = [10, 20, 30, 40, 50]
mean = sum(data) / len(data)
variance = sum((x - mean) ** 2 for x in data) / len(data)
std_dev = math.sqrt(variance)
print(f"Standard Deviation: {std_dev}")
```

### Percentiles
- **Definition:** Indicates the value below which a given percentage of observations fall.
- **Example:**
```python
import numpy as np

data = [10, 20, 30, 40, 50]
percentile_25 = np.percentile(data, 25)
percentile_50 = np.percentile(data, 50)  # This is the median
percentile_75 = np.percentile(data, 75)
print(f"25th Percentile: {percentile_25}")
print(f"50th Percentile (Median): {percentile_50}")
print(f"75th Percentile: {percentile_75}")
```

### Data Distribution
- **Definition:** Describes the frequencies of values in a dataset.
- **Example of Normal Distribution:**
```python
import numpy as np
import matplotlib.pyplot as plt

data = np.random.normal(loc=50, scale=10, size=1000)
plt.hist(data, bins=30, edgecolor='black')
plt.title('Normal Distribution')
plt.xlabel('Value')
plt.ylabel('Frequency')
plt.show()
```

## Practical Session: Statistical Analysis Using Python

### Calculating Mean, Median, and Mode
```python
import numpy as np
import pandas as pd
from scipy import stats

# Sample dataset
data = [10, 20, 30, 40, 50, 20, 20]

# Calculating mean
mean = np.mean(data)
print(f"Mean: {mean}")

# Calculating median
median = np.median(data)
print(f"Median: {median}")

# Calculating mode
mode = stats.mode(data)[0][0]
print(f"Mode: {mode}")
```

### Calculating Standard Deviation and Percentiles
```python
import numpy as np

# Sample dataset
data = [10, 20, 30, 40, 50, 20, 20]

# Calculating standard deviation
std_dev = np.std(data)
print(f"Standard Deviation: {std_dev}")

# Calculating percentiles
percentile_25 = np.percentile(data, 25)
percentile_50 = np.percentile(data, 50)  # This is the median
percentile_75 = np.percentile(data, 75)
print(f"25th Percentile: {percentile_25}")
print(f"50th Percentile (Median): {percentile_50}")
print(f"75th Percentile: {percentile_75}")
```

### Visualizing Data Distribution
```python
import numpy as np
import matplotlib.pyplot as plt

# Sample dataset
data = np.random.normal(loc=50, scale=10, size=1000)

# Plotting histogram
plt.hist(data, bins=30, edgecolor='black')
plt.title('Normal Distribution')
plt.xlabel('Value')
plt.ylabel('Frequency')
plt.show()
```

## Assignments
1. Write a Python program to calculate the mean, median, and mode of a dataset.
```python
import numpy as np
from scipy import stats

# Sample dataset
data = [15, 20, 35, 40, 50, 50, 50, 60, 70, 80, 80, 95]

# Calculating mean
mean = np.mean(data)
print(f"Mean: {mean}")

# Calculating median
median = np.median(data)
print(f"Median: {median}")

# Calculating mode
mode = stats.mode(data)[0][0]
print(f"Mode: {mode}")
```

2. Create a Python program to calculate standard deviation and percentiles of a dataset.
```python
import numpy as np

# Sample dataset
data = [15, 20, 35, 40, 50, 50, 50, 60, 70, 80, 80, 95]

# Calculating standard deviation
std_dev = np.std(data)
print(f"Standard Deviation: {std_dev}")

# Calculating percentiles
percentile_25 = np.percentile(data, 25)
percentile_50 = np.percentile(data, 50)  # This is the median
percentile_75 = np.percentile(data, 75)
print(f"25th Percentile: {percentile_25}")
print(f"50th Percentile (Median): {percentile_50}")
print(f"75th Percentile: {percentile_75}")
```
```

In the code cells of the notebook, include the Python code provided above for each section.
