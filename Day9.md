### Day 9: Introduction to FastAPI

#### FastAPI Introduction: Building a Simple API with FastAPI

**What is FastAPI?**
FastAPI is a modern, fast (high-performance), web framework for building APIs with Python 3.7+ based on standard Python type hints. FastAPI is designed to be easy to use and learn, and it is ideal for building robust and performant APIs.

**Key Features of FastAPI:**
- **High Performance:** One of the fastest Python web frameworks.
- **Easy to Use:** Designed to be easy and intuitive to use.
- **Automatic Interactive Documentation:** Provides interactive API documentation out-of-the-box (Swagger UI and ReDoc).
- **Based on Standards:** Built on top of Starlette for the web parts and Pydantic for the data parts.
- **Type Safety:** Uses Python type hints to provide robust data validation and parsing.

**Installing FastAPI:**
1. **Install FastAPI and an ASGI server (e.g., `uvicorn`):**
   ```sh
   pip install fastapi uvicorn
   ```

**Creating a Simple FastAPI Application:**
1. **Basic Setup:**
   - Create a file named `main.py` with the following content:
     ```python
     from fastapi import FastAPI

     app = FastAPI()

     @app.get("/")
     def read_root():
         return {"Hello": "World"}

     if __name__ == "__main__":
         import uvicorn
         uvicorn.run(app, host="127.0.0.1", port=8000)
     ```

2. **Running the Application:**
   - Run the application using `uvicorn`:
     ```sh
     uvicorn main:app --reload
     ```
   - Open your browser and navigate to `http://127.0.0.1:8000` to see the JSON response `{"Hello": "World"}`.

**Interactive API Documentation:**
- FastAPI automatically generates interactive API documentation at:
  - Swagger UI: `http://127.0.0.1:8000/docs`
  - ReDoc: `http://127.0.0.1:8000/redoc`

#### Practical Session: Developing and Testing FastAPI Endpoints

**Building a Simple CRUD API:**

1. **Setting Up Models:**
   ```python
   from pydantic import BaseModel

   class Item(BaseModel):
       name: str
       description: str = None
       price: float
       tax: float = None
   ```

2. **Creating CRUD Endpoints:**
   ```python
   from fastapi import FastAPI, HTTPException

   app = FastAPI()

   items = {}

   @app.post("/items/", response_model=Item)
   def create_item(item_id: int, item: Item):
       if item_id in items:
           raise HTTPException(status_code=400, detail="Item already exists")
       items[item_id] = item
       return item

   @app.get("/items/{item_id}", response_model=Item)
   def read_item(item_id: int):
       if item_id not in items:
           raise HTTPException(status_code=404, detail="Item not found")
       return items[item_id]

   @app.put("/items/{item_id}", response_model=Item)
   def update_item(item_id: int, item: Item):
       if item_id not in items:
           raise HTTPException(status_code=404, detail="Item not found")
       items[item_id] = item
       return item

   @app.delete("/items/{item_id}", response_model=Item)
   def delete_item(item_id: int):
       if item_id not in items:
           raise HTTPException(status_code=404, detail="Item not found")
       return items.pop(item_id)
   ```

3. **Testing the Endpoints:**
   - Use tools like Postman or the interactive Swagger UI at `http://127.0.0.1:8000/docs` to test the CRUD operations.

**Handling User Authentication:**

1. **Installing Dependencies:**
   ```sh
   pip install python-multipart
   ```

