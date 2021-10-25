# Table of contents

|Read No. | Name of chapter|
|:---------: |:--------------:|
|28|[Django Settings Best Practices](Django-Settings-Best-Practices.md)
|28|[SSH Tutorial](SSH-Tutorial.md)









# Django Settings Best Practices

## Managing Django Settings: Issues
### **Different environments**. Usually, you have several environments: local, dev, ci, qa, staging, production, etc. Each environment can have its own specific settings (for example: DEBUG = True, more verbose logging, additional apps, some mocked data, etc). You need an approach that allows you to keep all these Django setting configurations.

### **Sensitive data**. You have SECRET_KEY in each Django project. On top of this there can be DB passwords and tokens for third-party APIs like Amazon or Twitter. This data cannot be stored in VCS.

### **Sharing settings between team members**. You need a general approach to eliminate human error when working with the settings. For example, a developer may add a third-party app or some API integration and fail to add specific settings. On large (or even mid-size) projects, this can cause real issues.

### **Django settings are a Python code**. This is a curse and a blessing at the same time. It gives you a lot of flexibility, but can also be a problem – instead of key-value pairs, settings.py can have a very tricky logic.

## Setting Configuration: Different Approaches
### There is no built-in universal way to configure Django settings without hardcoding them. But books, open-source and work projects provide a lot of recommendations and approaches on how to do it best. Let’s take a brief look at the most popular ones to examine their weaknesses and strengths.

### **settings_local.py**
### This is the oldest method. I used it when I was configuring a Django project on a production server for the first time. I saw a lot of people use it back in the day, and I still see it now.

### The basic idea of this method is to extend all environment-specific settings in the settings_local.py file, which is ignored by VCS. Here’s an example:

### settings.py file:
```python
ALLOWED_HOSTS = ['example.com']
DEBUG = False
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'production_db',
        'USER': 'user',
        'PASSWORD': 'password',
        'HOST': 'db.example.com',
        'PORT': '5432',
        'OPTIONS': {
            'sslmode': 'require'
        }
    }
}

...

from .settings_local import *
```
### settings_local.py file:
```python
ALLOWED_HOSTS = ['localhost']
DEBUG = True
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'local_db',
        'HOST': '127.0.0.1',
        'PORT': '5432',
    }
}
```
### Pros:
### Secrets not in VCS.
### Cons:
### settings_local.py is not in VCS, so you can lose some of your Django environment settings.

### The Django settings file is a Python code, so settings_local.py can have some non-obvious logic.
### You need to have settings_local.example (in VCS) to share the default configurations for developers.
### Separate settings file for each environment
### This is an extension of the previous approach. It allows you to keep all configurations in VCS and to share default settings between developers.

### In this case, you make a settings package with the following file structure:
```
settings/
   ├── __init__.py
   ├── base.py
   ├── ci.py
   ├── local.py
   ├── staging.py
   ├── production.py
   └── qa.py
```
### settings/local.py:
```python
from .base import *


ALLOWED_HOSTS = ['localhost']
DEBUG = True
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'local_db',
        'HOST': '127.0.0.1',
        'PORT': '5432',
    }
}
```

### To run a project with a specific configuration, you need to set an additional parameter:
```
python manage.py runserver --settings=settings.local
```
### Pros:
- All environments are in VCS.
- It’s easy to share settings between developers.
### Cons:
### You need to find a way to handle secret passwords and tokens.
### “Inheritance” of settings can be hard to trace and maintain.
### Environment variables
### To solve the issue with sensitive data, you can use environment variables.
```python
import os


SECRET_KEY = os.environ['SECRET_KEY']
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.environ['DATABASE_NAME'],
        'HOST': os.environ['DATABASE_HOST'],
        'PORT': int(os.environ['DATABASE_PORT']),
    }
}
```
### This is the simplest example using Python os.environ and it has several issues:

### You need to handle KeyError exceptions.
### You need to convert types manually (see DATABASE_PORT usage).
### To fix KeyError, you can write your own custom wrapper. For example:
```python
import os

from django.core.exceptions import ImproperlyConfigured


def get_env_value(env_variable):
    try:
      	return os.environ[env_variable]
    except KeyError:
        error_msg = 'Set the {} environment variable'.format(var_name)
        raise ImproperlyConfigured(error_msg)


SECRET_KEY = get_env_value('SECRET_KEY')
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': get_env_value('DATABASE_NAME'),
        'HOST': get_env_value('DATABASE_HOST'),
        'PORT': int(get_env_value('DATABASE_PORT')),
    }
}
```
### Also, you can set default values for this wrapper and add type conversion. But actually there is no need to write this wrapper, because you can use a third-party library (we’ll talk about this later).

