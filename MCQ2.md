---

### Final MCQ Test for Second 5 Days

**Test 2: Day 6 to Day 10**

1. **Which of the following is a supervised learning algorithm?**
   - a) K-Means
   - b) Linear Regression
   - c) PCA
   - d) DBSCAN
   
   **Answer:** b) Linear Regression
   **Explanation:** Linear regression is a supervised learning algorithm used for predicting continuous values.

2. **What does the `mean` function calculate in statistics?**
   - a) The middle value in a dataset
   - b) The most frequent value in a dataset
   - c) The average value of a dataset
   - d) The range of a dataset
   
   **Answer:** c) The average value of a dataset
   **Explanation:** The mean is the sum of all values divided by the number of values.

3. **Which Python library is commonly used for data manipulation and analysis?**
   - a) NumPy
   - b) SciPy
   - c) Matplotlib
   - d) Pandas
   
   **Answer:** d) Pandas
   **Explanation:** Pandas is a powerful library for data manipulation and analysis.

4. **Which method is used to calculate the standard deviation of a dataset in Python?**
   - a) np.mean()
   - b) np.std()
   - c) np.var()
   - d) np.sum()
   
   **Answer:** b) np.std()
   **Explanation:** The `np.std()` method is used to calculate the standard deviation.

5. **What does the `fit` method do in a machine learning model?**
   - a) It evaluates the model's performance.
   - b) It trains the model using the provided data.
   - c) It makes predictions using the model.
   - d) It scales the data.
   
   **Answer:** b) It trains the model using the provided data.
   **Explanation:** The `fit` method trains the model on the provided data.

6. **Which of the following is used to evaluate the performance of a classification model?**
   - a) Mean Squared Error
   - b) R-Squared
   - c) F1 Score
   - d) Silhouette Score
   
   **Answer:** c) F1 Score
   **Explanation:** The F1 score is a measure of a model's accuracy, considering both precision and recall.

7. **What is cross-validation in machine learning?**
   - a) A technique to balance data
   - b) A method to split the dataset into multiple training and testing sets
   - c) A way to handle missing data
   - d) A technique to reduce the dimensionality of data
   
   **Answer:** b) A method to split the dataset into multiple training and testing sets
   **Explanation:** Cross-validation is used to evaluate the generalizability of a model.

8. **Which of the following is a document-oriented NoSQL database?**
   - a) MySQL
   - b) PostgreSQL
   - c) MongoDB
   - d) SQLite
   
   **Answer:** c) MongoDB
   **Explanation:** MongoDB is a document-oriented NoSQL database.

9. **Which Python library is used for connecting to MongoDB?**
   - a) PyMongo
   - b) SQLite3
   - c) MySQLdb
   - d) SQLAlchemy
   
   **Answer:** a) PyMongo
   **Explanation:** PyMongo is the official MongoDB driver for Python.

10. **How do you insert a document into a MongoDB collection using PyMongo?**
    - a) collection.add_one(document)
    - b) collection.insert_one(document)
    - c) collection.save(document)
    - d) collection.put(document)
   
    **Answer:** b) collection.insert_one(document)
    **Explanation:** The `insert_one` method is used to insert a document into a MongoDB collection.

11. **Which command is used to retrieve all documents from a MongoDB collection?**
    - a) collection.find_all()
    - b) collection.find({})
    - c) collection.get_all()
    - d) collection.select_all()
   
    **Answer:** b) collection.find({})
    **Explanation:** The `find` method with an empty query retrieves all documents.

12. **How do you update a document in MongoDB using PyMongo?**
    - a) collection.modify_one(query, update)
    - b) collection.update_one(query, update)
    - c) collection.change_one(query, update)
    - d) collection.alter_one(query, update)
   
    **Answer:** b) collection.update_one(query, update)
    **Explanation:** The `update_one` method is used to update a document in MongoDB.

13. **Which framework is known for its high performance in building APIs with Python?**
    - a) Flask
    - b) Django
    - c) FastAPI
    - d) Bottle
   
    **Answer:** c) FastAPI
    **Explanation:** FastAPI is known for its high performance and ease of use for building APIs.

