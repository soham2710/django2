# 🧮 Django Calculator App with Jinja Templates & Railway Deployment

This project is a **simple calculator web app built using Django**. It demonstrates:

* Django fundamentals (views, templates, forms)
* Jinja templating (`base.html` & `index.html`)
* Environment configuration using `.env`
* Deployment to [Railway](https://railway.app)

---

## 📁 Project Structure

```
calculator_project/
│
├── calculator/                 # Main app
│   ├── templates/
│   │   ├── base.html           # Base layout
│   │   └── index.html          # Calculator form & result
│   ├── views.py                # Calculator logic
│   └── urls.py                 # App-specific routing
│
├── calculator_project/         # Django project
│   ├── settings.py             # Settings (using .env)
│   ├── urls.py                 # Main URL routing
│   └── wsgi.py                 # WSGI for deployment
│
├── manage.py
├── requirements.txt
├── Procfile                    # For Railway deployment
├── runtime.txt                 # Python version
├── .gitignore
└── .env                        # Environment variables (not committed)
```

---

## ⚙️ Features

* Add, subtract, multiply, divide
* Jinja template inheritance
* Form handling with POST & CSRF
* Dynamic rendering of results
* Railway deployment-ready

---

## 🛠️ Setup Instructions

### 1. 📦 Clone and Setup Virtual Environment

```bash
git clone https://github.com/yourusername/calculator_project.git
cd calculator_project
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install -r requirements.txt
```

---

### 2. ⚙️ Configure `.env`

Create a `.env` file in the project root:

```
SECRET_KEY=your-very-secret-key
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
```

> Make sure `.env` is **in your `.gitignore`**!

---

### 3. 🔧 Update `settings.py`

Make sure you have this at the top:

```python
from decouple import config

SECRET_KEY = config('SECRET_KEY')
DEBUG = config('DEBUG', cast=bool)
ALLOWED_HOSTS = config('ALLOWED_HOSTS').split(',')
```

---

### 4. 🔌 Run the App Locally

```bash
python manage.py migrate
python manage.py runserver
```

Visit: [http://127.0.0.1:8000](http://127.0.0.1:8000)

---

## 📄 Jinja Templates

### `base.html`

```html
<!DOCTYPE html>
<html>
<head>
    <title>Django Calculator</title>
</head>
<body>
    <h1>Simple Calculator</h1>
    {% block content %}{% endblock %}
</body>
</html>
```

---

### `index.html`

```html
{% extends 'base.html' %}

{% block content %}
<form method="POST">
    {% csrf_token %}
    <input type="number" name="num1" placeholder="First Number" required>
    <input type="number" name="num2" placeholder="Second Number" required><br><br>

    <button type="submit" name="operation" value="add">Add</button>
    <button type="submit" name="operation" value="subtract">Subtract</button>
    <button type="submit" name="operation" value="multiply">Multiply</button>
    <button type="submit" name="operation" value="divide">Divide</button>
</form>

{% if result is not None %}
    <h2>Result: {{ result }}</h2>
{% endif %}
{% endblock %}
```

---

## 🚀 Deployment on Railway

### 1. ✅ Prepare Files for Railway

Make sure these files exist at the root:

* `Procfile`

  ```text
  web: gunicorn calculator_project.wsgi
  ```
* `requirements.txt`
  (Run `pip freeze > requirements.txt`)
* `runtime.txt`

  ```text
  python-3.11.8
  ```

---

### 2. 🆙 Push to GitHub

```bash
git init
git add .
git commit -m "Initial calculator project"
git branch -M main
git remote add origin https://github.com/yourusername/calculator_project.git
git push -u origin main
```

---

### 3. 🌐 Deploy via Railway

1. Go to [https://railway.app](https://railway.app)
2. Create a new project → **Deploy from GitHub**
3. Choose your repository
4. In the Railway dashboard:

   * Go to **Variables**
   * Add your `.env` variables:

     ```
     SECRET_KEY=your-very-secret-key
     DEBUG=False
     ALLOWED_HOSTS=your-subdomain.up.railway.app
     ```
5. Click **Deploy**

---

## 🧪 Troubleshooting

| Issue                          | Solution                                                      |
| ------------------------------ | ------------------------------------------------------------- |
| `No start command found`       | Add `Procfile` with `web: gunicorn calculator_project.wsgi`   |
| `DisallowedHost` error         | Set correct `ALLOWED_HOSTS` in `.env` or `settings.py`        |
| Railway can’t detect the build | Ensure `requirements.txt`, `Procfile` are at the project root |

---

## 🧑‍🏫 Teaching Notes

This project is perfect to demonstrate:

| Concept            | How It's Used                     |
| ------------------ | --------------------------------- |
| Views & Forms      | `views.py`, HTML form, POST data  |
| Templating         | `base.html`, `index.html`, blocks |
| CSRF Protection    | `{% csrf_token %}`                |
| Environment Config | `.env`, `python-decouple`         |
| Deployment         | GitHub + Railway + Procfile       |

Encourage students to:

* Add new operations (e.g. modulus)
* Style with CSS or Bootstrap
* Separate form logic using Django Forms (advanced)

---

## 📜 License

MIT License

---

Would you like me to bundle this whole thing into a ready-to-deploy ZIP including the working `.env.example` file and all templates?
