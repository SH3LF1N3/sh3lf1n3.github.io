A **configuration file** (like `config.py`) in Flask is a Python file used to **store all the important settings** that your Flask app needs to run — especially things like:

- Database connection details
    
- Secret keys
    
- Debug mode status
    
- Mail server settings
    
- File upload settings

## Why Use a Configuration File?

Imagine your app is a car, and the configuration file is the dashboard where you control things like:

- Where to connect for fuel (Database)
    
- Security settings (Keys)
    
- Whether to show warning lights (Debugging logs)
    

Here’s **why it matters**:

1. **Keeps your app organized**: Instead of hardcoding values all over your app, you define them in one place.
    
2. **Easy to manage environments**: You can easily switch between _development_, _testing_, and _production_ settings.
    
3. **Improves security**: Keeps secrets (like `SECRET_KEY`) separate from the main codebase — better if moved to environment variables later.

```python
class Config:
    # SQLAlchemy DB URI format:
    # mysql+pymysql://username:password@localhost/db_name
    SQLALCHEMY_DATABASE_URI = 'mysql+pymysql://root:your_password@localhost/flask_db'
    SQLALCHEMY_TRACK_MODIFICATIONS = False  # Turn off unnecessary warning
    SECRET_KEY = 'your_secret_key'  # Used for sessions and security
```

## N/B 
When naming classes in Python, the name of the class should always start with a capital letter.

Step by step explanation of creating  a configuration file

```python
class Config:
```
- `Config` is a Python class that holds all the configurations values for the app
- Once defined, it is later loaded to the Flask app using `app.config.from_object(Config)` 


```python
    SQLALCHEMY_DATABASE_URI = 'mysql+pymysql://root:your_password@localhost/flask_db'
    
```

- This line tells SQLAlchemy how to connect to MySQL database
- The `root` is the MySQL username
- The `your_password` should be replaced ny your real SQL password
	
	Incase your password contains special characters, remember to encode it using the following script.
```python
import urllib.parse

print(urllib.parse.quote('Robo@2025'))
```

- `localhost` means the db is in your computer
- `flask_db` is the name of the db

```python
    SQLALCHEMY_TRACK_MODIFICATIONS = False

```

- Disables Flask's event system for SQLAlchemy, which isn't needed and just gives a warning if left on.

- Helps improve performance slightly.

```python
    SECRET_KEY = 'your_secret_key'

```
 This key is used for:

- Managing user sessions (like remembering if a user is logged in).

- Protecting forms from CSRF attacks.

- This should always be a secret and hard to guess (usually use `secrets.token_hex(16)` to generate one).

OR

```python
import secrets

def generate_key(length=32):
	return secrets.token_hex(length)

print("SECRET_KEY =", generate_key())
print("JWT_SECRET_KEY_DEV =", generate_key())
print("JWT_SECRET_KEY =", generate_key())

```
## How to Load `Config` Class into Your Flask App 

### In `app.py`:
```python
from flask import Flask
from config import Config

app = Flask(__name__)
app.config.from_object(Config)

```


This loads all the settings in `Config` into your Flask app 

## Models 


```shell 


```

