# Table of contents

|Read No. | Name of chapter|
|:---------: |:--------------:|
|26|[Permissions](Permissions.md)







# Permissions

### Permission checks are always run at the very start of the view, before any other code is allowed to proceed. Permission checks will typically use the authentication information in the request.user and request.auth properties to determine if the incoming request should be permitted.

## How permissions are determined
### Permissions in REST framework are always defined as a list of permission classes.

### Before running the main body of the view each permission in the list is checked. If any permission check fails an exceptions.PermissionDenied or exceptions.NotAuthenticated exception will be raised, and the main body of the view will not run.

### When the permissions checks fail either a "403 Forbidden" or a "401 Unauthorized" response will be returned.

## Object level permissions
### REST framework permissions also support object-level permissioning. Object level permissions are used to determine if a user should be allowed to act on a particular object, which will typically be a model instance.

### Object level permissions are run by REST framework's generic views when .get_object() is called. As with view level permissions, an exceptions.PermissionDenied exception will be raised if the user is not allowed to act on the given object.

### If you're writing your own views and want to enforce object level permissions, or if you override the get_object method on a generic view, then you'll need to explicitly call the .check_object_permissions(request, obj) method on the view at the point at which you've retrieved the object.

### This will either raise a PermissionDenied or NotAuthenticated exception, or simply return if the view has the appropriate permissions.

## Setting the permission policy
### The default permission policy may be set globally, using the DEFAULT_PERMISSION_CLASSES setting. For example.
```python
REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ]
}
```

### If not specified, this setting defaults to allowing unrestricted access:
```python
'DEFAULT_PERMISSION_CLASSES': [
   'rest_framework.permissions.AllowAny',
]
```
### You can also set the authentication policy on a per-view, or per-viewset basis, using the APIView class-based views.
```python
from rest_framework.permissions import IsAuthenticated
from rest_framework.response import Response
from rest_framework.views import APIView

class ExampleView(APIView):
    permission_classes = [IsAuthenticated]

    def get(self, request, format=None):
        content = {
            'status': 'request was permitted'
        }
        return Response(content)

```
## API Reference

### **AllowAny**
### The AllowAny permission class will allow unrestricted access, regardless of if the request was authenticated or unauthenticated.

### This permission is not strictly required, since you can achieve the same result by using an empty list or tuple for the permissions setting, but you may find it useful to specify this class because it makes the intention explicit.

### **IsAuthenticated**
### The IsAuthenticated permission class will deny permission to any unauthenticated user, and allow permission otherwise.

### This permission is suitable if you want your API to only be accessible to registered users.

### **IsAdminUser**
### The IsAdminUser permission class will deny permission to any user, unless user.is_staff is True in which case permission will be allowed.

### This permission is suitable if you want your API to only be accessible to a subset of trusted administrators.

### **IsAuthenticatedOrReadOnly**
### The IsAuthenticatedOrReadOnly will allow authenticated users to perform any request. Requests for unauthorised users will only be permitted if the request method is one of the "safe" methods; GET, HEAD or OPTIONS.

### This permission is suitable if you want to your API to allow read permissions to anonymous users, and only allow write permissions to authenticated users.

## DjangoModelPermissions
### This permission class ties into Django's standard django.contrib.auth model permissions. This permission must only be applied to views that have a .queryset property set. Authorization will only be granted if the user is authenticated and has the relevant model permissions assigned.

- POST requests require the user to have the add permission on the model.
- PUT and PATCH requests require the user to have the change permission on the model.
- DELETE requests require the user to have the delete permission on the model.
## Custom permissions

### To implement a custom permission, override BasePermission and implement either, or both, of the following methods:

- .has_permission(self, request, view)
- .has_object_permission(self, request, view, obj)
### The methods should return True if the request should be granted access, and False otherwise.

### If you need to test if a request is a read operation or a write operation, you should check the request method against the constant SAFE_METHODS, which is a tuple containing 'GET', 'OPTIONS' and 'HEAD'.

