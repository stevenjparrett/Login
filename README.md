# Login
Certainly! Below, I'll provide a basic example of a signup and signin page using HTML and JavaScript that interacts with browser's local storage. Remember, this method should not be used for storing sensitive information like passwords in production environments, as local storage is not secure.

### Step 1: HTML for Signup and Signin Pages

You can use a single HTML file to handle both signup and signin or separate them. For simplicity, here's a single page:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Auth System</title>
</head>
<body>
    <div id="signup">
        <h2>Signup</h2>
        <input type="text" id="newUsername" placeholder="Enter Username">
        <input type="password" id="newPassword" placeholder="Enter Password">
        <button onclick="signup()">Register</button>
        <p id="signupMessage"></p>
    </div>

    <div id="signin">
        <h2>Signin</h2>
        <input type="text" id="username" placeholder="Enter Username">
        <input type="password" id="password" placeholder="Enter Password">
        <button onclick="signin()">Login</button>
        <p id="signinMessage"></p>
    </div>

    <script src="auth.js"></script>
</body>
</html>
```

### Step 2: JavaScript for Handling Signup and Signin

Create a file named `auth.js` to handle user registration and login:

```javascript
// Function to handle user registration
function signup() {
    const username = document.getElementById('newUsername').value;
    const password = document.getElementById('newPassword').value;
    if (!username || !password) {
        document.getElementById('signupMessage').innerText = 'Both fields are required.';
        return;
    }

    const users = JSON.parse(localStorage.getItem('users')) || [];
    if (users.some(user => user.username === username)) {
        document.getElementById('signupMessage').innerText = 'User already exists.';
        return;
    }

    users.push({ username, password });
    localStorage.setItem('users', JSON.stringify(users));
    document.getElementById('signupMessage').innerText = 'Registration successful!';
}

// Function to handle user login
function signin() {
    const username = document.getElementById('username').value;
    const password = document.getElementById('password').value;
    const users = JSON.parse(localStorage.getItem('users')) || [];
    
    const user = users.find(user => user.username === username && user.password === password);
    if (user) {
        document.getElementById('signinMessage').innerText = 'Login successful!';
    } else {
        document.getElementById('signinMessage').innerText = 'Invalid username or password.';
    }
}
```

### Explanation
- **HTML:** This page includes forms for both signup and signin. Each section has its input fields for username and password, and a button that triggers the respective JavaScript function.
- **JavaScript (`auth.js`):** This script handles the logic for user registration and authentication.
  - `signup()`: Adds a new user to local storage if the username isn't already taken.
  - `signin()`: Checks if the user exists in local storage with the correct password and logs them in if valid.

Remember to serve this HTML file from a local or remote server because local storage might not behave as expected when opening files directly with a `file://` URL in some browsers.


To direct users to a different page upon successful login, you can use JavaScript to change the location of the browser to the desired URL. Below, I'll adjust the JavaScript function for login (`signin`) to include a redirection to another page if the login is successful.

### Adjusted JavaScript with Redirect

Let's update the `signin()` function in your `auth.js` file:

```javascript
// Function to handle user login
function signin() {
    const username = document.getElementById('username').value;
    const password = document.getElementById('password').value;
    const users = JSON.parse(localStorage.getItem('users')) || [];
    
    const user = users.find(user => user.username === username && user.password === password);
    if (user) {
        document.getElementById('signinMessage').innerText = 'Login successful! Redirecting...';
        // Redirect to another page after successful login
        window.location.href = 'homepage.html'; // Change 'homepage.html' to your desired page
    } else {
        document.getElementById('signinMessage').innerText = 'Invalid username or password.';
    }
}
```

### Explanation:

- **Redirect on Success:** The `window.location.href` property is used to navigate to another page. Replace `'homepage.html'` with the actual URL or path to the page you want the user to go to after a successful login.

### Complete HTML Example:

For clarity, here’s how the entire HTML file would look with the JavaScript embedded directly for handling the signup and login. This includes the redirect on a successful login:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Auth System</title>
</head>
<body>
    <div id="signup">
        <h2>Signup</h2>
        <input type="text" id="newUsername" placeholder="Enter Username">
        <input type="password" id="newPassword" placeholder="Enter Password">
        <button onclick="signup()">Register</button>
        <p id="signupMessage"></p>
    </div>

    <div id="signin">
        <h2>Signin</h2>
        <input type="text" id="username" placeholder="Enter Username">
        <input type="password" id="password" placeholder="Enter Password">
        <button onclick="signin()">Login</button>
        <p id="signinMessage"></p>
    </div>

    <script>
        // Function to handle user registration
        function signup() {
            const username = document.getElementById('newUsername').value;
            const password = document.getElementById('newPassword').value;
            if (!username || !password) {
                document.getElementById('signupMessage').innerText = 'Both fields are required.';
                return;
            }

            const users = JSON.parse(localStorage.getItem('users')) || [];
            if (users.some(user => user.username === username)) {
                document.getElementById('signupMessage').innerText = 'User already exists.';
                return;
            }

            users.push({ username, password });
            localStorage.setItem('users', JSON.stringify(users));
            document.getElementById('signupMessage').innerText = 'Registration successful!';
        }

        // Function to handle user login
        function signin() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            const users = JSON.parse(localStorage.getItem('users')) || [];
            
            const user = users.find(user => user.username === username && user.password === password);
            if (user) {
                document.getElementById('signinMessage').innerText = 'Login successful! Redirecting...';
                window.location.href = 'homepage.html'; // Change 'homepage.html' to your desired page
            } else {
                document.getElementById('signinMessage').innerText = 'Invalid username or password.';
            }
        }
    </script>
</body>
</html>
```

Make sure to create the target page (e.g., `homepage.html`) that users will be redirected to after login.
