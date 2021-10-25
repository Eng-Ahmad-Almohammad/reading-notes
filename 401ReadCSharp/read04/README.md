# Classes & Memory Management

# Table of contents


|Read No. | Name of chapter|
|:---------: |:--------------:|
|04|[Classes](Classes.md)|
|04|[Constructors](Constructors.md)|
|04|[Properties](Properties.md)|
|04|[Stack and Heap](Stack-and-Heap.md)|
|04|[Garbage Collection](Garbage-Collection.md)|





# Classes

## eference types

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






# Constructors

Whenever a class or struct is created, its constructor is called. A class or struct may have multiple constructors that take different arguments. Constructors enable the programmer to set default values, limit instantiation, and write code that is flexible and easy to read.

## Constructor syntax
A constructor is a method whose name is the same as the name of its type. Its method signature includes only the method name and its parameter list; it does not include a return type. The following example shows the constructor for a class named Person.

```csharp
public class Person
{
   private string last;
   private string first;

   public Person(string lastName, string firstName)
   {
      last = lastName;
      first = firstName;
   }

   // Remaining implementation of Person class.
}
```
```csharp
public class Location
{
   private string locationName;

   public Location(string name) => Name = name;

   public string Name
   {
      get => locationName;
      set => locationName = value;
   }
}
```

## Static constructors

A class or struct can also have a static constructor, which initializes static members of the type. Static constructors are parameterless.

```csharp
public class Adult : Person
{
   private static int minimumAge;

   public Adult(string lastName, string firstName) : base(lastName, firstName)
   { }

   static Adult()
   {
      minimumAge = 18;
   }

   // Remaining implementation of Adult class.
}
```



# Heap and Stack

There are two places the .NET framework stores items in memory as your code executes. If you haven't already met, let me introduce you to the Stack and the Heap. Both the stack and heap help us run our code. They reside in the operating memory on our machine and contain the pieces of information we need to make it all happen.

## Stack vs. Heap: What's the difference?
The Stack is more or less responsible for keeping track of what's executing in our code (or what's been "called").  The Heap is more or less responsible for keeping track of our objects.

Think of the Stack as a series of boxes stacked one on top of the next.  We keep track of what's going on in our application by stacking another box on top every time we call a method (called a Frame).  We can only use what's in the top box on the stack.  When we're done with the top box (the method is done executing) we throw it away and proceed to use the stuff in the previous box on the top of the stack. The Heap is similar except that its purpose is to hold information (not keep track of execution most of the time) so anything in our Heap can be accessed at any time.

## What goes on the Stack and Heap?

We have four main types of things we'll be putting in the Stack and Heap as our code is executing: Value Types, Reference Types, Pointers, and Instructions. 

## Value Types
 
In C#, all the "things" declared with the following list of type declarations are Value types (because they are from System.ValueType):
- bool
- byte
- char
- decimal
- double
- enum
- float
- int
- long
- sbyte
- short
- struct
- uint
- ulong
- ushort

## Reference Types

All the "things" declared with the types in this list are Reference types (and inherit from System.Object... except, of course, for object which is the System.Object object):
- class
- interface
- delegate
- object
- string

## Pointers
The third type of "thing" to be put in our memory management scheme is a Reference to a Type. A Reference is often referred to as a Pointer.  We don't explicitly use Pointers, they are managed by the Common Language Runtime (CLR). A Pointer (or Reference) is different than a Reference Type in that when we say something is a Reference Type is a means we access it through a Pointer.  A Pointer is a chunk of space in memory that points to another space in memory.  A Pointer takes up space just like any other thing that we're putting in the Stack and Heap and its value is either a memory address or null. 

## How is it decided what goes where? (Huh?)

Here are our two golden rules:
A Reference Type always goes on the Heap - easy enough, right? 
Value Types and Pointers always go where they were declared.  This is a little more complex and needs a bit more understanding of how the Stack works to figure out where "things" are declared.
The Stack, as we mentioned earlier, is responsible for keeping track of where each thread is during the execution of our code (or what's been called). You can think of it as a thread "state" and each thread has its own stack.  When our code makes a call to execute a method the thread starts executing the instructions that have been JIT-compiled and live on the method table, it also puts the method's parameters on the thread stack.  Then, as we go through the code and run into variables within the method they are placed on top of the stack.



# Fundamentals of garbage collection

In the common language runtime (CLR), the garbage collector (GC) serves as an automatic memory manager. The garbage collector manages the allocation and release of memory for an application. For developers working with managed code, this means that you don't have to write code to perform memory management tasks. Automatic memory management can eliminate common problems, such as forgetting to free an object and causing a memory leak or attempting to access memory for an object that's already been freed.


## Benefits
The garbage collector provides the following benefits:

1- Frees developers from having to manually release memory.

2- Allocates objects on the managed heap efficiently.

3- Reclaims objects that are no longer being used, clears their memory, and keeps the memory available for future allocations. Managed objects automatically get clean content to start with, so their constructors don't have to initialize every data field.

4- Provides memory safety by making sure that an object cannot use for itself the memory allocated for another object.

