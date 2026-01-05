# Web Security Analysis & Patching (Flask)

![Python](https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python)
![Flask](https://img.shields.io/badge/Framework-Flask-green?style=for-the-badge)
![Security](https://img.shields.io/badge/Focus-Web%20Security-red?style=for-the-badge)

## 📌 Project Overview

This project focuses on the analysis and remediation of security vulnerabilities within a simple Student Management System built with **Python Flask** and **SQLite**.

Originally, the application was intentionally vulnerable to common web attacks. [cite_start]This repository documents the process of identifying these flaws and implementing secure coding practices to patch them, satisfying the requirements for the **Cybersecurity (Keamanan Siber)** course at Telkom University[cite: 1, 2, 5].

## 👥 Team Members

* [cite_start]**Rafif Baltirus Budiman** (1301204443) - Environment setup, SQL Injection patching, and reporting[cite: 9].
* [cite_start]**Faisal Surya Saputra** (103012330152) - Authentication implementation, XSS patching, and penetration testing[cite: 9].
* [cite_start]**Rafie Novianto Sudrajat** (103012500133) - CSRF protection (Secret Key configuration) and research[cite: 9].

## 🛡️ Vulnerabilities Patched

The following Common Weakness Enumerations (CWE) were identified and resolved:

### 1. Broken Authentication (CWE-306)
* **Vulnerability:** The application lacked login functionality. [cite_start]Critical actions (Create, Read, Update, Delete) were accessible to anonymous users via direct URL manipulation[cite: 36, 38].
* [cite_start]**Fix:** Implemented a login route, session management (`session['logged_in']`), and access control checks on all sensitive routes[cite: 60, 65].

### 2. Cross-Site Scripting (XSS) (CWE-79)
* [cite_start]**Vulnerability:** User input was rendered in `index.html` using the `|safe` filter, allowing malicious JavaScript (e.g., `<script>alert('XSS')</script>`) to execute in the browser[cite: 106, 110].
* [cite_start]**Fix:** Removed the `|safe` filter to allow Jinja2's auto-escaping mechanism to neutralize HTML tags[cite: 137].

### 3. SQL Injection (CWE-89)
* [cite_start]**Vulnerability:** The application used Python f-strings to construct raw SQL queries, allowing attackers to manipulate database commands[cite: 166, 170].
    * *Vulnerable Code:* `cursor.execute(f"INSERT ... VALUES ('{name}')")`
* [cite_start]**Fix:** Replaced raw queries with **parameterized queries** using `?` placeholders, ensuring inputs are treated as data, not executable code[cite: 191].

### 4. Cross-Site Request Forgery (CSRF) (CWE-352)
* [cite_start]**Vulnerability:** The application accepted POST requests without verification, allowing external sites to trigger unwanted actions on behalf of a logged-in user[cite: 209, 215].
* **Fix:** Integrated **Flask-WTF** and `CSRFProtect`. [cite_start]Added a `SECRET_KEY` and included hidden CSRF tokens in HTML forms[cite: 280, 285].

## 🛠️ Installation & Usage

1.  **Clone the repository**
    ```bash
    git clone [https://github.com/yourusername/flask-web-security-patching.git](https://github.com/yourusername/flask-web-security-patching.git)
    cd flask-web-security-patching
    ```

2.  **Set up Virtual Environment**
    ```bash
    python -m venv .venv
    # Windows
    .venv\Scripts\Activate
    # macOS/Linux
    source .venv/bin/activate
    ```

3.  **Install Dependencies**
    ```bash
    pip install flask flask_sqlalchemy flask_wtf
    ```

4.  **Run the Application**
    ```bash
    python app.py
    ```
    [cite_start]Access the app at `http://127.0.0.1:5000`[cite: 25].

## 💻 Tech Stack

* **Language:** Python
* **Framework:** Flask
* **Database:** SQLite / SQLAlchemy
* **Security Libraries:** Flask-WTF (CSRF Protection)

---
*Disclaimer: This project is for educational purposes to demonstrate secure coding practices.*