2. **Setting Up Authentication:**
   ```python
   from fastapi import FastAPI, Depends, HTTPException, status
   from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm
   from pydantic import BaseModel
   from passlib.context import CryptContext

   app = FastAPI()

   pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto")
   oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

   fake_users_db = {
       "john": {
           "username": "john",
           "full_name": "John Doe",
           "email": "john@example.com",
           "hashed_password": pwd_context.hash("secret"),
           "disabled": False,
       }
   }

   class User(BaseModel):
       username: str
       email: str = None
       full_name: str = None
       disabled: bool = None

   class UserInDB(User):
       hashed_password: str

   def verify_password(plain_password, hashed_password):
       return pwd_context.verify(plain_password, hashed_password)

   def get_user(db, username: str):
       if username in db:
           user_dict = db[username]
           return UserInDB(**user_dict)

   def authenticate_user(fake_db, username: str, password: str):
       user = get_user(fake_db, username)
       if not user:
           return False
       if not verify_password(password, user.hashed_password):
           return False
       return user

   @app.post("/token")
   async def login(form_data: OAuth2PasswordRequestForm = Depends()):
       user = authenticate_user(fake_users_db, form_data.username, form_data.password)
       if not user:
           raise HTTPException(
               status_code=status.HTTP_401_UNAUTHORIZED,
               detail="Incorrect username or password",
               headers={"WWW-Authenticate": "Bearer"},
           )
       return {"access_token": user.username, "token_type": "bearer"}

   @app.get("/users/me")
   async def read_users_me(token: str = Depends(oauth2_scheme)):
       user = get_user(fake_users_db, token)
       if user is None:
           raise HTTPException(status_code=401, detail="Invalid authentication credentials")
       return user
   ```

3. **Testing the Authentication Endpoints:**
   - Use the `/token` endpoint to get a token by passing a username and password.
   - Use the token to access the `/users/me` endpoint.

### Assignment Questions

**Question 1: Write a FastAPI application to create a simple CRUD API.**
```python
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    description: str = None
    price: float
    tax: float = None

items = {}

@app.post("/items/", response_model=Item)
def create_item(item_id: int, item: Item):
    if item_id in items:
        raise HTTPException(status_code=400, detail="Item already exists")
    items[item_id] = item
    return item

@app.get("/items/{item_id}", response_model=Item)
def read_item(item_id: int):
    if item_id not in items:
        raise HTTPException(status_code=404, detail="Item not found")
    return items[item_id]

@app.put("/items/{item_id}", response_model=Item)
def update_item(item_id: int, item: Item):
    if item_id not in items:
        raise HTTPException(status_code=404, detail="Item not found")
    items[item_id] = item
    return item

@app.delete("/items/{item_id}", response_model=Item)
def delete_item(item_id: int):
    if item_id not in items:
        raise HTTPException(status_code=404, detail="Item not found")
    return items.pop(item_id)
```

**Question 2: Create a FastAPI endpoint to handle user authentication.**
```python
from fastapi import FastAPI, Depends, HTTPException, status
from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm
from pydantic import BaseModel
from passlib.context import CryptContext

app = FastAPI()

pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto")
oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

fake_users_db = {
    "john": {
        "username": "john",
        "full_name": "John Doe",
        "email": "john@example.com",
        "hashed_password": pwd_context.hash("secret"),
        "disabled": False,
    }
}

class User(BaseModel):
    username: str
    email: str = None
    full_name: str = None
    disabled: bool = None

class UserInDB(User):
    hashed_password: str

def verify_password(plain_password, hashed_password):
    return pwd_context.verify(plain_password, hashed_password)

def get_user(db, username: str):
    if username in db:
        user_dict = db[username]
        return UserInDB(**user_dict)

def authenticate_user(fake_db, username: str, password: str):
    user = get_user(fake_db, username)
    if not user:
        return False
    if not verify_password(password, user.hashed_password):
        return False
    return user

@app.post("/token")
async def login(form_data: OAuth2PasswordRequestForm = Depends()):
    user = authenticate_user(fake_users_db, form_data.username, form_data.password)
    if not user:
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Incorrect username or password",
            headers={"WWW-Authenticate": "Bearer"},
        )
    return {"access_token": user.username, "token_type": "bearer"}

@app.get("/users/me")
async def read_users_me(token: str = Depends(oauth2_scheme)):
    user = get_user(fake_users_db, token)
    if user is None:
        raise HTTPException(status_code=401, detail="Invalid authentication credentials")
    return user
```

