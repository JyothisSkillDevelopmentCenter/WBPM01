### Day 5: Advanced SQL and Data Operations

#### Advanced SQL: Update, Delete, Order By, Where, And, Or, Not, Min, Max, Count, Top, Sum, Like, In, Between, Joins

**Update Data:**
The UPDATE statement is used to modify existing records in a table.
**Syntax:**
```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```
**Example:**
```sql
UPDATE students
SET age = 19
WHERE name = 'John Doe';
```

**Delete Data:**
The DELETE statement is used to remove existing records from a table.
**Syntax:**
```sql
DELETE FROM table_name
WHERE condition;
```
**Example:**
```sql
DELETE FROM students
WHERE name = 'John Doe';
```

**Order By:**
The ORDER BY keyword is used to sort the result set in ascending or descending order.
**Syntax:**
```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column1 ASC|DESC;
```
**Example:**
```sql
SELECT * FROM students
ORDER BY age DESC;
```

**Where Clause:**
The WHERE clause is used to filter records that meet a certain condition.
**Syntax:**
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```
**Example:**
```sql
SELECT * FROM students
WHERE age > 18;
```

**Logical Operators (AND, OR, NOT):**
These operators are used to combine multiple conditions in a WHERE clause.
**Example:**
```sql
SELECT * FROM students
WHERE age > 18 AND grade = 'A';
```

**Aggregate Functions (MIN, MAX, COUNT, SUM):**
Aggregate functions perform calculations on a set of values and return a single value.
**Examples:**
```sql
SELECT MIN(age) FROM students;
SELECT MAX(age) FROM students;
SELECT COUNT(*) FROM students;
SELECT SUM(age) FROM students;
```

**LIKE Operator:**
The LIKE operator is used to search for a specified pattern in a column.
**Syntax:**
```sql
SELECT column1, column2, ...
FROM table_name
WHERE columnN LIKE pattern;
```
**Example:**
```sql
SELECT * FROM students
WHERE name LIKE 'J%';
```

**IN Operator:**
The IN operator allows you to specify multiple values in a WHERE clause.
**Syntax:**
```sql
SELECT column1, column2, ...
FROM table_name
WHERE columnN IN (value1, value2, ...);
```
**Example:**
```sql
SELECT * FROM students
WHERE grade IN ('A', 'B');
```

**BETWEEN Operator:**
The BETWEEN operator selects values within a given range.
**Syntax:**
```sql
SELECT column1, column2, ...
FROM table_name
WHERE columnN BETWEEN value1 AND value2;
```
**Example:**
```sql
SELECT * FROM students
WHERE age BETWEEN 18 AND 22;
```

**Joins (INNER, LEFT, RIGHT, FULL):**
Joins are used to combine rows from two or more tables based on a related column.
**Examples:**
```sql
-- Inner Join
SELECT students.name, courses.course_name
FROM students
INNER JOIN courses ON students.id = courses.student_id;

-- Left Join
SELECT students.name, courses.course_name
FROM students
LEFT JOIN courses ON students.id = courses.student_id;

-- Right Join
SELECT students.name, courses.course_name
FROM students
RIGHT JOIN courses ON students.id = courses.student_id;

-- Full Join
SELECT students.name, courses.course_name
FROM students
FULL JOIN courses ON students.id = courses.student_id;
```

#### Practical Session: Advanced SQL Queries and Data Manipulation

**Connecting to MySQL:**
```python
import mysql.connector

# Establishing connection
conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="your_password",
    database="school"
)

# Creating a cursor object
cursor = conn.cursor()
```

**Updating Data:**
```python
# Updating data in the students table
cursor.execute("""
UPDATE students
SET age = %s
WHERE name = %s
""", (21, "Alice"))
conn.commit()
```

**Deleting Data:**
```python
# Deleting data from the students table
cursor.execute("DELETE FROM students WHERE name = %s", ("Alice",))
conn.commit()
```

**Ordering Data:**
```python
# Selecting and ordering data
cursor.execute("SELECT * FROM students ORDER BY age DESC")
rows = cursor.fetchall()
for row in rows:
    print(row)
```

**Filtering Data with WHERE:**
```python
# Filtering data using WHERE clause
cursor.execute("SELECT * FROM students WHERE age > 18")
rows = cursor.fetchall()
for row in rows:
    print(row)