### Pros:
- Configuration is separated from code.
- Environment parity – you have the same code for all environments.
- No inheritance in settings, and cleaner and more consistent ### code.
- There is a theoretical grounding for using environment - variables – 12 Factors.
### Cons:
### You need to handle sharing default config between developers.

## 12 Factors
### 12 Factors is a collection of recommendations on how to build distributed web-apps that will be easy to deploy and scale in the Cloud. It was created by Heroku, a well-known Cloud hosting provider.

### As the name suggests, the collection consists of twelve parts:

1- Codebase
2- Dependencies
3- Config
4- Backing services
5- Build, release, run
6- Processes
7- Port binding
8- Concurrency
9- Disposability
10- Dev/prod parity
11- Logs
12- Admin processes

## Setting Structure
### Instead of splitting settings by environments, you can split them by the source: Django, third- party apps (Celery, DRF, etc.), and your custom settings.

### File structure:
```
project/
├── apps/
├── settings/
│   ├── __init__.py
│   ├── djano.py
│   ├── project.py
│   └── third_party.py
└── manage.py
```
### __init__.py file:
```python
from .django import *       # All Django related settings
from .third_party import *  # Celery, Django REST Framework & other 3rd parties
from .project import *      # You custom settings
```
### Each module could be done as a package, and you can split it more granularly:
```
project/
├── apps/
├── settings/
│   ├── project
│   │   ├── __init__.py
│   │   ├── custom_module_foo.py
│   │   ├── custom_module_bar.py
│   │   └── custom_module_xyz.py
│   ├── third_party
│   │   ├── __init__.py
│   │   ├── celery.py
│   │   ├── email.py
│   │   └── rest_framework.py
│   ├── __init__.py
│   └── djano.py
└── manage.py
```


# SSH Tutorial

# How Does SSH Work
## What is SSH
### SSH, or Secure Shell, is a remote administration protocol that allows users to control and modify their remote servers over the Internet. The service was created as a secure replacement for the unencrypted Telnet and uses cryptographic techniques to ensure that all communication to and from the remote server happens in an encrypted manner. It provides a mechanism for authenticating a remote user, transferring inputs from the client to the host, and relaying the output back to the client.

## How Does SSH Work
### If you’re using Linux or Mac, then using SSH is very simple. If you use Windows, you will need to utilize an SSH client to open SSH connections. The most popular SSH client is PuTTY.

### For Mac and Linux users, head over to your terminal program and then follow the procedure below:

### The SSH command consists of 3 distinct parts:
```
ssh {user}@{host}
```
### The SSH key command instructs your system that you want to open an encrypted Secure Shell Connection. {user} represents the account you want to access. For example, you may want to access the root user, which is basically synonymous for system administrator with complete rights to modify anything on the system. {host} refers to the computer you want to access. This can be an IP Address (e.g. 244.235.23.19) or a domain name (e.g. www.xyzdomain.com).

### When you hit enter, you will be prompted to enter the password for the requested account. When you type it in, nothing will appear on the screen, but your password is, in fact being transmitted. Once you’re done typing, hit enter once again. If your password is correct, you will be greeted with a remote terminal window.

## Understanding Different Encryption Techniques
### The significant advantage offered by SSH over its predecessors is the use of encryption to ensure secure transfer of information between the host and the client. Host refers to the remote server you are trying to access, while the client is the computer you are using to access the host. There are three different encryption technologies used by SSH:

- Symmetrical encryption
- Asymmetrical encryption
- Hashing.

## Symmetric Encryption
### Symmetric encryption is a form of encryption where a secret key is used for both encryption and decryption of a message by both the client and the host. Effectively, any one possessing the key can decrypt the message being transferred.
## Asymmetric Encryption
### Unlike symmetrical encryption, asymmetrical encryption uses two separate keys for encryption and decryption. These two keys are known as the public key and the private key. Together, both these keys form a public-private key pair.
## Hashing
### One-way hashing is another form of cryptography used in Secure Shell Connections. One-way-hash functions differ from the above two forms of encryption in the sense that they are never meant to be decrypted. They generate a unique value of a fixed length for each input that shows no clear trend which can exploited. This makes them practically impossible to reverse.
