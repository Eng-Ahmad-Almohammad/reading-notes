# Table of contents

|Read No. | Name of chapter|
|:---------: |:--------------:|
|27|[JSON Web Tokens](JSON-Web-Tokens.md)
|27|[DRF JWT Authentication](DRF-JWT-Authentication.md)











# JSON Web Tokens

## What is JSON Web Token?

### JSON Web Token (JWT) is an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed.

## When should you use JSON Web Tokens?
### Here are some scenarios where JSON Web Tokens are useful:

- **Authorization:** This is the most common scenario for using JWT. Once the user is logged in, each subsequent request will include the JWT, allowing the user to access routes, services, and resources that are permitted with that token.

- **Information Exchange:** JSON Web Tokens are a good way of securely transmitting information between parties. Because JWTs can be signed—for example, using public/private key pairs—you can be sure the senders are who they say they are. Additionally, as the signature is calculated using the header and the payload, you can also verify that the content hasn't been tampered with.

## What is the JSON Web Token structure?
### In its compact form, JSON Web Tokens consist of three parts separated by dots (.), which are:

- Header
- Payload
- Signature
### Therefore, a JWT typically looks like the following.

### xxxxx.yyyyy.zzzzz

### **Header**
### The header typically consists of two parts: the type of the token, which is JWT, and the signing algorithm being used, such as HMAC SHA256 or RSA.
```
For example:

{
  "alg": "HS256",
  "typ": "JWT"
}
```
### **Payload**
### The second part of the token is the payload, which contains the claims. Claims are statements about an entity (typically, the user) and additional data. There are three types of claims:
- **Registered claims:** These are a set of predefined claims which are not mandatory but recommended, to provide a set of useful, interoperable claims. Some of them are: iss (issuer), exp (expiration time), sub (subject), aud (audience),
- **Public claims:** These can be defined at will by those using JWTs. But to avoid collisions they should be defined in the IANA JSON Web Token Registry or be defined as a URI that contains a collision resistant namespace.

- **Private claims:** These are the custom claims created to share information between parties that agree on using them and are neither registered or public claims.

### An example payload could be:
```
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```

### **Signature**
### To create the signature part you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.

### For example if you want to use the HMAC SHA256 algorithm, the signature will be created in the following way:
```
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```

### The signature is used to verify the message wasn't changed along the way, and, in the case of tokens signed with a private key, it can also verify that the sender of the JWT is who it says it is.

## How do JSON Web Tokens work?
### In authentication, when the user successfully logs in using their credentials, a JSON Web Token will be returned. Since tokens are credentials, great care must be taken to prevent security issues. In general, you should not keep tokens longer than required.

### You also should not store sensitive session data in browser storage due to lack of security.

### Whenever the user wants to access a protected route or resource, the user agent should send the JWT, typically in the Authorization header using the Bearer schema. The content of the header should look like the following:
```
Authorization: Bearer <token>
```
### This can be, in certain cases, a stateless authorization mechanism. The server's protected routes will check for a valid JWT in the Authorization header, and if it's present, the user will be allowed to access protected resources. If the JWT contains the necessary data, the need to query the database for certain operations may be reduced, though this may not always be the case.

### If the token is sent in the Authorization header, Cross-Origin Resource Sharing (CORS) won't be an issue as it doesn't use cookies.

## Why should we use JSON Web Tokens?
### Let's talk about the benefits of JSON Web Tokens (JWT) when compared to Simple Web Tokens (SWT) and Security Assertion Markup Language Tokens (SAML).

### As JSON is less verbose than XML, when it is encoded its size is also smaller, making JWT more compact than SAML. This makes JWT a good choice to be passed in HTML and HTTP environments.

### Security-wise, SWT can only be symmetrically signed by a shared secret using the HMAC algorithm. However, JWT and SAML tokens can use a public/private key pair in the form of a X.509 certificate for signing. Signing XML with XML Digital Signature without introducing obscure security holes is very difficult when compared to the simplicity of signing JSON.

### JSON parsers are common in most programming languages because they map directly to objects. Conversely, XML doesn't have a natural document-to-object mapping. This makes it easier to work with JWT than SAML assertions.





# DRF JWT Authentication
## How JWT Works?
### The JWT is just an authorization token that should be included in all requests:
```
curl http://127.0.0.1:8000/hello/ -H 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNTQzODI4NDMxLCJqdGkiOiI3ZjU5OTdiNzE1MGQ0NjU3OWRjMmI0OTE2NzA5N2U3YiIsInVzZXJfaWQiOjF9.Ju70kdcaHKn1Qaz8H42zrOYk0Jx9kIckTn9Xx7vhikY'
```
### The JWT is acquired by exchanging an username + password for an access token and an refresh token.

### The access token is usually short-lived (expires in 5 min or so, can be customized though).

### The refresh token lives a little bit longer (expires in 24 hours, also customizable). It is comparable to an authentication session. After it expires, you need a full login with username + password again.

## Why is that?