```

**Using Logical Operators:**
```python
# Using logical operators
cursor.execute("SELECT * FROM students WHERE age > 18 AND grade = 'A'")
rows = cursor.fetchall()
for row in rows:
    print(row)
```

**Using Aggregate Functions:**
```python
# Using aggregate functions
cursor.execute("SELECT MIN(age) FROM students")
min_age = cursor.fetchone()[0]
print(f"Minimum age: {min_age}")

cursor.execute("SELECT MAX(age) FROM students")
max_age = cursor.fetchone()[0]
print(f"Maximum age: {max_age}")

cursor.execute("SELECT COUNT(*) FROM students")
count = cursor.fetchone()[0]
print(f"Number of students: {count}")

cursor.execute("SELECT SUM(age) FROM students")
total_age = cursor.fetchone()[0]
print(f"Total age: {total_age}")
```

**Using LIKE Operator:**
```python
# Using LIKE operator
cursor.execute("SELECT * FROM students WHERE name LIKE 'J%'")
rows = cursor.fetchall()
for row in rows:
    print(row)
```

**Using IN Operator:**
```python
# Using IN operator
cursor.execute("SELECT * FROM students WHERE grade IN ('A', 'B')")
rows = cursor.fetchall()
for row in rows:
    print(row)
```

**Using BETWEEN Operator:**
```python
# Using BETWEEN operator
cursor.execute("SELECT * FROM students WHERE age BETWEEN 18 AND 22")
rows = cursor.fetchall()
for row in rows:
    print(row)
```

**Using Joins:**
```python
# Creating another table for demonstration
cursor.execute("""
CREATE TABLE IF NOT EXISTS courses (
    course_id INT AUTO_INCREMENT PRIMARY KEY,
    course_name VARCHAR(100) NOT NULL,
    student_id INT,
    FOREIGN KEY (student_id) REFERENCES students(id)
)
""")
conn.commit()

# Inserting data into courses table
cursor.execute("""
INSERT INTO courses (course_name, student_id)
VALUES (%s, %s)
""", ("Mathematics", 1))
conn.commit()

# Using INNER JOIN
cursor.execute("""
SELECT students.name, courses.course_name
FROM students
INNER JOIN courses ON students.id = courses.student_id
""")
rows = cursor.fetchall()
for row in rows:
    print(row)
```

### Assignment Questions

**Question 1: Write a Python program to update and delete records in a MySQL table.**
```python
import mysql.connector

# Establishing connection
conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="your_password",
    database="testdb"
)

# Creating a cursor object
cursor = conn.cursor()

# Updating data in the employees table
cursor.execute("""
UPDATE employees
SET position = %s, salary = %s
WHERE name = %s
""", ("Senior Software Engineer", 85000.00, "John Doe"))
conn.commit()

# Deleting data from the employees table
cursor.execute("DELETE FROM employees WHERE name = %s", ("John Doe",))
conn.commit()

# Closing the connection
conn.close()
```

**Question 2: Create a program to demonstrate the use of aggregate functions and joins in SQL.**
```python
import mysql.connector

# Establishing connection
conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="your_password",
    database="testdb"
)

# Creating a cursor object
cursor = conn.cursor()

# Using aggregate functions
cursor.execute("SELECT MIN(salary) FROM employees")
min_salary = cursor.fetchone()[0]
print(f"Minimum salary: {min_salary}")

cursor.execute("SELECT MAX(salary) FROM employees")
max_salary = cursor.fetchone()[0]
print(f"Maximum salary: {max_salary}")

cursor.execute("SELECT COUNT(*) FROM employees")
employee_count = cursor.fetchone()[0]
print(f"Number of employees: {employee_count}")

cursor.execute("SELECT SUM(salary) FROM employees")
total_salary = cursor.fetchone()[0]
print(f"Total salary: {total_salary}")

# Creating another table for demonstration
cursor.execute("""
CREATE TABLE IF NOT EXISTS departments (
    department_id INT AUTO_INCREMENT PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL,
    employee_id INT,
    FOREIGN KEY (employee_id) REFERENCES employees(id)
)
""")
conn.commit()

# Inserting data into departments table
cursor.execute("""
INSERT INTO departments (department_name, employee_id)
VALUES (%s, %s)
""", ("IT", 1))
conn.commit()

