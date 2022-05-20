# Django REST Framework and Docker


## Django REST Framework
Reading from [DRF](https://realpython.com/django-rest-framework-quick-start/)

Django REST Framework works alongside the Django web framework to create web APIs. We cannot build a web API with only Django Rest Framework. It always must be added to a project after Django itself has been installed and configured.
The most important takeaway is that **Django** creates websites containing webpages, while **Django REST** Framework creates web APIs which are a collection of URL endpoints containing available HTTP verbs that return JSON.


### DRF setup
Install:

$ pip install djangorestframework
$ pip freeze > requirements.txt
Update settings.py:
```
INSTALLED_APPS = (
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'talk',
    'rest_framework'
)
```

In a RESTful API, endpoints (URLs) define the structure of the API and how end users access data from our application using the HTTP methods: GET, POST, PUT, DELETE. Endpoints should be logically organized around collections and elements, both of which are resources.


## Model Serializer
DRF’s Serializers convert model instances to Python dictionaires, which can then be rendered in various API appropriate formats - like JSON or XML. Similar to the Django ModelForm class, DRF comes with a concise format for its Serializers, the ModelSerializer class. It’s simple to use: Just tell it which fields you want to use from the model:
```
from rest_framework import serializers
from talk.models import Post


class PostSerializer(serializers.ModelSerializer):

    class Meta:
        model = Post
        fields = ('id', 'author', 'text', 'created', 'updated')
```

## **Docker**: 
is a way to isolate and run entire applications.

Reading from [Dockor](https://wsvincent.com/beginners-guide-to-docker/)
### Docker advantages:
- The entire development environment is isolated: programming language, software packages, databases, and more.
- With Docker we now longer have to mess around with virtual environments. We can faithfully reproduce a production environment locally
- Docker can be shared among team members so everyone is working on the same setup
  
### Docker disadvantages:
- Complexity. Docker is a complex beast under the hood.
  
## Linux Containers
Docker is really just Linux containers which are a type of **virtualization**.

**Virtualization** has its roots at the beginning of computer science when large, expensive mainframe computers were the norm. How could multiple programmers use the same single machine? The answer was virtualization and specifically virtual machines which are complete copies of a computer system from the operating system on up.

### Downside to a virtual machine:
Size and speed. A typical guest operating system can easily take up 700MB of size. So if one physical server supports three virtual machines, that’s at least 2.1GB of disk space taken up along with separate needs for CPU and memory resources.

Linux containers, also known as “containerization,” has become increasingly popular. For most applications, a virtual machine provides far more resources than are needed and a container is more than sufficient.

This, fundamentally, is what Docker is. A way to implement Linux containers!


## Containers vs Virtual Environments

Virtual environments are used to isolate Python software packages locally. We can create an isolated box for individual projects so one can use Python 2.7 and Django 1.5 while another can use Python 3.5 and Django 2.1 on the same computer. Virtual environments are great.

But…virtual environments can only isolate Python packages. They still rely on a global, system-level installation of Python albeit they can refer to the proper version. So when we use Python 2.7 in a project, we’re pointing to an installation of Python 2.7 on the computer itself, not actually within the virtual environment.

Also we can’t run a production database or other services within virtual environments so compared to Docker containers they are far more limited.