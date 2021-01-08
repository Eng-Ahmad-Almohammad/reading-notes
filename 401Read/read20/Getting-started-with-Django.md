# Intro to Django
## Object-relational mapper
### **Models**
### A model is the single, definitive source of information about your data. It contains the essential fields and behaviors of the data you’re storing. Generally, each model maps to a single database table.

### The basics:

- Each model is a Python class that subclasses django.db.models.Model.
- Each attribute of the model represents a database field.
- With all of this, Django gives you an automatically-generated database-access API.

```python
from django.db import models

class Person(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30)
```

### first_name and last_name are fields of the model. Each field is specified as a class attribute, and each attribute maps to a database column.

### **Using models**
### Once you have defined your models, you need to tell Django you’re going to use those models. Do this by editing your settings file and changing the INSTALLED_APPS setting to add the name of the module that contains your models.py.

### For example, if the models for your application live in the module myapp.models (the package structure that is created for an application by the manage.py startapp script), INSTALLED_APPS should read, in part:

```python
INSTALLED_APPS = [
    #...
    'myapp',
    #...
]
```
### **Field types**
### Each field in your model should be an instance of the appropriate Field class. Django uses the field class types to determine a few things:

- The column type, which tells the database what kind of data to store (e.g. INTEGER, VARCHAR, TEXT).
- The default HTML widget to use when rendering a form field (e.g. <input type="text">, <select>).
- The minimal validation requirements, used in Django’s admin and in automatically-generated forms.

### Field options
### Each field takes a certain set of field-specific arguments. For example, CharField (and its subclasses) require a max_length argument which specifies the size of the VARCHAR database field used to store the data.

### There’s also a set of common arguments available to all field types. All are optional. Here’s a quick summary of the most often-used ones:

### null
### If True, Django will store empty values as NULL in the database. Default is False.
### blank
### If True, the field is allowed to be blank. Default is False.

### Note that this is different than null. null is purely database-related, whereas blank is validation-related. If a field has blank=True, form validation will allow entry of an empty value. If a field has blank=False, the field will be required.

### choices
### A sequence of 2-tuples to use as choices for this field. If this is given, the default form widget will be a select box instead of the standard text field and will limit choices to the choices given.

### A choices list looks like this:
```python
YEAR_IN_SCHOOL_CHOICES = [
    ('FR', 'Freshman'),
    ('SO', 'Sophomore'),
    ('JR', 'Junior'),
    ('SR', 'Senior'),
    ('GR', 'Graduate'),
]
```
### The first element in each tuple is the value that will be stored in the database. The second element is displayed by the field’s form widget.
### Given a model instance, the display value for a field with choices can be accessed using the get_FOO_display() method. For example:
```python
from django.db import models

class Person(models.Model):
    SHIRT_SIZES = (
        ('S', 'Small'),
        ('M', 'Medium'),
        ('L', 'Large'),
    )
    name = models.CharField(max_length=60)
    shirt_size = models.CharField(max_length=1, choices=SHIRT_SIZES)
```
```python
>>> p = Person(name="Fred Flintstone", shirt_size="L")
>>> p.save()
>>> p.shirt_size
'L'
>>> p.get_shirt_size_display()
'Large'
```
### default
### The default value for the field. This can be a value or a callable object. If callable it will be called every time a new object is created.
### help_text
### Extra “help” text to be displayed with the form widget. It’s useful for documentation even if your field isn’t used on a form.
### primary_key
### If True, this field is the primary key for the model.

### If you don’t specify primary_key=True for any fields in your model, Django will automatically add an IntegerField to hold the primary key, so you don’t need to set primary_key=True on any of your fields unless you want to override the default primary-key behavior.

### The primary key field is read-only. If you change the value of the primary key on an existing object and then save it, a new object will be created alongside the old one. For example:
```python
from django.db import models

class Fruit(models.Model):
    name = models.CharField(max_length=100, primary_key=True)
```
```python
>>> fruit = Fruit.objects.create(name='Apple')
>>> fruit.name = 'Pear'
>>> fruit.save()
>>> Fruit.objects.values_list('name', flat=True)
<QuerySet ['Apple', 'Pear']>
```
### unique
### If True, this field must be unique throughout the table.

### **Automatic primary key fields**
### By default, Django gives each model the following field:
```python
id = models.AutoField(primary_key=True)
```
### This is an auto-incrementing primary key.