# Using INNER JOIN
cursor.execute("""
SELECT employees.name, departments.department_name
FROM employees
INNER JOIN departments ON employees.id = departments.employee_id
""")
rows = cursor.fetchall()
for row in rows:
    print(row)

# Closing the connection
conn.close()
```

### IPython Notebook Example

Create a new Jupyter Notebook and include the following content:

```markdown
# Day 5: Advanced SQL and Data Operations

## Advanced SQL: Update, Delete, Order By , Where, And, Or, Not, Min, Max, Count, Top, Sum, Like, In, Between, Joins

### Update Data
- **Syntax:**
```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```
- **Example:**
```sql
UPDATE students
SET age = 19
WHERE name = 'John Doe';
```

### Delete Data
- **Syntax:**
```sql
DELETE FROM table_name
WHERE condition;
```
- **Example:**
```sql
DELETE FROM students
WHERE name = 'John Doe';
```

### Order By
- **Syntax:**
```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column1 ASC|DESC;
```
- **Example:**
```sql
SELECT * FROM students
ORDER BY age DESC;
```

### Where Clause
- **Syntax:**
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```
- **Example:**
```sql
SELECT * FROM students
WHERE age > 18;
```

### Logical Operators (AND, OR, NOT)
- **Example:**
```sql
SELECT * FROM students
WHERE age > 18 AND grade = 'A';
```

### Aggregate Functions (MIN, MAX, COUNT, SUM)
- **Examples:**
```sql
SELECT MIN(age) FROM students;
SELECT MAX(age) FROM students;
SELECT COUNT(*) FROM students;
SELECT SUM(age) FROM students;
```

### LIKE Operator
- **Syntax:**
```sql
SELECT column1, column2, ...
FROM table_name
WHERE columnN LIKE pattern;
```
- **Example:**
```sql
SELECT * FROM students
WHERE name LIKE 'J%';
```

### IN Operator
- **Syntax:**
```sql
SELECT column1, column2, ...
FROM table_name
WHERE columnN IN (value1, value2, ...);
```
- **Example:**
```sql
SELECT * FROM students
WHERE grade IN ('A', 'B');
```

### BETWEEN Operator
- **Syntax:**
```sql
SELECT column1, column2, ...
FROM table_name
WHERE columnN BETWEEN value1 AND value2;
```
- **Example:**
```sql
SELECT * FROM students
WHERE age BETWEEN 18 AND 22;
```

### Joins (INNER, LEFT, RIGHT, FULL)
- **Examples:**
```sql
-- Inner Join
SELECT students.name, courses.course_name
FROM students
INNER JOIN courses ON students.id = courses.student_id;

-- Left Join
SELECT students.name, courses.course_name
FROM students
LEFT JOIN courses ON students.id = courses.student_id;

-- Right Join
SELECT students.name, courses.course_name
FROM students
RIGHT JOIN courses ON students.id = courses.student_id;

-- Full Join
SELECT students.name, courses.course_name
FROM students
FULL JOIN courses ON students.id = courses.student_id;
```

## Practical Session: Advanced SQL Queries and Data Manipulation

1. **Connecting to MySQL:**
```python
import mysql.connector

# Establishing connection
conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="your_password",
    database="school"
)

# Creating a cursor object
cursor = conn.cursor()
```

2. **Updating Data:**
```python
# Updating data in the students table
cursor.execute("""
UPDATE students
SET age = %s
WHERE name = %s
""", (21, "Alice"))
conn.commit()
```

3. **Deleting Data:**
```python
# Deleting data from the students table
cursor.execute("DELETE FROM students WHERE name = %s", ("Alice",))
conn.commit()
```

4. **Ordering Data:**
```python
# Selecting and ordering data
cursor.execute("SELECT * FROM students ORDER BY age DESC")
rows = cursor.fetchall()
for row in rows:
    print(row)
```

5. **Filtering Data with WHERE:**
```python
# Filtering data using WHERE clause
cursor.execute("SELECT * FROM students WHERE age > 18")
rows = cursor.fetchall()
for row in rows:
    print(row)
```

6. **Using Logical Operators:**
```python
# Using logical operators
cursor.execute("SELECT * FROM students WHERE age > 18 AND grade = 'A'")
rows = cursor.fetchall()
for row in rows:
    print(row)