### IPython Notebook Example

Create a new Jupyter Notebook and include the following content:

```markdown
# Day 9: Introduction to FastAPI

## FastAPI Introduction: Building a Simple API with FastAPI

### What is FastAPI?
FastAPI is a modern, fast (high-performance), web framework for building APIs with Python 3.7+ based on standard Python type hints.

### Key Features of FastAPI
- **High Performance:** One of the fastest Python web frameworks.
- **Easy to Use:** Designed to be easy and intuitive to use.
- **Automatic Interactive Documentation:** Provides interactive API documentation out-of-the-box (Swagger UI and ReDoc).
- **Based on Standards:** Built on top of Starlette for the web parts and Pydantic for the data parts.
- **Type Safety:** Uses Python type hints to provide robust data validation and parsing.

### Installing FastAPI
1. **Install FastAPI and an ASGI server (e.g., `uvicorn`):**
   ```sh
   pip install fastapi uvicorn
   ```

### Creating a Simple FastAPI Application
1. **Basic Setup:**
   - Create a file named `main.py` with the following content:
     ```python
     from fastapi import FastAPI

     app = FastAPI()

     @app.get("/")
     def read_root():
         return {"Hello": "World"}

     if __name__ == "__main__":
         import uvicorn
         uvicorn.run(app, host="127.0.0.1", port=8000)
     ```

2. **Running the Application:**
   - Run the application using `uvicorn`:
     ```sh
     uvicorn main:app --reload
     ```
   - Open your browser and navigate to `http://127.0.0.1:8000` to see the JSON response `{"Hello": "World"}`.

### Interactive API Documentation
- FastAPI automatically generates interactive API documentation at:
  - Swagger UI: `http://127.0.0.1:8000/docs`
  - ReDoc: `http://127.0.0.1:8000/redoc`

## Practical Session: Developing and Testing FastAPI Endpoints

### Building a Simple CRUD API

1. **Setting Up Models:**
   ```python
   from pydantic import BaseModel

   class Item(BaseModel):
       name: str
       description: str = None
       price: float
       tax: float = None
   ```

2. **Creating CRUD Endpoints:**
   ```python
   from fastapi import FastAPI, HTTPException

   app = FastAPI()

   items = {}

   @app.post("/items/", response_model=Item)
   def create_item(item_id: int, item: Item):
       if item_id in items:
           raise HTTPException(status_code=400, detail="Item already exists")
       items[item_id] = item
       return item

   @app.get("/items/{item_id}", response_model=Item)
   def read_item(item_id: int):
       if item_id not in items:
           raise HTTPException(status_code=404, detail="Item not found")
       return items[item_id]

   @app.put("/items/{item_id}", response_model=Item)
   def update_item(item_id: int, item: Item):
       if item_id not in items:
           raise HTTPException(status_code=404, detail="Item not found")
       items[item_id] = item
       return item

   @app.delete("/items/{item_id}", response_model=Item)
   def delete_item(item_id: int):
       if item_id not in items:
           raise HTTPException(status_code=404, detail="Item not found")
       return items.pop(item_id)
   ```

3. **Testing the Endpoints:**
   - Use tools like Postman or the interactive Swagger UI at `http://127.0.0.1:8000/docs` to test the CRUD operations.

### Handling User Authentication

1. **Installing Dependencies:**
   ```sh
   pip install python-multipart
   ```

