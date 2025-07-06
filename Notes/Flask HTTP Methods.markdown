# Flask HTTP Methods

## 1. Request

The `request` object in Flask provides access to incoming request data, such as form data, query parameters, headers, and more. It is part of the `flask` module and is typically imported as `from flask import request`.

**Example Use Case**: Handling form submissions or retrieving query parameters.

**Python Example**:

```python
from flask import Flask, request

app = Flask(__name__)

@app.route('/submit', methods=['POST'])
def submit():
    username = request.form.get('username')
    return f"Received: {username}"
```

**HTML Template (submit.html)**:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Submit Form</title>
</head>
<body>
    <h1>Submit Your Name</h1>
    <form method="POST" action="/submit">
        <label for="username">Username:</label>
        <input type="text" id="username" name="username">
        <button type="submit">Submit</button>
    </form>
</body>
</html>
```

## 2. Response

The `Response` object in Flask allows you to customize the HTTP response, including status codes, headers, and content. You can use `make_response` to create a response object.

**Example Use Case**: Setting custom headers or status codes.

**Python Example**:

```python
from flask import Flask, make_response

app = Flask(__name__)

@app.route('/response')
def custom_response():
    response = make_response('Custom Response', 200)
    response.headers['X-Custom-Header'] = 'Value'
    return response
```

**HTML Template (response.html)**:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Custom Response</title>
</head>
<body>
    <h1>Custom Response Page</h1>
    <p>This page returns a custom response with headers.</p>
</body>
</html>
```

## 3. Redirect

The `redirect` function in Flask redirects the user to another URL. It is commonly used after form submissions or to guide users to another route.

**Example Use Case**: Redirecting after a successful form submission.

**Python Example**:

```python
from flask import Flask, redirect, url_for

app = Flask(__name__)

@app.route('/go')
def go():
    return redirect(url_for('home'))
```

**HTML Template (go.html)**:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Redirect Page</title>
</head>
<body>
    <h1>Redirecting...</h1>
    <p>You will be redirected to the home page.</p>
</body>
</html>
```

## 4. Render

The `render_template` function in Flask renders an HTML template with optional context variables. It is used to generate dynamic HTML pages.

**Example Use Case**: Displaying dynamic content in a template.

**Python Example**:

```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/user/<name>')
def user(name):
    return render_template('user.html', name=name)
```

**HTML Template (user.html)**:

```html
<!DOCTYPE html>
<html>
<head>
    <title>User Page</title>
</head>
<body>
    <h1>Hello, {{ name }}!</h1>
    <p>Welcome to your personalized page.</p>
</body>
</html>
```

## 5. url_for

The `url_for` function generates URLs for Flask routes dynamically based on the endpoint name. It is useful for avoiding hard-coded URLs.

**Example Use Case**: Linking to other routes in templates or redirects.

**Python Example**:

```python
from flask import Flask, url_for, render_template

app = Flask(__name__)

@app.route('/')
def home():
    link = url_for('user', name='Alice')
    return render_template('home.html', link=link)
```

**HTML Template (home.html)**:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Home Page</title>
</head>
<body>
    <h1>Welcome to the Home Page</h1>
    <p>Visit the user page: <a href="{{ link }}">User Page</a></p>
</body>
</html>
```

## 6. Session

The `session` object in Flask is used to store user data across requests, stored server-side with a cookie-based session ID. It requires a secret key for security.

**Example Use Case**: Storing user login state or temporary data.

**Python Example**:

```python
from flask import Flask, session, redirect, url_for, render_template

app = Flask(__name__)
app.secret_key = 'your-secret-key'

@app.route('/login', methods=['POST'])
def login():
    session['username'] = request.form.get('username')
    return redirect(url_for('profile'))

@app.route('/profile')
def profile():
    username = session.get('username', 'Guest')
    return render_template('profile.html', username=username)
```

**HTML Template (login.html)**:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Login</title>
</head>
<body>
    <h1>Login</h1>
    <form method="POST" action="/login">
        <label for="username">Username:</label>
        <input type="text" id="username" name="username">
        <button type="submit">Login</button>
    </form>
</body>
</html>
```

**HTML Template (profile.html)**:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Profile</title>
</head>
<body>
    <h1>Profile Page</h1>
    <p>Welcome, {{ username }}!</p>
</body>
</html>
```