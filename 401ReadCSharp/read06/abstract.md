# Abstract and Sealed Classes and Class Members

### The abstract keyword enables you to create classes and class members that are incomplete and must be implemented in a derived class.

### The sealed keyword enables you to prevent the inheritance of a class or certain class members that were previously marked virtual.

## Abstract Classes and Class Members

```csharp
public abstract class A
{
    // Class members here.
}
```

### An abstract class cannot be instantiated. The purpose of an abstract class is to provide a common definition of a base class that multiple derived classes can share.

### Abstract classes may also define abstract methods. This is accomplished by adding the keyword abstract before the return type of the method. For example:

```csharp
public abstract class A
{
    public abstract void DoWork(int i);
}

```

### Abstract methods have no implementation, so the method definition is followed by a semicolon instead of a normal method block.

### Derived classes of the abstract class must implement all abstract methods. When an abstract class inherits a virtual method from a base class, the abstract class can override the virtual method with an abstract method. For example:

```csharp
// compile with: -target:library
public class D
{
    public virtual void DoWork(int i)
    {
        // Original implementation.
    }
}

public abstract class E : D
{
    public abstract override void DoWork(int i);
}

public class F : E
{
    public override void DoWork(int i)
    {
        // New implementation.
    }
}
```

## Sealed Classes and Class Members

```csharp
public sealed class D
{
    // Class members here.
}
```

### A sealed class cannot be used as a base class. For this reason, it cannot also be an abstract class. Sealed classes prevent derivation. Because they can never be used as a base class, some run-time optimizations can make calling sealed class members slightly faster.