2. **Setting Up Authentication:**
   ```python
   from fastapi import FastAPI, Depends, HTTPException, status
   from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm
   from pydantic import BaseModel
   from passlib.context import CryptContext

   app = FastAPI()

   pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto")
   oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

   fake_users_db = {
       "john": {
           "username": "john",
           "full_name": "John Doe",
           "email": "john@example.com",
           "hashed_password": pwd_context.hash("secret"),
           "disabled": False,
       }
   }

   class User(BaseModel):
       username: str
       email: str = None
       full_name: str = None
       disabled: bool = None

   class UserInDB(User):
       hashed_password: str

   def verify_password(plain_password, hashed_password):
       return pwd_context.verify(plain_password, hashed_password)

   def get_user(db, username: str):
       if username in db:
           user_dict = db[username]
           return UserInDB(**user_dict)

   def authenticate_user(fake_db, username: str, password: str):
       user = get_user(fake_db, username)
       if not user:
           return False
       if not verify_password(password, user.hashed_password):
           return False
       return user

   @app.post("/token")
   async def login(form_data: OAuth2PasswordRequestForm = Depends()):
       user = authenticate_user(fake_users_db, form_data.username, form_data.password)
       if not user:
           raise HTTPException(
               status_code=status.HTTP_401_UNAUTHORIZED,
               detail="Incorrect username or password",
               headers={"WWW-Authenticate": "Bearer"},
           )
       return {"access_token": user.username, "token_type": "bearer"}

   @app.get("/users/me")
   async def read_users_me(token: str = Depends(oauth2_scheme)):
       user = get_user(fake_users_db, token)
       if user is None:
           raise HTTPException(status_code=401, detail="Invalid authentication credentials")
       return user
   ```

3. **Testing the Authentication Endpoints:**
   - Use the `/token` endpoint to get a token by passing a username and password.
   - Use the token to access the `/users/me` endpoint.

## Assignments
1. Write a FastAPI application to create a simple CRUD API.
```python
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    description: str = None
    price: float
    tax: float = None

items = {}

@app.post("/items/", response_model=Item)
def create_item(item_id: int, item: Item):
    if item_id in items:
        raise HTTPException(status_code=400, detail="Item already exists")
    items[item_id] = item
    return item

@app.get("/items/{item_id}", response_model=Item)
def read_item(item_id: int):
    if item_id not in items:
        raise HTTPException(status_code=404, detail="Item not found")
    return items[item_id]

@app.put("/items/{item_id}", response_model=Item)
def update_item(item_id: int, item: Item):
    if item_id not in items:
        raise HTTPException(status_code=404, detail="Item not found")
    items[item_id] = item
    return item

@app.delete("/items/{item_id}", response_model=Item)
def delete_item(item_id: int):
    if item_id not in items:
        raise HTTPException(status_code=404, detail="Item not found")
    return items.pop(item_id)
```

2. Create a FastAPI endpoint to handle user authentication.
```python
from fastapi import FastAPI, Depends, HTTPException, status
from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm
from pydantic import BaseModel
from passlib.context import CryptContext

app = FastAPI()

pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto")
oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

fake_users_db = {
    "john": {
        "username": "john",
        "full_name": "John Doe",
        "email": "john@example.com",
        "hashed_password": pwd_context.hash("secret"),
        "disabled": False,
    }
}

class User(BaseModel):
    username: str
    email: str = None
    full_name: str = None
    disabled: bool = None

class UserInDB(User):
    hashed_password: str

def verify_password(plain_password, hashed_password):
    return pwd_context.verify(plain_password, hashed_password)

def get_user(db, username: str):
    if username in db:
        user_dict = db[username]
        return UserInDB(**user_dict)

def authenticate_user(fake_db, username: str, password: str):
    user = get_user(fake_db, username)
    if not user:
        return False
    if not verify_password(password, user.hashed_password):
        return False
    return user

@app.post("/token")
async def login(form_data: OAuth2PasswordRequestForm = Depends()):
    user = authenticate_user(fake_users_db, form_data.username, form_data.password)
    if not user:
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Incorrect username or password",
            headers={"WWW-Authenticate": "Bearer"},
        )
    return {"access_token": user.username, "token_type": "bearer"}

@app.get("/users/me")
async def read_users_me(token: str = Depends(oauth2_scheme)):
    user = get_user(fake_users_db, token)
    if user is None:
        raise HTTPException(status_code=401, detail="Invalid authentication credentials")
    return user
```
```

In the code cells of the notebook, include the Python code provided above for each section.
