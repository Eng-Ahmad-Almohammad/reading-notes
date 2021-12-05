# Classes

## Reference types

### A type that is defined as a class is a reference type. When you declare a variable of a reference type, the variable contains the value null until you explicitly create an instance of the class by using the new operator, or assign it an object of a compatible type that may have been created elsewhere, as shown in the following example:

```csharp
//Declaring an object of type MyClass.
MyClass mc = new MyClass();

//Declaring another object of the same type, assigning it the value of the first object.
MyClass mc2 = mc;

```

In the above example when MyClass object is created, enough memory is allocated on the managed heap for it, and the variable mc holds only a reference to the location of said object.

## Declaring Classes

### Classes are declared by using the class keyword followed by a unique identifier, as shown in the following example:

```csharp

//[access modifier] - [class] - [identifier]
public class Customer
{
   // Fields, properties, methods and events go here...
}

```
The access modifier ***public*** give the access to anyone to create instance of *Customer* class.

## Creating objects
A class and an object are different things. A class defines a type of object, but it is not an object itself. An object is a concrete entity based on a class, and is sometimes referred to as an instance of a class.

Objects can be created by using the new keyword followed by the name of the class that the object will be based on, like this:

```csharp

Customer object1 = new Customer();

```

 In the previous example, object1 is a reference to an object that is based on Customer. This reference refers to the new object but does not contain the object data itself. In fact, you can create an object reference without creating an object at all:

 ```csharp
 Customer object2;
 ```

However, such a reference can be made to refer to an object, either by creating a new object, or by assigning it an existing object, such as this:

```csharp
Customer object3 = new Customer();
Customer object4 = object3;
```

This code creates two object references that both refer to the same object. Therefore, any changes to the object made through object3 are reflected in subsequent uses of object4. Because objects that are based on classes are referred to by reference, classes are known as reference types.

## Class inheritance

Classes fully support inheritance, a fundamental characteristic of object-oriented programming. When you create a class, you can inherit from any other class that is not defined as sealed, and other classes can inherit from your class and override class virtual methods.  A base class is specified by appending a colon and the name of the base class following the derived class name, like this:

```csharp
public class Manager : Employee
{
    // Employee fields, properties, methods and events are inherited
    // New Manager fields, properties, methods and events go here...
}
```

When a class declares a base class, it inherits all the members of the base class except the constructors.

A class can be declared abstract. An abstract class contains abstract methods that have a signature definition but no implementation. Abstract classes cannot be instantiated. They can only be used through derived classes that implement the abstract methods.