# Polymorphism


### Polymorphism has two distinct aspects:

- At run time, objects of a derived class may be treated as objects of a base class in places such as method parameters and collections or arrays. When this polymorphism occurs, the object's declared type is no longer identical to its run-time type.

- Base classes may define and implement virtual methods, and derived classes can override them, which means they provide their own definition and implementation. At run-time, when client code calls the method, the CLR looks up the run-time type of the object, and invokes that override of the virtual method. In your source code you can call a method on a base class, and cause a derived class's version of the method to be executed.


## Polymorphism overview

### When a derived class inherits from a base class, it gains all the methods, fields, properties, and events of the base class. The designer of the derived class has different choices for the behavior of virtual methods:

- The derived class may override virtual members in the base class, defining new behavior.
- The derived class inherit the closest base class method without overriding it, preserving the existing behavior but enabling further derived classes to override the method.
- The derived class may define new non-virtual implementation of those members that hide the base class implementations.

### A derived class can override a base class member only if the base class member is declared as virtual or abstract. The derived member must use the override keyword to explicitly indicate that the method is intended to participate in virtual invocation. The following code provides an example:

```csharp
public class BaseClass
{
    public virtual void DoWork() { }
    public virtual int WorkProperty
    {
        get { return 0; }
    }
}
public class DerivedClass : BaseClass
{
    public override void DoWork() { }
    public override int WorkProperty
    {
        get { return 0; }
    }
}
```

## Hide base class members with new members

### If you want your derived class to have a member with the same name as a member in a base class, you can use the new keyword to hide the base class member. The new keyword is put before the return type of a class member that is being replaced. The following code provides an example:

```csharp
public class BaseClass
{
    public void DoWork() { WorkField++; }
    public int WorkField;
    public int WorkProperty
    {
        get { return 0; }
    }
}

public class DerivedClass : BaseClass
{
    public new void DoWork() { WorkField++; }
    public new int WorkField;
    public new int WorkProperty
    {
        get { return 0; }
    }
}
```

## Prevent derived classes from overriding virtual members

### Virtual members remain virtual, regardless of how many classes have been declared between the virtual member and the class that originally declared it. If class A declares a virtual member, and class B derives from A, and class C derives from B, class C inherits the virtual member, and may override it, regardless of whether class B declared an override for that member. The following code provides an example:

```csharp
public class A
{
    public virtual void DoWork() { }
}
public class B : A
{
    public override void DoWork() { }
}
```

### A derived class can stop virtual inheritance by declaring an override as sealed. Stopping inheritance requires putting the sealed keyword before the override keyword in the class member declaration. The following code provides an example:

```csharp
public class C : B
{
    public sealed override void DoWork() { }
}
```

### In the previous example, the method DoWork is no longer virtual to any class derived from C. It's still virtual for instances of C, even if they're cast to type B or type A. Sealed methods can be replaced by derived classes by using the new keyword, as the following example shows:

```csharp
public class D : C
{
    public new void DoWork() { }
}
```
### In this case, if DoWork is called on D using a variable of type D, the new DoWork is called. If a variable of type C, B, or A is used to access an instance of D, a call to DoWork will follow the rules of virtual inheritance, routing those calls to the implementation of DoWork on class C.


## Access base class virtual members from derived classes
### A derived class that has replaced or overridden a method or property can still access the method or property on the base class using the base keyword. The following code provides an example:

```csharp

public class Base
{
    public virtual void DoWork() {/*...*/ }
}
public class Derived : Base
{
    public override void DoWork()
    {
        //Perform Derived's work here
        //...
        // Call DoWork on base class
        base.DoWork();
    }
}
```