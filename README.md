# django-for-beginners

Welcome to the Django for beginners! In this tutorial, we will walk through building a simple web application using Django. We'll cover the essential concepts. By following this hands-on approach, you'll gain understanding of Django's core features. Let's get started!

## Step 1: Setting Up the Project

Install Python: Follow the official Python installation guide for your operating system.

**Create a Virtual Environment:**

Open your terminal and run the following commands:

```
python3 -m venv myenv
```

```
source myenv/bin/activate
```

**Install Django:**

Run the command in your virtual environment to install Django.
```
pip install django
```

To check installation
```
python3 -m django --version
```

**Create a Django Project:**

Run 

```
django-admin startproject myproject
```
To create a new Django project named ``` myproject ```.

## Step 2: Creating and Configuring the Database

**Configure Database Settings:**

Open ``` myproject/settings.py ``` and configure the database settings according to your needs (e.g., SQLite, MySQL, PostgreSQL).

**Create Database Tables:**

Run 

```
python3 manage.py migrate
```

to create the necessary database tables.

## Step 3: Building Models and Database Relationships

**Define Models:**

Create a new file called ``` models.py ``` in your project's main directory. 

Define your models using Django's model syntax, including fields and relationships.

```

from django.db import models

class Category(models.Model):
    name = models.CharField(max_length=100)

class Product(models.Model):
    name = models.CharField(max_length=100)
    price = models.DecimalField(max_digits=8, decimal_places=2)
    category = models.ForeignKey(Category, on_delete=models.CASCADE)
    
```

**Register Models:**

Open ``` myproject/admin.py ``` and register your models to make them accessible via the Django admin interface.

```

from django.contrib import admin
from .models import Category, Product

admin.site.register(Category)
admin.site.register(Product)

```

## Step 4: Creating Views and Templates

**Create Views:**

In your project's main directory, create a new file called ``` views.py ```. 

Define your views using functions or classes.

```

from django.shortcuts import render
from .models import Category, Product

def product_list(request):
    products = Product.objects.all()
    return render(request, 'product_list.html', {'products': products})
    
```

**Create Templates:**

Create a new directory called ``` templates ``` in your project's main directory. 

Inside the templates directory, create a file called ``` product_list.html ``` and define the HTML template.

```

<!DOCTYPE html>
<html>
  <head>
      <title>Product List</title>
  </head>
  <body>
      <h1>Product List</h1>
      <ul>
          {% for product in products %}
              <li>{{ product.name }} - ${{ product.price }}</li>
          {% endfor %}
      </ul>
  </body>
</html>

```

## Step 5: Configuring URLs and Routing

**Create URL Patterns:**

Open ``` myproject/urls.py ``` and define your URL patterns, mapping them to the appropriate views.

```

from django.urls import path
from .views import product_list

urlpatterns = [
    path('products/', product_list, name='product_list'),
]

```

## Step 6: Running the Development Server

**Start the Development Server:**

In your terminal, run below command to start the Django development server.

```
python manage.py runserver 
```

**Access the Web Application:**

Open your web browser and navigate to ``` http://localhost:8000/products/ ``` to see the product list page rendered.

## Step 7: Adding User Authentication

**Enable Authentication URLs:**

Open ``` myproject/urls.py ``` and add the authentication URLs provided by Django.

```

from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('accounts/', include('django.contrib.auth.urls')),
    # other URL patterns
]

```

**Create User Registration View:**

Create a new file called ``` views.py ``` in your project's main directory and define a view for user registration.

```

from django.shortcuts import render, redirect
from django.contrib.auth.forms import UserCreationForm

def register(request):
    if request.method == 'POST':
        form = UserCreationForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('product_list')
    else:
        form = UserCreationForm()
    return render(request, 'registration/register.html', {'form': form})
    
```    

**Create Registration Template:**

Create a new directory called ``` registration ``` inside the ``` templates ``` directory. 

Inside the registration directory, create a file called ``` register.html ``` and define the registration form template.

```

<!DOCTYPE html>
<html>
<head>
    <title>User Registration</title>
</head>
<body>
    <h1>User Registration</h1>
    <form method="POST">
        {% csrf_token %}
        {{ form.as_p }}
        <button type="submit">Register</button>
    </form>
</body>
</html>

```

**Update URL Patterns:**

Open ``` myproject/urls.py ``` and add a URL pattern for the user registration view.

```

from .views import register

urlpatterns = [
    # existing URL patterns
    path('accounts/register/', register, name='register'),
]

```

## Conclusion

Congratulations on completing the practical Django tutorial for beginners! You've built a simple web application with database models, views, templates, URL routing, and user authentication. This hands-on approach should have provided you with a foundation in Django development. Keep exploring Django's extensive features and consider building more complex projects to further enhance your skills. 

**Happy coding!**

## Step 8: Further Learning

**Django Documentation:**

The official Django documentation is an excellent resource to explore in-depth explanations, tutorials, and reference materials. Visit the Django documentation website at [https://docs.djangoproject.com/](https://docs.djangoproject.com/) to access the latest documentation.

**Django for Beginners:**

A step-by-step guidebook written by William S. Vincent that covers the basics of Django development. It provides hands-on examples and practical explanations for beginners. You can find it at [https://djangoforbeginners.com/](https://djangoforbeginners.com/).

**Django Girls Tutorial:**

Django Girls offers a beginner-friendly tutorial that walks you through building a simple web application using Django. It provides clear instructions and code examples. Access the tutorial at [https://tutorial.djangogirls.org/](https://tutorial.djangogirls.org/).

**DjangoCon Videos:**

DjangoCon is an annual conference focused on Django and web development. The conference features talks and presentations by industry experts. You can find recorded videos from past DjangoCon events on YouTube and the official DjangoCon website.

**Django Project's YouTube Channel:**

The Django Project maintains a YouTube channel where you can find video tutorials, talks, and interviews related to Django. Visit the channel at [https://www.youtube.com/user/django](https://www.youtube.com/user/django).

**Two Scoops of Django:**

A comprehensive book by Daniel Roy Greenfeld and Audrey Roy Greenfeld that provides best practices, tips, and techniques for Django development. It covers various topics and advanced concepts. Find it at [https://www.twoscoopspress.com/products/two-scoops-of-django-3-x](https://www.twoscoopspress.com/products/two-scoops-of-django-3-x).

**Django Reddit and Forum:**

Engage with the Django community through platforms like the Django subreddit [https://www.reddit.com/r/django/](https://www.reddit.com/r/django/) and the Django forum [https://forum.djangoproject.com/](https://forum.djangoproject.com/). Participate in discussions, ask questions, and learn from other Django developers.

**Django Packages:**

Explore the Django Packages website [https://djangopackages.org/](https://djangopackages.org/) to discover and explore a wide range of Django packages and libraries. It's a valuable resource to find pre-built solutions for common functionalities.

***Remember, practice is key to mastering Django. Work on personal projects, contribute to open-source projects, and experiment with different features and techniques. Stay up-to-date with the latest Django releases and advancements in the Django ecosystem.*** 

### Happy learning!
