# Navigation Properties and Routing

# Table of contents


|Read No. | Name of chapter|
|:---------: |:--------------:|
|14|[ASP.NET MVC Routing Overview](MVC-Routing.md)|
|14|[Routing in ASP.NET Core](Core-Routing.md)|





# ASP.NET MVC Routing Overview (C#)

## Using the Default Route Table

When you create a new ASP.NET MVC application, the application is already configured to use ASP.NET Routing. ASP.NET Routing is setup in two places.

First, ASP.NET Routing is enabled in your application's Web configuration file (Web.config file). There are four sections in the configuration file that are relevant to routing: the system.web.httpModules section, the system.web.httpHandlers section, the system.webserver.modules section, and the system.webserver.handlers section. Be careful not to delete these sections because without these sections routing will no longer work.

Second, and more importantly, a route table is created in the application's Global.asax file. The Global.asax file is a special file that contains event handlers for ASP.NET application lifecycle events. The route table is created during the Application Start event.

The file in Listing 1 contains the default Global.asax file for an ASP.NET MVC application.

**Listing 1 - Global.asax.cs**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Mvc;
using System.Web.Routing;

namespace MvcApplication1
{
    // Note: For instructions on enabling IIS6 or IIS7 classic mode, 
    // visit https://go.microsoft.com/?LinkId=9394801

    public class MvcApplication : System.Web.HttpApplication
    {
        public static void RegisterRoutes(RouteCollection routes)
        {
            routes.IgnoreRoute("{resource}.axd/{*pathInfo}");

            routes.MapRoute(
                "Default",                                              // Route name
                "{controller}/{action}/{id}",                           // URL with parameters
                new { controller = "Home", action = "Index", id = "" }  // Parameter defaults
            );
        }

        protected void Application_Start()
        {
            RegisterRoutes(RouteTable.Routes);
        }
    }
}
```

When an MVC application first starts, the Application_Start() method is called. This method, in turn, calls the RegisterRoutes() method. The RegisterRoutes() method creates the route table.

The default route table contains a single route (named Default). The Default route maps the first segment of a URL to a controller name, the second segment of a URL to a controller action, and the third segment to a parameter named id.

Imagine that you enter the following URL into your web browser's address bar:

/Home/Index/3

The Default route maps this URL to the following parameters:

- controller = Home

- action = Index

- id = 3

When you request the URL /Home/Index/3, the following code is executed:

HomeController.Index(3)

The Default route includes defaults for all three parameters. If you don't supply a controller, then the controller parameter defaults to the value Home. If you don't supply an action, the action parameter defaults to the value Index. Finally, if you don't supply an id, the id parameter defaults to an empty string.

Let's look at a few examples of how the Default route maps URLs to controller actions. Imagine that you enter the following URL into your browser address bar:

/Home

Because of the Default route parameter defaults, entering this URL will cause the Index() method of the HomeController class in Listing 2 to be called.

**Listing 2 - HomeController.cs**

```csharp
using System.Web.Mvc;

namespace MvcApplication1.Controllers
{
    [HandleError]
    public class HomeController : Controller
    {
        public ActionResult Index(string id)
        {
            return View();
        }
    }
}
```
In Listing 2, the HomeController class includes a method named Index() that accepts a single parameter named Id. The URL /Home causes the Index() method to be called with an empty string as the value of the Id parameter.

Because of the way that the MVC framework invokes controller actions, the URL /Home also matches the Index() method of the HomeController class in Listing 3.

**Listing 3 - HomeController.cs (Index action with no parameter)**
```csharp
using System.Web.Mvc;

namespace MvcApplication1.Controllers
{
    [HandleError]
    public class HomeController : Controller
    {
        public ActionResult Index()
        {
            return View();
        }
    }
}
```
The Index() method in Listing 3 does not accept any parameters. The URL /Home will cause this Index() method to be called. The URL /Home/Index/3 also invokes this method (the Id is ignored).

The URL /Home also matches the Index() method of the HomeController class in Listing 4.

**Listing 4 - HomeController.cs (Index action with nullable parameter)**

```csharp
using System.Web.Mvc;

