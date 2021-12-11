# How to use Data Transfer Objects in ASP.NET Core

A Data Transfer Object (commonly known as a DTO) is usually an instance of a POCO (plain old CLR object) class used as a container to encapsulate data and pass it from one layer of the application to another. You would typically find DTOs being used in the service layer to return data back to the presentation layer. The biggest advantage of using DTOs is decoupling clients from your internal data structures.

## Why use Data Transfer Objects (DTOs)?

When designing and developing an application, if you’re using models to pass data between the layers and sending data back to the presentation layer, then you’re exposing the internal data structures of your application. That’s a major design flaw in your application.

By decoupling your layers DTOs make life easier when you’re implementing APIs, MVC applications, and also messaging patterns such as Message Broker. A DTO is a great choice when you would like to pass a lightweight object across the wire — especially when you’re passing your object via a medium that is bandwidth-constrained.

## Use DTOs for data hiding
Another reason you would want to use DTOs is data hiding. That is, by using DTOs you can return only the data requested. As an example, assume you have a method named GetAllEmployees() that returns all the data pertaining to all employees. Let’s illustrate this by writing some code.

In the project we created earlier, create a new file called Employee.cs. Write the following code inside this file to define a model class named Employee.

```csharp
public class Employee
    {
        public int Id { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public string DepartmentName { get; set; }
        public decimal Basic { get; set; }
        public decimal DA { get; set; }
        public decimal HRA { get; set; }
        public decimal NetSalary { get; set; }
    }
```
Note the Employee class contains properties including Id, FirstName, LastName, Department, Basic, DA, HRA, and NetSalary. However, the presentation layer might only need the Id, FirstName, LastName, and Department Name of the employees from the GetAllEmployees() method. If this method returns a List< Employee> then anyone would be able to see the salary details of an employee. You don’t want that. 

To avoid this problem, you might design a DTO class named EmployeeDTO that would contain only the properties that are requested (such as Id, FirstName, LastName, and Department Name).

## Create a DTO class in C#
To achieve this, create a file named EmployeeDTO.cs and write the following code in there.

```csharp
public class EmployeeDTO
    {
        public int Id { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public string DepartmentName { get; set; }
    }
```

Now that the model and data transfer object classes are available, you might want to create a converter class that contains two methods: one to convert an instance of the Employee model class to an instance of EmployeeDTO and (vice versa) one to convert an instance of EmployeeDTO to an instance of the Employee model class. You might also take advantage of AutoMapper, a popular object-to-object mapping library to map these two dissimilar types.

You should create a List< EmployeeDTO> in the service layer of your application and return the collection back to the presentation layer.

