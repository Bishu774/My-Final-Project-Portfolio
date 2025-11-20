# CS50 Mail
#### “This project can be viewed in the video demonstration (link below), which is recommended for admissions committees.”
Video Demo: https://youtu.be/1Dme9LivOiw
#### Description:
**CS50 Mail** is a fully functional web-based email client built using HTML, CSS, JavaScript, and Python (Flask).You can do three main tasks here. It simulates the experience of using an actual email platform and includes features such as inbox and sent view, email reading and composing emails and replying to received messages. This project is part of the final submission for the CS50x course and represents the culmination of several weeks of foundational work in computer science.

The motivation behind building this project was to deeply understand how modern web applications operate behind the scenes. Emails have become an essential part of our communication infrastructure, and learning how to replicate that functionality from scratch was both challenging and educational. The application was developed from scratch, emphasizing clarity, modularity, and security in both logic and user experience.

...
## 🚀 Features

**User Registration & Login**: Secure account creation with hashed passwords using Werkzeug’s password-hashing functions.
**Inbox View**: Logged-in users can view all received emails that match their username, presented in a clear tabular format.
**Sent View**: Displays all emails the user has sent.
**Compose Email**: Allows users to create new messages by specifying recipient, subject, and body.
**Reply Functionality**: Users can reply to emails, with subject line auto-filled and original message quoted.
**Email Detail View**: Each email can be viewed in detail on a separate page.
**Session Management**: Secure handling of user sessions using Flask-Session and cookies.
**Database Interaction**: Uses SQLite through CS50’s SQL wrapper for simplified querying and safety.
**Basic Input Validation**: Ensures that all required fields are filled, and usernames are unique during registration.

....
## 📁 File & Code Structure


### "app.py"
The heart of the backend, app.py contains all route definitions and application logic:

- @app.route("/") → Inbox (protected with @login_required)
- @app.route("/compose", methods=["GET", "POST"]) → Compose email
- @app.route("/sent") → Sent mailbox view
- @app.route("/email", methods=["POST"]) → Individual email detail view
- @app.route("/reply", methods=["POST"]) → Pre-fills compose form for reply
- @app.route("/register", methods=["GET", "POST"]) → User registration
- @app.route("/login", methods=["GET", "POST"])` → Login with session logic
- `@app.route("/logout") → Clears session and logs out user

These routes connect to various templates and handle both page rendering and backend processing.

### `helpers.py`
Contains utility functions:
- `apology()` – Displays error messages
- `login_required()` – Flask decorator to ensure a route requires a logged-in user
- `lookup()` and `usd()` – Repurposed or placeholder CS50 finance functions

### `templates/`
- `layout.html`: Base template with navigation and structure
- `index.html`: Used for both inbox and sent views
- `compose.html`: Form for creating a new message
- `email.html`: Displays full details of a selected email
- `reply.html`: Pre-filled form to reply to a message
- `login.html`, `register.html`: Auth pages

### `static/`
- `styles.css`: Custom CSS styling
- JavaScript logic was likely embedded or minimal; the app is primarily server-rendered.

---

## 🛠️ Technical Design

- **Flask Framework**: Enables server-side routing and HTML rendering via Jinja2.
- **Session Management**: Handled using Flask-Session with secure configuration (`SESSION_TYPE=filesystem`) and custom cookie expiration.
- **SQLite Database**: Two tables — `users` for authentication, and `emails` for storing message data. SQL queries use placeholders to prevent SQL injection.
- **Input Validation**: Checks for empty fields, duplicate usernames, and password mismatch during registration.
- **Security**: Passwords are hashed using `generate_password_hash()`; login checks use `check_password_hash()` to prevent plain-text password storage.

---

## 🔐 Email Flow Breakdown

### 📥 Inbox
- Uses `session["user_id"]` to get the current user
- Retrieves all emails where the user is the recipient

### 📤 Sent Mailbox
- Filters emails by current user's username as the sender

### ✉️ Compose
- GET: Loads a pre-filled form with sender’s username
- POST: Validates input, inserts new record into the `emails` table

### 🔁 Reply
- Retrieves the email’s original sender/subject/body and passes it to the reply form

### 🧾 Email View
- POST route `/email` retrieves and displays full message details, including subject, body, and timestamp

---

## 💡 Design Challenges & Decisions

- **Reply Feature Logic**: Required careful parsing of the email data and smart formatting to avoid redundant "Re:" prefixes.
- **Session Authentication**: Managing user state securely across routes while minimizing page reloads.
- **Data Integrity**: Ensured that every email operation (send, read, reply) required login and valid session ID.
- **Modular Structure**: Used CS50’s helper structure to keep the application modular and maintainable.

---

## 📚 What I Learned

This project helped me solidify:
- Full-stack logic from browser to database
- Secure password management
- Building REST-like web applications
- Validating forms and handling user feedback
- Rendering dynamic pages using Jinja2 templating
- Working with relational data and foreign key logic

I also became more confident with Flask, HTTP methods, session management, and separating concerns between front-end and back-end components.

---

## 🧠 Future Improvements

- Add email deletion and trash management
- Implement AJAX-based dynamic loading for mailbox views
- Allow email threads or conversation grouping
- Responsive design for mobile view
- Notification system for new mail
- Upload attachments to emails
- Better user input sanitation and error handling with Flask-WTF

---

## 🤖 Use of AI
# Used ChatGPT to help structure the README.md text. All code and logic are my own.
I used ChatGPT to:
- Help draft this README
- Assist with minor Flask syntax clarification
- Suggest reply formatting logic for clean subject lines

All core application logic, templates, routing, and database management were designed and implemented by me.

---

## ✅ Conclusion

**CS50 Mail** was a rewarding project that brought together the entire CS50 curriculum into one real-world application. It taught me how to think like a full-stack developer, manage user flow, design meaningful features, and deploy a useful tool that mimics real webmail systems. It was built with clarity, usability, and security in mind, and I am proud of what it represents as the final milestone of CS50x.


