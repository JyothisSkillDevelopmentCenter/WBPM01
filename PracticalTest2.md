
### Practical Test Questions for Second 5 Days

**Test 2: Day 6 to Day 10**

**Question 1: Machine Learning - Linear Regression**

**Task:**
Write a Python program to perform a simple linear regression using a given dataset of house sizes (in square feet) and their corresponding prices (in USD). Plot the regression line along with the data points.

**Answer:**
```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression

# Sample data
sizes = np.array([1500, 1600, 1700, 1800, 1900]).reshape(-1, 1)
prices = np.array([300000, 320000, 340000, 360000, 380000])

# Create and train the model
model = LinearRegression()
model.fit(sizes, prices)

# Predict prices
predicted_prices = model.predict(sizes)

# Plot data points and regression line
plt.scatter(sizes, prices, color='blue', label='Actual Prices')
plt.plot(sizes, predicted_prices, color='red', label='Regression Line')
plt.xlabel('Size (sq ft)')
plt.ylabel('Price (USD)')
plt.legend()
plt.show()
```

**Explanation:**
- The program creates a linear regression model using `sklearn.linear_model.LinearRegression`.
- It fits the model with the given sizes and prices.
- It predicts prices using the model and plots the actual data points and the regression line.

**Question 2: FastAPI and MongoDB Integration**

**Task:**
Create a FastAPI application with endpoints to perform CRUD operations on a MongoDB collection named `Books`. Each book should have a title, author, and year of publication. Include endpoints to create, read, update, and delete books.

**Answer:**
```python
from fastapi import FastAPI, HTTPException
from motor.motor_asyncio import AsyncIOMotorClient
from pydantic import BaseModel
from bson import ObjectId
from typing import List

app = FastAPI()

# MongoDB connection
client = AsyncIOMotorClient("mongodb://localhost:27017")
db = client["library"]
collection = db["books"]

class Book(BaseModel):
    title: str
    author: str
    year: int

class BookInDB(Book):
    id: str

# Helper function to convert MongoDB document to Pydantic model
def book_helper(book) -> BookInDB:
    return BookInDB(
        id=str(book["_id"]),
        title=book["title"],
        author=book["author"],
        year=book["year"]
    )

@app.post("/books/", response_model=BookInDB)
async def create_book(book: Book):
    result = await collection.insert_one(book.dict())
    new_book = await collection.find_one({"_id": result.inserted_id})
    return book_helper(new_book)

@app.get("/books/{book_id}", response_model=BookInDB)
async def read_book(book_id: str):
    book = await collection.find_one({"_id": ObjectId(book_id)})
    if book is None:
        raise HTTPException(status_code=404, detail="Book not found")
    return book_helper(book)

@app.put("/books/{book_id}", response_model=BookInDB)
async def update_book(book_id: str, book: Book):
    result = await collection.update_one({"_id": ObjectId(book_id)}, {"$set": book.dict()})
    if result.matched_count == 0:
        raise HTTPException(status_code=404, detail="Book not found")
    updated_book = await collection.find_one({"_id": ObjectId(book_id)})
    return book_helper(updated_book)

@app.delete("/books/{book_id}", response_model=BookInDB)
async def delete_book(book_id: str):
    result = await collection.delete_one({"_id": ObjectId(book_id)})
    if result.deleted_count == 0:
        raise HTTPException(status_code=404, detail="Book not found")
    return {"message": "Book deleted successfully"}

@app.get("/books/", response_model=List[BookInDB])
async def list_books():
    books = []
    async for book in collection.find():
        books.append(book_helper(book))
    return books
```

**Explanation:**
- The FastAPI application connects to a MongoDB collection named `Books`.
- It defines CRUD endpoints to create, read, update, and delete books.
- Each endpoint performs the respective operation on the MongoDB collection and returns the appropriate response.

These practical test questions assess the students' ability to apply the concepts learned in real-world scenarios, covering Python programming, SQL operations, machine learning, FastAPI, and MongoDB integration.
