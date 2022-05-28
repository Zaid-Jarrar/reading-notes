# Reading 33 - Authentication & Production Server

## What is a JSON Web Token?

**JSON Web Token**(JWT) - compact and self contained way for secure transmitting information between parties as a JSON object

## When should you use JWT?

**Authorization** - common way of using JWT. The user is logged in, each following request will include JWT.

Authorization allows user to access:
1.routes
2.services
3.resources

**Information Exchange** - JWT good way of transferring information between parties.

## JSON Web Token Structure?

consists of three parts separated by dots ( . ):

-Header
-Payload
-Signature

ie `xxxxx.yyyyy.zzzzz`

**Header** - consists of two parts:
-type of token
-signing algorithm being used.

```python
{
  "alg": "HS256",
  "typ": "JWT"
}
```

**Payload** - contains claims
  **claims** - statements about an entity and additional data.

*3 types of claims:*

**Registered claims** - set of predefined claims that aren't mandatory and provide interoperable claims.

**Public claims** - defined at will by using JWTs

**Private claims** - custom claims made to share information between parties.

payload

```python
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```

**Signature** - take encoded header, encoded payload a secret, the algorithm specified in the header and sign that.

```python

HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)

```

### How to Use JWT

1. Application your clients requests authorization to the authentication server.
-Performed through a form of authorization flows

2.Authorization granted, authorization server returns access token to the application

3.Application uses access token to access protected resource

```python
curl http://127.0.0.1:8000/hello/ -H 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNTQzODI4NDMxLCJqdGkiOiI3ZjU5OTdiNzE1MGQ0NjU3OWRjMmI0OTE2NzA5N2U3YiIsInVzZXJfaWQiOjF9.Ju70kdcaHKn1Qaz8H42zrOYk0Jx9kIckTn9Xx7vhikY'
```

### Installation and Setup

`pip install djangorestframework_simplejwt`

in settings.py:

```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    ],
}
```

in urls.py:

```python
from django.urls import path
from rest_framework_simplejwt import views as jwt_views

urlpatterns = [
    # Your URLs...
    path('api/token/', jwt_views.TokenObtainPairView.as_view(), name='token_obtain_pair'),
    path('api/token/refresh/', jwt_views.TokenRefreshView.as_view(), name='token_refresh'),
]
```

### Django Runserver Is Not Your Production Server

Through *production stack*:
-consists of multiple components, and is talented at one specific thing.

**dedicated web server** - request passed through this web server when presented at the server.

**application server** - gets requests and constructs Python objects which are usable by Django.

### How Django Fit in?

`uwsgi.py` - contains function to be called by application server.
-function calls code then produces a response object which is passed to the WSGI server.