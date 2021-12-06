# LINQ

# Table of contents


|Read No. | Name of chapter|
|:---------: |:--------------:|
|09|[LINQ ](LINQ.md)
|09|[Introduction to LINQ Queries ](Introduction-to-LINQ-Queries.md)
|09|[Basic LINQ Query Operations ](Basic-LINQ-Query-Operations.md)



# Language Integrated Query (LINQ)

Language-Integrated Query (LINQ) is the name for a set of technologies based on the integration of query capabilities directly into the C# language. Traditionally, queries against data are expressed as simple strings without type checking at compile time or IntelliSense support. Furthermore, you have to learn a different query language for each type of data source: SQL databases, XML documents, various Web services, and so on. With LINQ, a query is a first-class language construct, just like classes, methods, events. You write queries against strongly typed collections of objects by using language keywords and familiar operators. The LINQ family of technologies provides a consistent query experience for objects (LINQ to Objects), relational databases (LINQ to SQL), and XML (LINQ to XML).

For a developer who writes queries, the most visible "language-integrated" part of LINQ is the query expression. Query expressions are written in a declarative query syntax. By using query syntax, you can perform filtering, ordering, and grouping operations on data sources with a minimum of code. You use the same basic query expression patterns to query and transform data in SQL databases, ADO.NET Datasets, XML documents and streams, and .NET collections.

You can write LINQ queries in C# for SQL Server databases, XML documents, ADO.NET Datasets, and any collection of objects that supports IEnumerable or the generic IEnumerable<T> interface. LINQ support is also provided by third parties for many Web services and other database implementations.

The following example shows the complete query operation. The complete operation includes creating a data source, defining the query expression, and executing the query in a foreach statement.

```csharp
class LINQQueryExpressions
{
    static void Main()
    {

        // Specify the data source.
        int[] scores = new int[] { 97, 92, 81, 60 };

        // Define the query expression.
        IEnumerable<int> scoreQuery =
            from score in scores
            where score > 80
            select score;

        // Execute the query.
        foreach (int i in scoreQuery)
        {
            Console.Write(i + " ");
        }
    }
}
// Output: 97 92 81
```

## Query expression overview
- Query expressions can be used to query and to transform data from any LINQ-enabled data source. For example, a single query can retrieve data from a SQL database, and produce an XML stream as output.
- Query expressions are easy to grasp because they use many familiar C# language constructs.
- The variables in a query expression are all strongly typed, although in many cases you do not have to provide the type explicitly because the compiler can infer it.
- A query is not executed until you iterate over the query variable, for example, in a foreach statement.
- At compile time, query expressions are converted to Standard Query Operator method calls according to the rules set forth in the C# specification. Any query that can be expressed by using query syntax can also be expressed by using method syntax. However, in most cases query syntax is more readable and concise.
- As a rule when you write LINQ queries, we recommend that you use query syntax whenever possible and method syntax whenever necessary. There is no semantic or performance difference between the two different forms. Query expressions are often more readable than equivalent expressions written in method syntax.
- Query expressions can be compiled to expression trees or to delegates, depending on the type that the query is applied to. IEnumerable<T> queries are compiled to delegates. IQueryable and IQueryable<T> queries are compiled to expression trees.



# Introduction to LINQ Queries

## Three Parts of a Query Operation
### All LINQ query operations consist of three distinct actions:

1. Obtain the data source.

2. Create the query.

3. Execute the query.

The following example shows how the three parts of a query operation are expressed in source code. The example uses an integer array as a data source for convenience; however, the same concepts apply to other data sources also. This example is referred to throughout the rest of this topic.

```csharp
class IntroToLINQ
{
    static void Main()
    {
        // The Three Parts of a LINQ Query:
        // 1. Data source.
        int[] numbers = new int[7] { 0, 1, 2, 3, 4, 5, 6 };

        // 2. Query creation.
        // numQuery is an IEnumerable<int>
        var numQuery =
            from num in numbers
            where (num % 2) == 0
            select num;

        // 3. Query execution.
        foreach (int num in numQuery)
        {
            Console.Write("{0,1} ", num);
        }
    }
}
```
## The Data Source
In the previous example, because the data source is an array, it implicitly supports the generic IEnumerable<T> interface. This fact means it can be queried with LINQ. A query is executed in a foreach statement, and foreach requires IEnumerable or IEnumerable<T>. Types that support IEnumerable<T> or a derived interface such as the generic IQueryable<T> are called queryable types.

A queryable type requires no modification or special treatment to serve as a LINQ data source. If the source data is not already in memory as a queryable type, the LINQ provider must represent it as such. For example, LINQ to XML loads an XML document into a queryable XElement type:

```csharp
// Create a data source from an XML document.
// using System.Xml.Linq;
XElement contacts = XElement.Load(@"c:\myContactList.xml");
```

With LINQ to SQL, you first create an object-relational mapping at design time either manually or by using the LINQ to SQL Tools in Visual Studio. You write your queries against the objects, and at run-time LINQ to SQL handles the communication with the database. In the following example, Customers represents a specific table in the database, and the type of the query result, IQueryable<T>, derives from IEnumerable<T>.

```csharp
Northwnd db = new Northwnd(@"c:\northwnd.mdf");

// Query for customers in London.
IQueryable<Customer> custQuery =
    from cust in db.Customers
    where cust.City == "London"
    select cust;
```

## The Query
he query specifies what information to retrieve from the data source or sources. Optionally, a query also specifies how that information should be sorted, grouped, and shaped before it is returned. A query is stored in a query variable and initialized with a query expression. To make it easier to write queries, C# has introduced new query syntax.

The query in the previous example returns all the even numbers from the integer array. The query expression contains three clauses: from, where and select. (If you are familiar with SQL, you will have noticed that the ordering of the clauses is reversed from the order in SQL.) The from clause specifies the data source, the where clause applies the filter, and the select clause specifies the type of the returned elements.

For now, the important point is that in LINQ, the query variable itself takes no action and returns no data. It just stores the information that is required to produce the results when the query is executed at some later point.

## Query Execution
## Deferred Execution
As stated previously, the query variable itself only stores the query commands. The actual execution of the query is deferred until you iterate over the query variable in a foreach statement. This concept is referred to as deferred execution and is demonstrated in the following example:

```csharp
//  Query execution.
foreach (int num in numQuery)
{
    Console.Write("{0,1} ", num);
}
```
The foreach statement is also where the query results are retrieved. For example, in the previous query, the iteration variable num holds each value (one at a time) in the returned sequence.

## Forcing Immediate Execution
Queries that perform aggregation functions over a range of source elements must first iterate over those elements. Examples of such queries are Count, Max, Average, and First. These execute without an explicit foreach statement because the query itself must use foreach in order to return a result. Note also that these types of queries return a single value, not an IEnumerable collection. The following query returns a count of the even numbers in the source array:

```csharp
var evenNumQuery =
    from num in numbers
    where (num % 2) == 0
    select num;

int evenNumCount = evenNumQuery.Count();
```
To force immediate execution of any query and cache its results, you can call the ToList or ToArray methods.

```csharp
List<int> numQuery2 =
    (from num in numbers
     where (num % 2) == 0
     select num).ToList();

// or like this:
// numQuery3 is still an int[]

var numQuery3 =
    (from num in numbers
     where (num % 2) == 0
     select num).ToArray();
```


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

