# Interfaces

# Table of contents
|Read No. | Name of chapter|
|:---------: |:--------------:|
|07|[Interfaces ](interfaces.md)




# Interfaces - define behavior for multiple types

### An interface contains definitions for a group of related functionalities that a non-abstract class or a struct must implement. An interface may define static methods, which must have an implementation. Beginning with C# 8.0, an interface may define a default implementation for members. An interface may not declare instance data such as fields, auto-implemented properties, or property-like events.

### A class or struct can implement multiple interfaces, but a class can only inherit from a single class.

### Interfaces can contain instance methods, properties, events, indexers, or any combination of those four member types. Interfaces may contain static constructors, fields, constants, or operators. An interface can't contain instance fields, instance constructors, or finalizers. Interface members are public by default, and you can explicitly specify accessibility modifiers, such as public, protected, internal, private, protected internal, or private protected. A private member must have a default implementation.



### When a class or struct implements an interface, the class or struct must provide an implementation for all of the members that the interface declares but doesn't provide a default implementation for. However, if a base class implements an interface, any class that's derived from the base class inherits that implementation.

### You define an interface by using the interface keyword as the following example shows.

```csharp
interface IEquatable<T>
{
    bool Equals(T obj);
}
```

### The following example shows an implementation of the IEquatable<T> interface. The implementing class, Car, must provide an implementation of the Equals method.

```csharp
public class Car : IEquatable<Car>
{
    public string Make { get; set; }
    public string Model { get; set; }
    public string Year { get; set; }

    // Implementation of IEquatable<T> interface
    public bool Equals(Car car)
    {
        return (this.Make, this.Model, this.Year) ==
            (car.Make, car.Model, car.Year);
    }
}
```

