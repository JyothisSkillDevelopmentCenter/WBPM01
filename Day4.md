### Day 4: Database in Python

#### Database Overview: Introduction to MySQL

**Introduction to MySQL:**
MySQL is a widely-used open-source relational database management system (RDBMS) that uses Structured Query Language (SQL) for accessing and managing data. It is known for its reliability, scalability, and ease of use, making it a popular choice for web applications, data warehousing, and various other data-driven applications.

**Key Features of MySQL:**
- **Cross-Platform Support:** Available on various platforms, including Windows, macOS, Linux.
- **High Performance:** Optimized for speed and efficiency.
- **Scalability:** Suitable for small to large-scale applications.
- **Security:** Provides robust security features, including user authentication and access privileges.
- **Data Types and Indexing:** Supports various data types and indexing for efficient data retrieval.

**Installing MySQL:**
1. **Download MySQL:**
   - Visit the [MySQL website](https://dev.mysql.com/downloads/) and download the appropriate installer for your operating system.
2. **Install MySQL:**
   - Follow the installation instructions specific to your operating system. During installation, you will set up the root password and configure MySQL server options.
3. **Verify Installation:**
   - Open a terminal or command prompt and type `mysql --version` to ensure MySQL is installed correctly.

**Connecting to MySQL:**
You can connect to MySQL using various tools such as MySQL Workbench, command line, or Python (using connectors like `mysql-connector-python`).

#### SQL Statements: Creating Databases and Tables, Inserting and Selecting Data

**Creating a Database:**
Creating a database involves defining a new database in MySQL to organize your data.
**Syntax:**
```sql
CREATE DATABASE database_name;
```
**Example:**
```sql
CREATE DATABASE school;
```

**Creating a Table:**
Tables are used to store data in a structured format with rows and columns.
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
Inserting data into a table adds new rows of data.
**Syntax:**
```sql
INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);
```
**Example:**
```sql
INSERT INTO students (name, age, grade) VALUES ('John Doe', 18, 'A');
```

**Selecting Data:**
Selecting data retrieves data from the table based on specified criteria.
**Syntax:**
```sql
SELECT column1, column2, ... FROM table_name;
```
**Example:**
```sql
SELECT * FROM students;
```

#### Practical Session: Programs to Connect Python with MySQL, Performing Read and Write Operations

**Setting Up the Environment:**
1. **Install MySQL Connector:**
   - Use pip to install the MySQL connector for Python:
     ```sh
     pip install mysql-connector-python
     ```

**Connecting to MySQL:**
Connecting Python to MySQL involves using the `mysql-connector-python` library to establish a connection.
**Example:**
```python
import mysql.connector

# Establishing the connection
conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="your_password",
    database="school"
)

# Creating a cursor object
cursor = conn.cursor()
```

**Creating a Table:**
Use Python to create a table in the database.
**Example:**
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

**Inserting Data:**
Insert data into the table using Python.
**Example:**
```python
# Inserting data into the students table
cursor.execute("""
INSERT INTO students (name, age, grade)
VALUES (%s, %s, %s)
""", ("Alice", 20, "A"))
conn.commit()
```

**Selecting Data:**
Retrieve data from the table using Python.
**Example:**
```python
# Retrieving data from the students table
cursor.execute("SELECT * FROM students")
rows = cursor.fetchall()
for row in rows:
    print(row)
```

**Closing the Connection:**
Always close the connection after completing database operations.
**Example:**
```python
# Closing the connection
conn.close()
```

### Assignment Questions

**Question 1: Write a Python program to create a database and a table in MySQL.**
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

**Question 2: Create a program to insert data into a MySQL table and retrieve it using a SELECT query.**
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

## SQL Statements: Creating Databases and Tables, Inserting and Selecting Data
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
INSERT INTO students (name, age, grade) VALUES ('John Doe', 18, 'A');
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

5. **Closing the Connection:**
```python
# Closing the connection
conn.close()
```

## Assignments
1. Write a Python program to create a  database and a table in MySQL.
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
