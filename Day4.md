### Day 4: Database in Python

#### Database Overview: Introduction to MySQL

**Introduction to MySQL:**
MySQL is an open-source relational database management system (RDBMS) that uses Structured Query Language (SQL) for database creation, management, and data manipulation. It is widely used in web applications and services due to its reliability, robustness, and ease of use.

**Key Features of MySQL:**
- Cross-platform support (Windows, macOS, Linux)
- High performance and scalability
- Strong security features
- Comprehensive data storage and retrieval capabilities

**Installing MySQL:**
1. **Download MySQL:** Go to the [MySQL website](https://dev.mysql.com/downloads/) and download the installer for your operating system.
2. **Install MySQL:** Follow the installation instructions for your operating system. During the installation, you will set up the root password and configure MySQL server options.
3. **Verify Installation:** Open a terminal or command prompt and type `mysql --version` to check if MySQL is installed correctly.

**Connecting to MySQL:**
You can connect to MySQL using various tools such as MySQL Workbench, command line, or Python (using connectors like `mysql-connector-python`).

#### SQL Statements: Creating databases and tables, inserting and selecting data

**Creating a Database:**
**Syntax:**
```sql
CREATE DATABASE database_name;
```
**Example:**
```sql
CREATE DATABASE school;
```

**Creating a Table:**
**Syntax:**
```sql
CREATE TABLE table_name (
    column1 datatype constraints,
    column2 datatype constraints,
    ...
);
```
**Example:**
```sql
USE school;

CREATE TABLE students (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT,
    grade VARCHAR(5)
);
```

**Inserting Data:**
**Syntax:**
```sql
INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);
```
**Example:**
```sql
INSERT INTO students (name, age, grade) VALUES ('John Doe', 18, 'A');
```

**Selecting Data:**
**Syntax:**
```sql
SELECT column1, column2, ... FROM table_name;
```
**Example:**
```sql
SELECT * FROM students;
```

#### Advanced SQL: Update, delete, order by, where, and, or, not, min, max, count, top, sum, like, in, between, joins

**Updating Data:**
**Syntax:**
```sql
UPDATE table_name SET column1 = value1, column2 = value2, ... WHERE condition;
```
**Example:**
```sql
UPDATE students SET grade = 'B' WHERE name = 'John Doe';
```

**Deleting Data:**
**Syntax:**
```sql
DELETE FROM table_name WHERE condition;
```
**Example:**
```sql
DELETE FROM students WHERE name = 'John Doe';
```

**Ordering Data:**
**Syntax:**
```sql
SELECT column1, column2, ... FROM table_name ORDER BY column1 ASC|DESC;
```
**Example:**
```sql
SELECT * FROM students ORDER BY age DESC;
```

**Filtering Data with WHERE:**
**Syntax:**
```sql
SELECT column1, column2, ... FROM table_name WHERE condition;
```
**Example:**
```sql
SELECT * FROM students WHERE age > 18;
```

**Logical Operators (AND, OR, NOT):**
**Example:**
```sql
SELECT * FROM students WHERE age > 18 AND grade = 'A';
```

**Aggregate Functions (MIN, MAX, COUNT, SUM):**
**Example:**
```sql
SELECT MIN(age) FROM students;
SELECT MAX(age) FROM students;
SELECT COUNT(*) FROM students;
SELECT SUM(age) FROM students;
```

**Pattern Matching with LIKE:**
**Example:**
```sql
SELECT * FROM students WHERE name LIKE 'J%';
```

**IN Operator:**
**Example:**
```sql
SELECT * FROM students WHERE grade IN ('A', 'B');
```

**BETWEEN Operator:**
**Example:**
```sql
SELECT * FROM students WHERE age BETWEEN 18 AND 22;
```

**Joins (INNER, LEFT, RIGHT, FULL):**
**Example:**
```sql
CREATE TABLE courses (
    course_id INT AUTO_INCREMENT PRIMARY KEY,
    course_name VARCHAR(100) NOT NULL,
    student_id INT,
    FOREIGN KEY (student_id) REFERENCES students(id)
);

SELECT students.name, courses.course_name
FROM students
INNER JOIN courses ON students.id = courses.student_id;
```

#### Practical Session

**Programs to Connect Python with MySQL and Perform Read and Write Operations:**

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

2. **Creating a Table:**
```python
# Creating the students table
cursor.execute("""
CREATE TABLE IF NOT EXISTS students (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT,
    grade VARCHAR(5)
)
""")
conn.commit()
```

3. **Inserting Data:**
```python
# Inserting data into the students table
cursor.execute("""
INSERT INTO students (name, age, grade)
VALUES (%s, %s, %s)
""", ("Alice", 20, "A"))
conn.commit()
```

4. **Selecting Data:**
```python
# Retrieving data from the students table
cursor.execute("SELECT * FROM students")
rows = cursor.fetchall()
for row in rows:
    print(row)
```

5. **Updating Data:**
```python
# Updating data in the students table
cursor.execute("""
UPDATE students SET grade = %s WHERE name = %s
""", ("B", "Alice"))
conn.commit()
```

6. **Deleting Data:**
```python
# Deleting data from the students table
cursor.execute("DELETE FROM students WHERE name = %s", ("Alice",))
conn.commit()
```

7. **Closing the Connection:**
```python
# Closing the connection
conn.close()
```

### Assignment Questions

1. **Write a Python program to create a database and a table in MySQL.**
```python
import mysql.connector

# Establishing connection
conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="your_password"
)

# Creating a cursor object
cursor = conn.cursor()

# Creating a database
cursor.execute("CREATE DATABASE IF NOT EXISTS testdb")

# Using the created database
cursor.execute("USE testdb")

# Creating a table
cursor.execute("""
CREATE TABLE IF NOT EXISTS employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    position VARCHAR(100),
    salary DECIMAL(10, 2)
)
""")

# Committing the transaction
conn.commit()

# Closing the connection
conn.close()
```

2. **Create a program to insert data into a MySQL table and retrieve it using a SELECT query.**
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

# Inserting data into the employees table
cursor.execute("""
INSERT INTO employees (name, position, salary)
VALUES (%s, %s, %s)
""", ("John Doe", "Software Engineer", 75000.00))
conn.commit()

# Retrieving data from the employees table
cursor.execute("SELECT * FROM employees")
rows = cursor.fetchall()
for row in rows:
    print(row)

# Closing the connection
conn.close()
```

### IPython Notebook Example

Create a new Jupyter Notebook and include the following content:

```markdown
# Day 4: Database in Python

## Database Overview: Introduction to MySQL
### Introduction to MySQL
- **Key Features of MySQL:**
  - Cross-platform support (Windows, macOS, Linux)
  - High performance and scalability
  - Strong security features
  - Comprehensive data storage and retrieval capabilities

### Installing MySQL
1. **Download MySQL:** Go to the [MySQL website](https://dev.mysql.com/downloads/) and download the installer for your operating system.
2. **Install MySQL:** Follow the installation instructions for your operating system.
3. **Verify Installation:** Open a terminal or command prompt and type `mysql --version`.

### Connecting to MySQL
You can connect to MySQL using various tools such as MySQL Workbench, command line, or Python (using connectors like `mysql-connector-python`).

## SQL Statements: Creating databases and tables, inserting and selecting data
### Creating a Database
- **Syntax:**
```sql
CREATE DATABASE database_name;
```
- **Example:**
```sql
CREATE DATABASE school;
```

### Creating a Table
- **Syntax:**
```sql
CREATE TABLE table_name (
    column1 datatype constraints,
    column2 datatype constraints,
    ...
);
```
- **Example:**
```sql
USE school;

CREATE TABLE students (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT,
    grade VARCHAR(5)
);
```

### Inserting Data
- **Syntax:**
```sql
INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);
```
- **Example:**
```sql
INSERT INTO students (name, age, grade) VALUES
 ('John Doe', 18, 'A');
```

### Selecting Data
- **Syntax:**
```sql
SELECT column1, column2, ... FROM table_name;
```
- **Example:**
```sql
SELECT * FROM students;
```

## Advanced SQL: Update, delete, order by, where, and, or, not, min, max, count, top, sum, like, in, between, joins
### Updating Data
- **Syntax:**
```sql
UPDATE table_name SET column1 = value1, column2 = value2, ... WHERE condition;
```
- **Example:**
```sql
UPDATE students SET grade = 'B' WHERE name = 'John Doe';
```

### Deleting Data
- **Syntax:**
```sql
DELETE FROM table_name WHERE condition;
```
- **Example:**
```sql
DELETE FROM students WHERE name = 'John Doe';
```

### Ordering Data
- **Syntax:**
```sql
SELECT column1, column2, ... FROM table_name ORDER BY column1 ASC|DESC;
```
- **Example:**
```sql
SELECT * FROM students ORDER BY age DESC;
```

### Filtering Data with WHERE
- **Syntax:**
```sql
SELECT column1, column2, ... FROM table_name WHERE condition;
```
- **Example:**
```sql
SELECT * FROM students WHERE age > 18;
```

### Logical Operators (AND, OR, NOT)
- **Example:**
```sql
SELECT * FROM students WHERE age > 18 AND grade = 'A';
```

### Aggregate Functions (MIN, MAX, COUNT, SUM)
- **Example:**
```sql
SELECT MIN(age) FROM students;
SELECT MAX(age) FROM students;
SELECT COUNT(*) FROM students;
SELECT SUM(age) FROM students;
```

### Pattern Matching with LIKE
- **Example:**
```sql
SELECT * FROM students WHERE name LIKE 'J%';
```

### IN Operator
- **Example:**
```sql
SELECT * FROM students WHERE grade IN ('A', 'B');
```

### BETWEEN Operator
- **Example:**
```sql
SELECT * FROM students WHERE age BETWEEN 18 AND 22;
```

### Joins (INNER, LEFT, RIGHT, FULL)
- **Example:**
```sql
CREATE TABLE courses (
    course_id INT AUTO_INCREMENT PRIMARY KEY,
    course_name VARCHAR(100) NOT NULL,
    student_id INT,
    FOREIGN KEY (student_id) REFERENCES students(id)
);

SELECT students.name, courses.course_name
FROM students
INNER JOIN courses ON students.id = courses.student_id;
```

## Practical Session
### Programs to Connect Python with MySQL and Perform Read and Write Operations

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

2. **Creating a Table:**
```python
# Creating the students table
cursor.execute("""
CREATE TABLE IF NOT EXISTS students (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT,
    grade VARCHAR(5)
)
""")
conn.commit()
```

3. **Inserting Data:**
```python
# Inserting data into the students table
cursor.execute("""
INSERT INTO students (name, age, grade)
VALUES (%s, %s, %s)
""", ("Alice", 20, "A"))
conn.commit()
```

4. **Selecting Data:**
```python
# Retrieving data from the students table
cursor.execute("SELECT * FROM students")
rows = cursor.fetchall()
for row in rows:
    print(row)
```

5. **Updating Data:**
```python
# Updating data in the students table
cursor.execute("""
UPDATE students SET grade = %s WHERE name = %s
""", ("B", "Alice"))
conn.commit()
```

6. **Deleting Data:**
```python
# Deleting data from the students table
cursor.execute("DELETE FROM students WHERE name = %s", ("Alice",))
conn.commit()
```

7. **Closing the Connection:**
```python
# Closing the connection
conn.close()
```

## Assignments
1. Write a Python program to create a database and a table in MySQL.
```python
import mysql.connector

# Establishing connection
conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="your_password"
)

# Creating a cursor object
cursor = conn.cursor()

# Creating a database
cursor.execute("CREATE DATABASE IF NOT EXISTS testdb")

# Using the created database
cursor.execute("USE testdb")

# Creating a table
cursor.execute("""
CREATE TABLE IF NOT EXISTS employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    position VARCHAR(100),
    salary DECIMAL(10, 2)
)
""")

# Committing the transaction
conn.commit()

# Closing the connection
conn.close()
```

2. Create a program to insert data into a MySQL table and retrieve it using a SELECT query.
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

# Inserting data into the employees table
cursor.execute("""
INSERT INTO employees (name, position, salary)
VALUES (%s, %s, %s)
""", ("John Doe", "Software Engineer", 75000.00))
conn.commit()

# Retrieving data from the employees table
cursor.execute("SELECT * FROM employees")
rows = cursor.fetchall()
for row in rows:
    print(row)

# Closing the connection
conn.close()
```
```

In the code cells of the notebook, include the Python code provided above for each section.
