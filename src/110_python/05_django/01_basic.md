# Basic #
https://www.djangoproject.com/

Install Django
```bash
$pip install django==2.1
```

Create project
```bash
$django-admin startproject project_name .
```

Run server
```bash
$python manage.py runserver
```

Create sub app - it creates new package on folder structure
```bash
$python manage.py startapp app_name
```

On new app package go to file views.py  
Create basin url index
Returning test to the browser
```python
from django.http import HttpResponse
from django.shortcuts import render


def index(request): 
     return HttpResponse('Hello World')
```

### URL MAPPING ###
/products -> index function 
```python
from django.http import HttpResponse
from django.shortcuts import render


def index(request): 
     return HttpResponse('Hello World')
```