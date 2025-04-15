
# 🧠 Django New Website Cheat Sheet

## 🚀 Project Setup
```bash
cd ~/code/projects
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
pipenv install django
pipenv shell
django-admin startproject config .
code .
```

## 🧱 Create an App
```bash
python3 manage.py startapp core
```
Add `'core'` to `INSTALLED_APPS` in `config/settings.py`.

---

## 🌐 URL Configuration

**config/urls.py**
```python
from django.urls import path, include

urlpatterns = [
    path('', include('core.urls')),
]
```

**core/urls.py**
```python
from . import views

urlpatterns = [
    path('', views.home, name='home'),
    path('about/', views.about, name='about'),
]
```

---

## 🎯 Views

**core/views.py**
```python
from django.shortcuts import render

def home(request):
    return render(request, 'home.html')

def about(request):
    return render(request, 'about.html')
```

---

## 🖼 Templates Setup

```bash
mkdir -p core/templates
```

**home.html**
```django
{% extends 'base.html' %}
{% block content %}
<h1>Welcome</h1>
{% endblock %}
```

**base.html**
```django
{% load static %}
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}My Site{% endblock %}</title>
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
</head>
<body>
    <nav>
        <a href="/">Home</a> | <a href="/about">About</a>
    </nav>
    {% block content %}{% endblock %}
</body>
</html>
```

---

## 🎨 Static Files

```bash
mkdir -p core/static/css
touch core/static/css/style.css
```

**settings.py**
```python
STATIC_URL = 'static/'
```

⚠️ Restart the server after adding static files.

---

## 🧩 Models

**core/models.py**
```python
from django.db import models

class Item(models.Model):
    name = models.CharField(max_length=100)
    description = models.TextField()
    price = models.DecimalField(max_digits=6, decimal_places=2)

    def __str__(self):
        return self.name
```

---

## 🐘 PostgreSQL Setup

```bash
pipenv install psycopg2-binary
createdb mysite
```

**settings.py**
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'mysite',
    }
}
```

---

## 🛠 Migrations

```bash
python3 manage.py makemigrations
python3 manage.py migrate
```

---

## 🐍 Django Shell CRUD

```bash
python3 manage.py shell
```

```python
from core.models import Item

# Create
i = Item(name='Book', description='...', price=9.99)
i.save()

# Read
Item.objects.all()

# Update
i = Item.objects.first()
i.name = 'Updated'
i.save()

# Delete
i.delete()
```

---

## 🔥 Run the Server

```bash
python3 manage.py runserver
```

Then open: [http://127.0.0.1:8000](http://127.0.0.1:8000)

---
