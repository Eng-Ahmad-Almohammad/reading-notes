# Basic LINQ Query Operations
## Filtering
Probably the most common query operation is to apply a filter in the form of a Boolean expression. The filter causes the query to return only those elements for which the expression is true. The result is produced by using the where clause. The filter in effect specifies which elements to exclude from the source sequence. In the following example, only those customers who have an address in London are returned.

```csharp
var queryLondonCustomers = from cust in customers
                           where cust.City == "London"
                           select cust;
```

You can use the familiar C# logical AND and OR operators to apply as many filter expressions as necessary in the where clause. For example, to return only customers from "London" AND whose name is "Devon" you would write the following code:

```csharp
where cust.City == "London" && cust.Name == "Devon"
```

## Ordering
Often it is convenient to sort the returned data. The orderby clause will cause the elements in the returned sequence to be sorted according to the default comparer for the type being sorted. For example, the following query can be extended to sort the results based on the Name property. Because Name is a string, the default comparer performs an alphabetical sort from A to Z.

```csharp
var queryLondonCustomers3 =
    from cust in customers
    where cust.City == "London"
    orderby cust.Name ascending
    select cust;
```
To order the results in reverse order, from Z to A, use the orderby…descending clause.

## Grouping
The group clause enables you to group your results based on a key that you specify. For example you could specify that the results should be grouped by the City so that all customers from London or Paris are in individual groups. In this case, cust.City is the key.

```csharp
// queryCustomersByCity is an IEnumerable<IGrouping<string, Customer>>
  var queryCustomersByCity =
      from cust in customers
      group cust by cust.City;

  // customerGroup is an IGrouping<string, Customer>
  foreach (var customerGroup in queryCustomersByCity)
  {
      Console.WriteLine(customerGroup.Key);
      foreach (Customer customer in customerGroup)
      {
          Console.WriteLine("    {0}", customer.Name);
      }
  }
```
When you end a query with a group clause, your results take the form of a list of lists. Each element in the list is an object that has a Key member and a list of elements that are grouped under that key. When you iterate over a query that produces a sequence of groups, you must use a nested foreach loop. The outer loop iterates over each group, and the inner loop iterates over each group's members.

If you must refer to the results of a group operation, you can use the into keyword to create an identifier that can be queried further. The following query returns only those groups that contain more than two customers:

```csharp
// custQuery is an IEnumerable<IGrouping<string, Customer>>
var custQuery =
    from cust in customers
    group cust by cust.City into custGroup
    where custGroup.Count() > 2
    orderby custGroup.Key
    select custGroup;
```

## Joining
Join operations create associations between sequences that are not explicitly modeled in the data sources. For example you can perform a join to find all the customers and distributors who have the same location. In LINQ the join clause always works against object collections instead of database tables directly.

```csharp
var innerJoinQuery =
    from cust in customers
    join dist in distributors on cust.City equals dist.City
    select new { CustomerName = cust.Name, DistributorName = dist.Name };
```
In LINQ, you do not have to use join as often as you do in SQL, because foreign keys in LINQ are represented in the object model as properties that hold a collection of items. For example, a Customer object contains a collection of Order objects. Rather than performing a join, you access the orders by using dot notation:

```csharp
from order in Customer.Orders...
```