namespace MvcApplication1.Controllers
{
    [HandleError]
    public class HomeController : Controller
    {
        public ActionResult Index(int? id)
        {
            return View();
        }
    }
}
```
In Listing 4, the Index() method has one Integer parameter. Because the parameter is a nullable parameter (can have the value Null), the Index() can be called without raising an error.

Finally, invoking the Index() method in Listing 5 with the URL /Home causes an exception since the Id parameter is not a nullable parameter. If you attempt to invoke the Index() method then you get (ArgumentException was unhandled by user code).

**Listing 5 - HomeController.cs (Index action with Id parameter)**

```csharp
using System.Web.Mvc;

namespace MvcApplication1.Controllers
{
    [HandleError]
    public class HomeController : Controller
    {
        public ActionResult Index(int id)
        {
            return View();
        }
    }
}
```
The URL /Home/Index/3, on the other hand, works just fine with the Index controller action in Listing 5. The request /Home/Index/3 causes the Index() method to be called with an Id parameter that has the value 3.


# Routing in ASP.NET Core
Routing is responsible for matching incoming HTTP requests and dispatching those requests to the app's executable endpoints. Endpoints are the app's units of executable request-handling code. Endpoints are defined in the app and configured when the app starts. The endpoint matching process can extract values from the request's URL and provide those values for request processing. Using endpoint information from the app, routing is also able to generate URLs that map to endpoints.

Apps can configure routing using:

- Controllers
- Razor Pages
- SignalR
- gRPC Services
- Endpoint-enabled middleware such as Health Checks.
- Delegates and lambdas registered with routing.

## Routing basics
All ASP.NET Core templates include routing in the generated code. Routing is registered in the middleware pipeline in Startup.Configure.

The following code shows a basic example of routing:

```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }

    app.UseRouting();

    app.UseEndpoints(endpoints =>
    {
        endpoints.MapGet("/", async context =>
        {
            await context.Response.WriteAsync("Hello World!");
        });
    });
}
```
Routing uses a pair of middleware, registered by UseRouting and UseEndpoints:

- **UseRouting** adds route matching to the middleware pipeline. This middleware looks at the set of endpoints defined in the app, and selects the best match based on the request.
- **UseEndpoints** adds endpoint execution to the middleware pipeline. It runs the delegate associated with the selected endpoint.
The preceding example includes a single route to code endpoint using the MapGet method:

- When an HTTP GET request is sent to the root URL /:
    - The request delegate shown executes.
    - Hello World! is written to the HTTP response. By default, the root URL / is https://localhost:5001/.
- If the request method is not GET or the root URL is not /, no route matches and an HTTP 404 is returned.

## Endpoint

The MapGet method is used to define an endpoint. An endpoint is something that can be:

- Selected, by matching the URL and HTTP method.
- Executed, by running the delegate.

The following example shows routing with a more sophisticated route template:

```csharp
app.UseEndpoints(endpoints =>
{
    endpoints.MapGet("/hello/{name:alpha}", async context =>
    {
        var name = context.Request.RouteValues["name"];
        await context.Response.WriteAsync($"Hello {name}!");
    });
});
```

The string /hello/{name:alpha} is a route template. It is used to configure how the endpoint is matched. In this case, the template matches:

- A URL like /hello/Ryan
- Any URL path that begins with /hello/ followed by a sequence of alphabetic characters. :alpha applies a route constraint that matches only alphabetic characters. Route constraints are explained later in this document.
The second segment of the URL path, {name:alpha}:

- Is bound to the name parameter.
- Is captured and stored in HttpRequest.RouteValues.

For more information, this is the [Link](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/routing?view=aspnetcore-3.1)