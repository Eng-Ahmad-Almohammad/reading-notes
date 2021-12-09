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