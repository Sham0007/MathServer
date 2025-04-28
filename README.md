# Ex.05 Design a Website for Server Side Processing
## Date: 28/04/2025

## AIM:
 To design a website to calculate the power of a lamp filament in an incandescent bulb in the server side. 


## FORMULA:
P = I<sup>2</sup>R
<br> P --> Power (in watts)
<br> I --> Intensity
<br> R --> Resistance

## DESIGN STEPS:

### Step 1:
Clone the repository from GitHub.

### Step 2:
Create Django Admin project.

### Step 3:
Create a New App under the Django Admin project.

### Step 4:
Create python programs for views and urls to perform server side processing.

### Step 5:
Create a HTML file to implement form based input and output.

### Step 6:
Publish the website in the given URL.

## PROGRAM :
```
views.py



from django.shortcuts import render

def lamp(request):
    context={}
    context['Power'] = ""
    context['I'] = ""
    context['R'] = ""
    if request.method == 'POST':
        print("POST method is used")
        I = request.POST.get('Intensity','')
        R = request.POST.get('Resistence','')
        print('request=',request)
        print('Intensity=',I)
        print('Resistence=',R)
        Power = int(I) * int(I) * int(R)
        context['Power'] = Power
        context['I'] = I
        context['R'] = R
        print('Power=',Power)
    return render(request,'Calculation.html',context)


Calculation.html



<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Incandescent Bulb Power Calculator</title>
    <style>
        /* Reset */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background-color: #f4f4f9;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            color: #333;
            font-size: 16px;
            overflow: hidden;
        }

        .container {
            background-color: #fff;
            padding: 40px 50px;
            border-radius: 15px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 600px;
            transition: all 0.3s ease;
        }

        .container:hover {
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.2);
        }

        h1 {
            text-align: center;
            font-size: 28px;
            color: #4CAF50;
            margin-bottom: 20px;
            font-weight: bold;
        }

        .form-group {
            margin-bottom: 25px;
        }

        label {
            font-size: 18px;
            margin-bottom: 10px;
            display: block;
            color: #333;
        }

        input {
            width: 100%;
            padding: 15px;
            font-size: 18px;
            border: 1px solid #ddd;
            border-radius: 10px;
            background-color: #f9f9f9;
            margin-top: 8px;
            transition: all 0.3s ease;
        }

        input:focus {
            border-color: #4CAF50;
            background-color: #fff;
        }

        .btn {
            width: 100%;
            padding: 15px;
            background-color: #4CAF50;
            color: #fff;
            font-size: 20px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: background-color 0.3s ease;
            margin-top: 20px;
        }

        .btn:hover {
            background-color: #45a049;
        }

        .result-box {
            background-color: #e1f5e1;
            padding: 20px;
            border-radius: 10px;
            margin-top: 20px;
            text-align: center;
            font-size: 20px;
            font-weight: bold;
            color: #333;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
        }

        .footer {
            position: absolute;
            bottom: 20px;
            width: 100%;
            text-align: center;
            font-size: 14px;
            color: #555;
        }

        .footer a {
            color: #4CAF50;
            text-decoration: none;
            font-weight: bold;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Incandescent Bulb Power Calculator</h1>
    <form method="POST">
        {% csrf_token %}
        <div class="form-group">
            <label for="intensity">Enter Intensity (I) in Amperes:</label>
            <input type="text" id="intensity" name="Intensity" value="{{I}}" placeholder="Enter intensity" required>
        </div>
        <div class="form-group">
            <label for="resistance">Enter Resistance (R) in Ohms:</label>
            <input type="text" id="resistance" name="Resistence" value="{{R}}" placeholder="Enter resistance" required>
        </div>
        <button type="submit" class="btn">Calculate</button>
        <div class="result-box">
            <label for="power">Power:</label>
            <input  id="power" name="Power" value="                                   {{ Power}} Watts" readonly> 
        </div>
    </form>
</div>

<div class="footer">
    <p>&copy; 2024 Power Calculator. All rights reserved</p>
</div>

</body>
</html>



settings.py



from pathlib import Path
import os

BASE_DIR = Path(__file__).resolve().parent.parent

SECRET_KEY = 'django-insecure-e02v^$2so$xt&qztr@^^%cbm)^#k2x*tcbg3_=$@4(esyagui8'

DEBUG = True

ALLOWED_HOSTS = []

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'servercal',
]

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

ROOT_URLCONF = 'cal.urls'

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

WSGI_APPLICATION = 'cal.wsgi.application'

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}

AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
    },
]

LANGUAGE_CODE = 'en-us'

TIME_ZONE = 'UTC'

USE_I18N = True

USE_TZ = True
STATIC_URL = 'static/'

DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'



urls.py



from django.contrib import admin
from django.urls import path
from servercal import views
urlpatterns = [
    path('admin/', admin.site.urls),
    path('PowerOfLampFilamentInAnIncandescentBulb/',views.lamp,name="PowerOfLampFilamentInAnIncandescentBulb"),
    path('',views.lamp,name="PowerOfLampFilamentInAnIncandescentBulb")
]
```


## SERVER SIDE PROCESSING:

![image](https://github.com/user-attachments/assets/1c7a1e67-2cb5-43d1-a7bd-2147aecb3e7e)


## HOMEPAGE:

![image](https://github.com/user-attachments/assets/119d8387-322c-497f-8b62-c82b9bc714bd)


## RESULT:
The program for performing server side processing is completed successfully.