14. **Which FastAPI component is used for handling security and authentication?**
    - a) OAuth2PasswordBearer
    - b) FastAPISecurity
    - c) AuthBearer
    - d) TokenHandler
   
    **Answer:** a) OAuth2PasswordBearer
    **Explanation:** OAuth2PasswordBearer is used for handling security and authentication in FastAPI.

15. **How do you start a FastAPI application?**
    - a) run fastapi main:app
    - b) uvicorn main:app --reload
    - c) start fastapi main:app
    - d) python -m fastapi main:app
   
    **Answer:** b) uvicorn main:app --reload
    **Explanation:** Uvicorn is used to run a FastAPI application with the `--reload` option for development.

16. **Which method is used to create a GET endpoint in FastAPI?**
    - a) @app.route("/")
    - b) @app.get("/")
    - c) @app.fetch("/")
    - d) @app.retrieve("/")
   
    **Answer:** b) @app.get("/")
    **Explanation:** The `@app.get("/")` decorator is used to create a GET endpoint in FastAPI.

17. **What is the primary purpose of the Pydantic library in FastAPI?**
    - a) To handle HTTP requests
    - b) To connect to databases
    - c) To validate and parse data
    - d) To render templates
   
    **Answer:** c) To validate and parse data
    **Explanation:** Pydantic is used for data validation and parsing in FastAPI.

18. **Which command is used to delete a document from a MongoDB collection using PyMongo?**
    - a) collection.remove_one(query)
    - b) collection.delete_one(query)
    - c) collection.erase_one(query)
    - d) collection.clear_one(query)
   
    **Answer:** b) collection.delete_one(query)
    **Explanation:** The `delete_one` method is used to delete a document from a MongoDB collection.

19. **How do you connect to a MongoDB database asynchronously in FastAPI?**
    - a) motor.connect("mongodb://localhost:27017")
    - b) motor.AsyncIOMotorClient("mongodb://localhost:27017")
    - c) pymongo.AsyncClient("mongodb://localhost:27017")
    - d) fastapi.MongoClient("mongodb://localhost:27017")
   
    **Answer:** b) motor.AsyncIOMotorClient("mongodb://localhost:27017")
    **Explanation:** The `motor.AsyncIOMotorClient` is used to connect to MongoDB asynchronously.

20. **Which method is used to perform data aggregation in MongoDB?**
    - a) aggregate()
    - b) group()
    - c) collate()
    - d) sum()
   
    **Answer:** a) aggregate()
    **Explanation:** The `aggregate` method is used for data aggregation in MongoDB.

21. **What is the purpose of the `__init__` method in a Python class?**
    - a) To destroy an object
    - b) To initialize an object's attributes
    - c) To create a class
    - d) To call a method
   
    **Answer:** b) To initialize an object's attributes
    **Explanation:** The `__init__` method initializes an object's attributes when it is created.

22. **Which Python library provides functions for scientific and technical computing?**
    - a) Matplotlib
    - b) NumPy
    - c) Flask
    - d) BeautifulSoup
   
    **Answer:** b) NumPy
    **Explanation:** NumPy provides functions for scientific and technical computing.

23. **How do you create a new database in MongoDB?**
    - a) client.new_database("dbname")
    - b) client.create_db("dbname")
    - c) client["dbname"]
    - d) client.add_db("dbname")
   
    **Answer:** c) client["dbname"]
    **Explanation:** Accessing a database that doesn't exist will create it in MongoDB.

24. **Which function is used to calculate the median of a dataset in Python?**
    - a) np.mean()
    - b) np.median()
    - c) np.mode()
    - d) np.average()
   
    **Answer:** b) np.median()
    **Explanation:** The `np.median()` function calculates the median of a dataset.

25. **What is the output of the following code?**
    ```python
    import numpy as np

    data = [1, 2, 3, 4, 5]
    result = np.percentile(data, 50)
    print(result)
    ```
    - a) 3.0
    - b) 2.5
    - c) 5.0
    - d) 1.0
   
    **Answer:** a) 3.0
    **Explanation:** The 50th percentile (median) of the dataset [1, 2, 3, 4, 5] is 3.0.

---