### It’s a security feature and also it’s because the JWT holds a little bit more information. If you look closely the example I gave above, you will see the token is composed by three parts:
```
xxxxx.yyyyy.zzzzz
```
### Those are three distinctive parts that compose a JWT:
```
header.payload.signature
```
### So we have here:
```
header = eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9
payload = eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNTQzODI4NDMxLCJqdGkiOiI3ZjU5OTdiNzE1MGQ0NjU3OWRjMmI0OTE2NzA5N2U3YiIsInVzZXJfaWQiOjF9
signature = Ju70kdcaHKn1Qaz8H42zrOYk0Jx9kIckTn9Xx7vhikY
```
### This information is encoded using Base64. If we decode, we will see something like this:
### **header**
```


{
  "typ": "JWT",
  "alg": "HS256"
}
```

### **payload**
```
{
  "token_type": "access",
  "exp": 1543828431,
  "jti": "7f5997b7150d46579dc2b49167097e7b",
  "user_id": 1
}
```
### **signature**

### The signature is issued by the JWT backend, using the header base64 + payload base64 + SECRET_KEY. Upon each request this signature is verified. If any information in the header or in the payload was changed by the client it will invalidate the signature. The only way of checking and validating the signature is by using your application’s SECRET_KEY. 

## Installation & Setup
### For this tutorial we are going to use the djangorestframework_simplejwt library, recommended by the DRF developers.
```
pip install djangorestframework_simplejwt
```
### **settings.py**
```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    ],
}
```
### **urls.py**
```python
from django.urls import path
from rest_framework_simplejwt import views as jwt_views

urlpatterns = [
    # Your URLs...
    path('api/token/', jwt_views.TokenObtainPairView.as_view(), name='token_obtain_pair'),
    path('api/token/refresh/', jwt_views.TokenRefreshView.as_view(), name='token_refresh'),
]
```
## Example Code


### views.py
```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework.permissions import IsAuthenticated


class HelloView(APIView):
    permission_classes = (IsAuthenticated,)

    def get(self, request):
        content = {'message': 'Hello, World!'}
        return Response(content)

```
### urls.py
```python
from django.urls import path
from myapi.core import views

urlpatterns = [
    path('hello/', views.HelloView.as_view(), name='hello'),
]
```
## Obtain Token
### First step is to authenticate and obtain the token. The endpoint is /api/token/ and it only accepts POST requests.
```
http post http://127.0.0.1:8000/api/token/ username=vitor password=123
```
### So basically your response body is the two tokens:
```
{
    "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNTQ1MjI0MjU5LCJqdGkiOiIyYmQ1NjI3MmIzYjI0YjNmOGI1MjJlNThjMzdjMTdlMSIsInVzZXJfaWQiOjF9.D92tTuVi_YcNkJtiLGHtcn6tBcxLCBxz9FKD3qzhUg8",
    "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTU0NTMxMDM1OSwianRpIjoiMjk2ZDc1ZDA3Nzc2NDE0ZjkxYjhiOTY4MzI4NGRmOTUiLCJ1c2VyX2lkIjoxfQ.rA-mnGRg71NEW_ga0sJoaMODS5ABjE5HnxJDb0F8xAo"
}
```
### After that you are going to store both the access token and the refresh token on the client side, usually in the localStorage.

### In order to access the protected views on the backend (i.e., the API endpoints that require authentication), you should include the access token in the header of all requests, like this:
```
http http://127.0.0.1:8000/hello/ "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNTQ1MjI0MjAwLCJqdGkiOiJlMGQxZDY2MjE5ODc0ZTY3OWY0NjM0ZWU2NTQ2YTIwMCIsInVzZXJfaWQiOjF9.9eHat3CvRQYnb5EdcgYFzUyMobXzxlAVh_IAgqyvzCE"
```
### You can use this access token for the next five minutes.

### After five min, the token will expire, and if you try to access the view again, you are going to get the following error:
```
http http://127.0.0.1:8000/hello/ "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNTQ1MjI0MjAwLCJqdGkiOiJlMGQxZDY2MjE5ODc0ZTY3OWY0NjM0ZWU2NTQ2YTIwMCIsInVzZXJfaWQiOjF9.9eHat3CvRQYnb5EdcgYFzUyMobXzxlAVh_IAgqyvzCE"
```
![image](images/tokens.PNG)
## Refresh Token
### To get a new access token, you should use the refresh token endpoint /api/token/refresh/ posting the refresh token:
```
http post http://127.0.0.1:8000/api/token/refresh/ refresh=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTU0NTMwODIyMiwianRpIjoiNzAyOGFlNjc0ZTdjNDZlMDlmMzUwYjg3MjU1NGUxODQiLCJ1c2VyX2lkIjoxfQ.Md8AO3dDrQBvWYWeZsd_A1J39z6b6HEwWIUZ7ilOiPE
```
### The return is a new access token that you should use in the subsequent requests.

### The refresh token is valid for the next 24 hours. When it finally expires too, the user will need to perform a full authentication again using their username and password to get a new set of access token + refresh token.
