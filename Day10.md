### Day 10: MongoDB Integration with Python

#### Introduction to MongoDB: Connecting Python with MongoDB, CRUD Operations

**What is MongoDB?**
MongoDB is a popular, open-source, document-oriented NoSQL database that stores data in flexible, JSON-like documents. It is designed for scalability and flexibility, making it ideal for handling large volumes of unstructured data.

**Key Features of MongoDB:**
- **Document-Oriented Storage:** Data is stored in documents (similar to JSON) rather than rows and columns.
- **Dynamic Schema:** Allows for flexible and evolving data structures.
- **High Performance:** Optimized for read and write operations.
- **Scalability:** Supports horizontal scaling through sharding.

**Installing MongoDB:**
1. **Download and Install MongoDB:**
   - Visit the [MongoDB website](https://www.mongodb.com/try/download/community) to download and install MongoDB for your operating system.
   - Follow the installation instructions specific to your operating system.

**Installing `pymongo`:**
1. **Install `pymongo` library:**
   ```sh
   pip install pymongo
   ```

**Connecting to MongoDB:**
1. **Basic Connection:**
   ```python
   from pymongo import MongoClient

   # Create a connection to MongoDB
   client = MongoClient("mongodb://localhost:27017/")

   # Access a database
   db = client["test_database"]

   # Access a collection
   collection = db["test_collection"]
   ```

**CRUD Operations:**

1. **Create (Insert):**
   ```python
   # Insert a document
   document = {"name": "John Doe", "age": 25, "city": "New York"}
   collection.insert_one(document)
   ```

2. **Read (Find):**
   ```python
   # Find a single document
   result = collection.find_one({"name": "John Doe"})
   print(result)

   # Find multiple documents
   results = collection.find({"city": "New York"})
   for doc in results:
       print(doc)
   ```

3. **Update:**
   ```python
   # Update a document
   collection.update_one({"name": "John Doe"}, {"$set": {"age": 26}})
   ```

4. **Delete:**
   ```python
   # Delete a document
   collection.delete_one({"name": "John Doe"})
   ```

#### Practical Session: MongoDB Integration with Python and FastAPI

**Setting Up FastAPI with MongoDB:**

1. **Install `motor` (Asynchronous MongoDB driver):**
   ```sh
   pip install motor
   ```

2. **Create a FastAPI Application:**

**Main Application File (`main.py`):**
```python
from fastapi import FastAPI, HTTPException
from motor.motor_asyncio import AsyncIOMotorClient
from pydantic import BaseModel
from bson import ObjectId
from typing import List

app = FastAPI()

# MongoDB connection
client = AsyncIOMotorClient("mongodb://localhost:27017")
db = client["test_database"]
collection = db["test_collection"]

class Item(BaseModel):
    name: str
    description: str = None
    price: float
    tax: float = None

class ItemInDB(Item):
    id: str

# Helper function to convert MongoDB document to Pydantic model
def item_helper(item) -> ItemInDB:
    return ItemInDB(
        id=str(item["_id"]),
        name=item["name"],
        description=item["description"],
        price=item["price"],
        tax=item["tax"],
    )

@app.post("/items/", response_model=ItemInDB)
async def create_item(item: Item):
    result = await collection.insert_one(item.dict())
    new_item = await collection.find_one({"_id": result.inserted_id})
    return item_helper(new_item)

@app.get("/items/{item_id}", response_model=ItemInDB)
async def read_item(item_id: str):
    item = await collection.find_one({"_id": ObjectId(item_id)})
    if item is None:
        raise HTTPException(status_code=404, detail="Item not found")
    return item_helper(item)

@app.put("/items/{item_id}", response_model=ItemInDB)
async def update_item(item_id: str, item: Item):
    result = await collection.update_one({"_id": ObjectId(item_id)}, {"$set": item.dict()})
    if result.matched_count == 0:
        raise HTTPException(status_code=404, detail="Item not found")
    updated_item = await collection.find_one({"_id": ObjectId(item_id)})
    return item_helper(updated_item)

@app.delete("/items/{item_id}", response_model=ItemInDB)
async def delete_item(item_id: str):
    result = await collection.delete_one({"_id": ObjectId(item_id)})
    if result.deleted_count == 0:
        raise HTTPException(status_code=404, detail="Item not found")
    return {"message": "Item deleted successfully"}

@app.get("/items/", response_model=List[ItemInDB])
async def list_items():
    items = []
    async for item in collection.find():
        items.append(item_helper(item))
    return items
```

**Testing the FastAPI with MongoDB:**
- Use tools like Postman or the interactive Swagger UI at `http://127.0.0.1:8000/docs` to test the CRUD operations.

### Assignment Questions

**Question 1: Create a FastAPI application with endpoints to perform CRUD operations on a MongoDB collection.**
```python
from fastapi import FastAPI, HTTPException
from motor.motor_asyncio import AsyncIOMotorClient
from pydantic import BaseModel
from bson import ObjectId
from typing import List

app = FastAPI()

# MongoDB connection
client = AsyncIOMotorClient("mongodb://localhost:27017")
db = client["school"]
collection = db["students"]

class Student(BaseModel):
    name: str
    age: int
    grade: str

class StudentInDB(Student):
    id: str

# Helper function to convert MongoDB document to Pydantic model
def student_helper(student) -> StudentInDB:
    return StudentInDB(
        id=str(student["_id"]),
        name=student["name"],
        age=student["age"],
        grade=student["grade"],
    )

@app.post("/students/", response_model=StudentInDB)
async def create_student(student: Student):
    result = await collection.insert_one(student.dict())
    new_student = await collection.find_one({"_id": result.inserted_id})
    return student_helper(new_student)

@app.get("/students/{student_id}", response_model=StudentInDB)
async def read_student(student_id: str):
    student = await collection.find_one({"_id": ObjectId(student_id)})
    if student is None:
        raise HTTPException(status_code=404, detail="Student not found")
    return student_helper(student)

@app.put("/students/{student_id}", response_model=StudentInDB)
async def update_student(student_id: str, student: Student):
    result = await collection.update_one({"_id": ObjectId(student_id)}, {"$set": student.dict()})
    if result.matched_count == 0:
        raise HTTPException(status_code=404, detail="Student not found")
    updated_student = await collection.find_one({"_id": ObjectId(student_id)})
    return student_helper(updated_student)

@app.delete("/students/{student_id}", response_model=StudentInDB)
async def delete_student(student_id: str):
    result = await collection.delete_one({"_id": ObjectId(student_id)})
    if result.deleted_count == 0:
        raise HTTPException(status_code=404, detail="Student not found")
    return {"message": "Student deleted successfully"}

@app.get("/students/", response_model=List[StudentInDB])
async def list_students():
    students = []
    async for student in collection.find():
        students.append(student_helper(student))
    return students
```

**Question 2: Write a Python program to demonstrate data retrieval and manipulation from a MongoDB collection.**
```python
from pymongo import MongoClient
from bson import ObjectId

# Create a connection to MongoDB
client = MongoClient("mongodb://localhost:27017/")

# Access a database
db = client["school"]

# Access a collection
collection = db["students"]

# Insert a document
student = {"name": "Jane Doe", "age": 22, "grade": "A"}
result = collection.insert_one(student)
print(f"Inserted student with ID: {result.inserted_id}")

# Find a document
student = collection.find_one({"_id": ObjectId(result.inserted_id)})
print(f"Found student: {student}")

# Update a document
collection.update_one({"_id": ObjectId(result.inserted_id)}, {"$set": {"age": 23}})
student = collection.find_one({"_id": ObjectId(result.inserted_id)})
print(f"Updated student: {student}")

# Delete a document
collection.delete_one({"_id": ObjectId(result.inserted_id)})
student = collection.find_one({"_id": ObjectId(result.inserted_id)})
print(f"Deleted student: {student}")
```

### IPython Notebook Example

Create a new Jupyter Notebook and include the following content:

```markdown
# Day 10: MongoDB Integration with Python

## Introduction to MongoDB: Connecting Python with MongoDB, CRUD Operations

### What is MongoDB?
MongoDB is a popular, open-source, document-oriented NoSQL database that stores data in flexible, JSON-like documents.

### Key Features of MongoDB
- **Document-Oriented Storage:** Data is stored in documents (similar to JSON)
 rather than rows and columns.
- **Dynamic Schema:** Allows for flexible and evolving data structures.
- **High Performance:** Optimized for read and write operations.
- **Scalability:** Supports horizontal scaling through sharding.

### Installing MongoDB
1. **Download and Install MongoDB:**
   - Visit the [MongoDB website](https://www.mongodb.com/try/download/community) to download and install MongoDB for your operating system.
   - Follow the installation instructions specific to your operating system.

### Installing `pymongo`
1. **Install `pymongo` library:**
   ```sh
   pip install pymongo
   ```

### Connecting to MongoDB
1. **Basic Connection:**
   ```python
   from pymongo import MongoClient

   # Create a connection to MongoDB
   client = MongoClient("mongodb://localhost:27017/")

   # Access a database
   db = client["test_database"]

   # Access a collection
   collection = db["test_collection"]
   ```

### CRUD Operations

1. **Create (Insert):**
   ```python
   # Insert a document
   document = {"name": "John Doe", "age": 25, "city": "New York"}
   collection.insert_one(document)
   ```

2. **Read (Find):**
   ```python
   # Find a single document
   result = collection.find_one({"name": "John Doe"})
   print(result)

   # Find multiple documents
   results = collection.find({"city": "New York"})
   for doc in results:
       print(doc)
   ```

3. **Update:**
   ```python
   # Update a document
   collection.update_one({"name": "John Doe"}, {"$set": {"age": 26}})
   ```

4. **Delete:**
   ```python
   # Delete a document
   collection.delete_one({"name": "John Doe"})
   ```

## Practical Session: MongoDB Integration with Python and FastAPI

### Setting Up FastAPI with MongoDB

1. **Install `motor` (Asynchronous MongoDB driver):**
   ```sh
   pip install motor
   ```

2. **Create a FastAPI Application**

**Main Application File (`main.py`):**
```python
from fastapi import FastAPI, HTTPException
from motor.motor_asyncio import AsyncIOMotorClient
from pydantic import BaseModel
from bson import ObjectId
from typing import List

app = FastAPI()

# MongoDB connection
client = AsyncIOMotorClient("mongodb://localhost:27017")
db = client["test_database"]
collection = db["test_collection"]

class Item(BaseModel):
    name: str
    description: str = None
    price: float
    tax: float = None

class ItemInDB(Item):
    id: str

# Helper function to convert MongoDB document to Pydantic model
def item_helper(item) -> ItemInDB:
    return ItemInDB(
        id=str(item["_id"]),
        name=item["name"],
        description=item["description"],
        price=item["price"],
        tax=item["tax"],
    )

@app.post("/items/", response_model=ItemInDB)
async def create_item(item: Item):
    result = await collection.insert_one(item.dict())
    new_item = await collection.find_one({"_id": result.inserted_id})
    return item_helper(new_item)

@app.get("/items/{item_id}", response_model=ItemInDB)
async def read_item(item_id: str):
    item = await collection.find_one({"_id": ObjectId(item_id)})
    if item is None:
        raise HTTPException(status_code=404, detail="Item not found")
    return item_helper(item)

@app.put("/items/{item_id}", response_model=ItemInDB)
async def update_item(item_id: str, item: Item):
    result = await collection.update_one({"_id": ObjectId(item_id)}, {"$set": item.dict()})
    if result.matched_count == 0:
        raise HTTPException(status_code=404, detail="Item not found")
    updated_item = await collection.find_one({"_id": ObjectId(item_id)})
    return item_helper(updated_item)

@app.delete("/items/{item_id}", response_model=ItemInDB)
async def delete_item(item_id: str):
    result = await collection.delete_one({"_id": ObjectId(item_id)})
    if result.deleted_count == 0:
        raise HTTPException(status_code=404, detail="Item not found")
    return {"message": "Item deleted successfully"}

@app.get("/items/", response_model=List[ItemInDB])
async def list_items():
    items = []
    async for item in collection.find():
        items.append(item_helper(item))
    return items
```

### Testing the FastAPI with MongoDB
- Use tools like Postman or the interactive Swagger UI at `http://127.0.0.1:8000/docs` to test the CRUD operations.

## Assignments

### Question 1: Create a FastAPI application with endpoints to perform CRUD operations on a MongoDB collection.
```python
from fastapi import FastAPI, HTTPException
from motor.motor_asyncio import AsyncIOMotorClient
from pydantic import BaseModel
from bson import ObjectId
from typing import List

app = FastAPI()

# MongoDB connection
client = AsyncIOMotorClient("mongodb://localhost:27017")
db = client["school"]
collection = db["students"]

class Student(BaseModel):
    name: str
    age: int
    grade: str

class StudentInDB(Student):
    id: str

# Helper function to convert MongoDB document to Pydantic model
def student_helper(student) -> StudentInDB:
    return StudentInDB(
        id=str(student["_id"]),
        name=student["name"],
        age=student["age"],
        grade=student["grade"],
    )

@app.post("/students/", response_model=StudentInDB)
async def create_student(student: Student):
    result = await collection.insert_one(student.dict())
    new_student = await collection.find_one({"_id": result.inserted_id})
    return student_helper(new_student)

@app.get("/students/{student_id}", response_model=StudentInDB)
async def read_student(student_id: str):
    student = await collection.find_one({"_id": ObjectId(student_id)})
    if student is None:
        raise HTTPException(status_code=404, detail="Student not found")
    return student_helper(student)

@app.put("/students/{student_id}", response_model=StudentInDB)
async def update_student(student_id: str, student: Student):
    result = await collection.update_one({"_id": ObjectId(student_id)}, {"$set": student.dict()})
    if result.matched_count == 0:
        raise HTTPException(status_code=404, detail="Student not found")
    updated_student = await collection.find_one({"_id": ObjectId(student_id)})
    return student_helper(updated_student)

@app.delete("/students/{student_id}", response_model=StudentInDB)
async def delete_student(student_id: str):
    result = await collection.delete_one({"_id": ObjectId(student_id)})
    if result.deleted_count == 0:
        raise HTTPException(status_code=404, detail="Student not found")
    return {"message": "Student deleted successfully"}

@app.get("/students/", response_model=List[StudentInDB])
async def list_students():
    students = []
    async for student in collection.find():
        students.append(student_helper(student))
    return students
```

### Question 2: Write a Python program to demonstrate data retrieval and manipulation from a MongoDB collection.
```python
from pymongo import MongoClient
from bson import ObjectId

# Create a connection to MongoDB
client = MongoClient("mongodb://localhost:27017/")

# Access a database
db = client["school"]

# Access a collection
collection = db["students"]

# Insert a document
student = {"name": "Jane Doe", "age": 22, "grade": "A"}
result = collection.insert_one(student)
print(f"Inserted student with ID: {result.inserted_id}")

# Find a document
student = collection.find_one({"_id": ObjectId(result.inserted_id)})
print(f"Found student: {student}")

# Update a document
collection.update_one({"_id": ObjectId(result.inserted_id)}, {"$set": {"age": 23}})
student = collection.find_one({"_id": ObjectId(result.inserted_id)})
print(f"Updated student: {student}")

# Delete a document
collection.delete_one({"_id": ObjectId(result.inserted_id)})
student = collection.find_one({"_id": ObjectId(result.inserted_id)})
print(f"Deleted student: {student}")
```
```

In the code cells of the notebook, include the Python code provided above for each section.
