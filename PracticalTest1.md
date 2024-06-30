### Practical Test Questions for First 5 Days

**Test 1: Day 1 to Day 5**

**Question 1: Python Programming Basics**

**Task:**
Write a Python program to check if a given string is a palindrome. A palindrome is a word, phrase, number, or other sequences of characters that reads the same forward and backward (ignoring spaces, punctuation, and capitalization).

**Answer:**
```python
def is_palindrome(s):
    # Remove spaces and convert to lowercase
    s = ''.join(e for e in s if e.isalnum()).lower()
    return s == s[::-1]

# Test the function
test_string = "A man, a plan, a canal, Panama"
print(f"'{test_string}' is a palindrome: {is_palindrome(test_string)}")
```

**Explanation:**
- The function `is_palindrome` removes non-alphanumeric characters and converts the string to lowercase.
- It then checks if the string is equal to its reverse using slicing (`s[::-1]`).

**Question 2: SQL and Database Operations**

**Task:**
Create a Python program to connect to a MySQL database, create a table named `Employees`, insert records into the table, and retrieve and display all records from the table.

**Answer:**
```python
import mysql.connector

# Connect to the MySQL database
conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="your_password",
    database="test_db"
)

cursor = conn.cursor()

# Create table
cursor.execute("""
CREATE TABLE IF NOT EXISTS Employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    position VARCHAR(255),
    salary FLOAT
)
""")

# Insert records
cursor.execute("INSERT INTO Employees (name, position, salary) VALUES (%s, %s, %s)", ("John Doe", "Manager", 80000))
cursor.execute("INSERT INTO Employees (name, position, salary) VALUES (%s, %s, %s)", ("Jane Smith", "Developer", 60000))
conn.commit()

# Retrieve and display records
cursor.execute("SELECT * FROM Employees")
rows = cursor.fetchall()

for row in rows:
    print(row)

# Close the connection
cursor.close()
conn.close()
```

**Explanation:**
- The program connects to the MySQL database using `mysql.connector`.
- It creates the `Employees` table if it does not already exist.
- It inserts two records into the table.
- It retrieves and prints all records from the `Employees` table.

---