## **URLs and views**
### A clean, elegant URL scheme is an important detail in a high-quality Web application. Django encourages beautiful URL design and doesn’t put any cruft in URLs, like .php or .asp.

### To design URLs for an application, you create a Python module called a URLconf. Like a table of contents for your app, it contains a simple mapping between URL patterns and your views.

```python

from . import views

urlpatterns = [
    path('bands/', views.band_listing, name='band-list'),
    path('bands/<int:band_id>/', views.band_detail, name='band-detail'),
    path('bands/search/', views.band_search, name='band-search'),
]
```
```python     
from django.shortcuts import render

def band_listing(request):
    """A view of all bands."""
    bands = models.Band.objects.all()
    return render(request, 'bands/band_listing.html', {'bands': bands})

```
## **Templates**
### Django’s template language is designed to strike a balance between power and ease. It’s designed to feel comfortable and easy-to-learn to those used to working with HTML, like designers and front-end developers. But it is also flexible and highly extensible, allowing developers to augment the template language as needed.
```html
<html>
  <head>
    <title>Band Listing</title>
  </head>
  <body>
    <h1>All Bands</h1>
    <ul>
    {% for band in bands %}
      <li>
        <h2><a href="{{ band.get_absolute_url }}">{{ band.name }}</a></h2>
        {% if band.can_rock %}<p>This band can rock!</p>{% endif %}
      </li>
    {% endfor %}
    </ul>
  </body>
</html>
```

## **Forms**
### Django provides a powerful form library that handles rendering forms as HTML, validating user-submitted data, and converting that data to native Python types. Django also provides a way to generate forms from your existing models and use those forms to create and update data.

```python
from django import forms

class BandContactForm(forms.Form):
    subject = forms.CharField(max_length=100)
    message = forms.CharField()
    sender = forms.EmailField()
    cc_myself = forms.BooleanField(required=False)
```
### **Authentication**
### Django comes with a full-featured and secure authentication system. It handles user accounts, groups, permissions and cookie-based user sessions. This lets you easily build sites that allow users to create accounts and safely log in/out.
```python
from django.contrib.auth.decorators import login_required
from django.shortcuts import render

@login_required
def my_protected_view(request):
    """A view that can only be accessed by logged-in users"""
    return render(request, 'protected.html', {'current_user': request.user})
```

## **Admin**
### One of the most powerful parts of Django is its automatic admin interface. It reads metadata in your models to provide a powerful and production-ready interface that content producers can immediately use to start managing content on your site. It’s easy to set up and provides many hooks for customization.

```python
from django.contrib import admin
from bands.models import Band, Member

class MemberAdmin(admin.ModelAdmin):
    """Customize the look of the auto-generated admin for the Member model"""
    list_display = ('name', 'instrument')
    list_filter = ('band',)

admin.site.register(Band)  # Use the default options
admin.site.register(Member, MemberAdmin)  # Use the customized options
```
## **Internationalization**
### Django offers full support for translating text into different languages, plus locale-specific formatting of dates, times, numbers, and time zones. It lets developers and template authors specify which parts of their apps should be translated or formatted for local languages and cultures, and it uses these hooks to localize Web applications for particular users according to their preferences.

```python
from django.shortcuts import render
from django.utils.translation import gettext

def homepage(request):
    """
    Shows the homepage with a welcome message that is translated in the
    user's language.
    """
    message = gettext('Welcome to our site!')
    return render(request, 'homepage.html', {'message': message})
```
```html    

<html>
  <head>
    
  </head>
  <body>
    {# Translated in the view: #}
    <h1>{{ message }}</h1>
    <p>
      {% blocktrans count member_count=bands.count %}
      Here is the only band in the hall of fame:
      {% plural %}
      Here are all the {{ member_count }} bands in the hall of fame:
      {% endblocktrans %}
    </p>
    <ul>
    {% for band in bands %}
      <li>
        <h2><a href="{{ band.get_absolute_url }}">{{ band.name }}</a></h2>
        {% if band.can_rock %}<p>{% trans 'This band can rock!' %}</p>{% endif %}
      </li>
    {% endfor %}
    </ul>
  </body>
</html>
```
## **Security**
### Django provides multiple protections against:

- Clickjacking
- Cross-site scripting
- Cross Site Request Forgery (CSRF)
- SQL injection
- Remote code execution