```

7. **Using Aggregate Functions:**
```python
# Using aggregate functions
cursor.execute("SELECT MIN(age) FROM students")
min_age = cursor.fetchone()[0]
print(f"Minimum age: {min_age}")

cursor.execute("SELECT MAX(age) FROM students")
max_age = cursor.fetchone()[0]
print(f"Maximum age: {max_age}")

cursor.execute("SELECT COUNT(*) FROM students")
count = cursor.fetchone()[0]
print(f"Number of students: {count}")

cursor.execute("SELECT SUM(age) FROM students")
total_age = cursor.fetchone()[0]
print(f"Total age: {total_age}")
```

8. **Using LIKE Operator:**
```python
# Using LIKE operator
cursor.execute("SELECT * FROM students WHERE name LIKE 'J%'")
rows = cursor.fetchall()
for row in rows:
    print(row)
```

9. **Using IN Operator:**
```python
# Using IN operator
cursor.execute("SELECT * FROM students WHERE grade IN ('A', 'B')")
rows = cursor.fetchall()
for row in rows:
    print(row)
```

10. **Using BETWEEN Operator:**
```python
# Using BETWEEN operator
cursor.execute("SELECT * FROM students WHERE age BETWEEN 18 AND 22")
rows = cursor.fetchall()
for row in rows:
    print(row)
```

11. **Using Joins:**
```python
# Creating another table for demonstration
cursor.execute("""
CREATE TABLE IF NOT EXISTS courses (
    course_id INT AUTO_INCREMENT PRIMARY KEY,
    course_name VARCHAR(100) NOT NULL,
    student_id INT,
    FOREIGN KEY (student_id) REFERENCES students(id)
)
""")
conn.commit()

# Inserting data into courses table
cursor.execute("""
INSERT INTO courses (course_name, student_id)
VALUES (%s, %s)
""", ("Mathematics", 1))
conn.commit()

# Using INNER JOIN
cursor.execute("""
SELECT students.name, courses.course_name
FROM students
INNER JOIN courses ON students.id = courses.student_id
""")
rows = cursor.fetchall()
for row in rows:
    print(row)
```

## Assignments
1. Write a Python program to update and delete records in a MySQL table.
```python
import mysql.connector

# Establishing connection
conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="your_password",
    database="testdb"
)

# Creating a cursor object
cursor = conn.cursor()

# Updating data in the employees table
cursor.execute("""
UPDATE employees
SET position = %s, salary = %s
WHERE name = %s
""", ("Senior Software Engineer", 85000.00, "John Doe"))
conn.commit()

# Deleting data from the employees table
cursor.execute("DELETE FROM employees WHERE name = %s", ("John Doe",))
conn.commit()

# Closing the connection
conn.close()
```

2. Create a program to demonstrate the use of aggregate functions and joins in SQL.
```python
import mysql.connector

# Establishing connection
conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="your_password",
    database="testdb"
)

# Creating a cursor object
cursor = conn.cursor()

# Using aggregate functions
cursor.execute("SELECT MIN(salary) FROM employees")
min_salary = cursor.fetchone()[0]
print(f"Minimum salary: {min_salary}")

cursor.execute("SELECT MAX(salary) FROM employees")
max_salary = cursor.fetchone()[0]
print(f"Maximum salary: {max_salary}")

cursor.execute("SELECT COUNT(*) FROM employees")
employee_count = cursor.fetchone()[0]
print(f"Number of employees: {employee_count}")

cursor.execute("SELECT SUM(salary) FROM employees")
total_salary = cursor.fetchone()[0]
print(f"Total salary: {total_salary}")

# Creating another table for demonstration
cursor.execute("""
CREATE TABLE IF NOT EXISTS departments (
    department_id INT AUTO_INCREMENT PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL,
    employee_id INT,
    FOREIGN KEY (employee_id) REFERENCES employees(id)
)
""")
conn.commit()

# Inserting data into departments table
cursor.execute("""
INSERT INTO departments (department_name, employee_id)
VALUES (%s, %s)
""", ("IT", 1))
conn.commit()

# Using INNER JOIN
cursor.execute("""
SELECT employees.name, departments.department_name
FROM employees
INNER JOIN departments ON employees.id = departments.employee_id
""")
rows = cursor.fetchall()
for row in rows:
    print(row)

# Closing the connection
conn.close()
```
```

In the code cells of the notebook, include the Python code provided above for each section.
