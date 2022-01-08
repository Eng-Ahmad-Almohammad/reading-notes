# Roles, Claims and JWT Tokens

# Table of contents


|Read No. | Name of chapter|
|:---------: |:--------------:|
|19|[Claims-Based auth](Claims-Based-auth.md)|


# Claims-based authorization in ASP.NET Core

A claim is a name value pair that represents what the subject is, not what the subject can do.

An identity can contain multiple claims with multiple values and can contain multiple claims of the same type.

## Adding claims checks
Claim based authorization checks:

- Are declarative.
- Are applied to Razor Pages, controllers, or actions within a controller.
- Can not be applied at the Razor Page handler level, they must be applied to the Page.

Claims in code specify claims which the current user must possess, and optionally the value the claim must hold to access the requested resource. Claims requirements are policy based, the developer must build and register a policy expressing the claims requirements.

The simplest type of claim policy looks for the presence of a claim and doesn't check the value.

Build and register the policy and call UseAuthorization. Registering the policy takes place as part of the Authorization service configuration, typically in the Program.cs file:

```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddRazorPages();
builder.Services.AddControllersWithViews();

builder.Services.AddAuthorization(options =>
{
   options.AddPolicy("EmployeeOnly", policy => policy.RequireClaim("EmployeeNumber"));
});

var app = builder.Build();

if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Error");
    app.UseHsts();
}

app.UseHttpsRedirection();
app.UseStaticFiles();

app.UseAuthentication();
app.UseAuthorization();

app.MapDefaultControllerRoute();
app.MapRazorPages();

app.Run();
```
In this case the EmployeeOnly policy checks for the presence of an EmployeeNumber claim on the current identity.

Apply the policy using the Policy property on the [Authorize] attribute to specify the policy name;

```csharp
[Authorize(Policy = "EmployeeOnly")]
public IActionResult VacationBalance()
{
    return View();
}
```

The [Authorize] attribute can be applied to an entire controller or Razor Page, in this instance only identities matching the policy are allowed access to any Action on the controller.

```csharp
[Authorize(Policy = "EmployeeOnly")]
public class VacationController : Controller
{
    public IActionResult Index()
    {
        return View();
    }

    public ActionResult VacationBalance()
    {
        return View();
    }

    [AllowAnonymous]
    public ActionResult VacationPolicy()
    {
        return View();
    }
}
```

The following code applies the [Authorize] attribute to a Razor Page:

```csharp
[Authorize(Policy = "EmployeeOnly")]
public class IndexModel : PageModel
{
   public void OnGet()
    {

    }
}
```

Policies can not be applied at the Razor Page handler level, they must be applied to the Page.

If you have a controller that's protected by the [Authorize] attribute, but want to allow anonymous access to particular actions you apply the AllowAnonymousAttribute attribute.

```csharp
[Authorize(Policy = "EmployeeOnly")]
public class VacationController : Controller
{
    public IActionResult Index()
    {
        return View();
    }

    public ActionResult VacationBalance()
    {
        return View();
    }

    [AllowAnonymous]
    public ActionResult VacationPolicy()
    {
        return View();
    }
}
```
Because policies can not be applied at the Razor Page handler level, we recommend using a controller when polices must be applied at the page handler level. The rest of the app that doesn't require policies at the Razor Page handler level can use Razor Pages.

Most claims come with a value. You can specify a list of allowed values when creating the policy. The following example would only succeed for employees whose employee number was 1, 2, 3, 4 or 5.

```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddRazorPages();
builder.Services.AddControllersWithViews();

builder.Services.AddAuthorization(options =>
{
    options.AddPolicy("Founders", policy =>
                      policy.RequireClaim("EmployeeNumber", "1", "2", "3", "4", "5"));
});

var app = builder.Build();

if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Error");
    app.UseHsts();
}

app.UseHttpsRedirection();
app.UseStaticFiles();

app.UseAuthentication();
app.UseAuthorization();

app.MapDefaultControllerRoute();
app.MapRazorPages();

app.Run();
```

## Multiple Policy Evaluation
If you apply multiple policies to a controller or action, then all policies must pass before access is granted. For example:

```csharp
[Authorize(Policy = "EmployeeOnly")]
public class SalaryController : Controller
{
    public IActionResult Index()
    {
        return View();
    }

    public IActionResult Payslip()
    {
        return View();
    }

    [Authorize(Policy = "HumanResources")]
    public IActionResult UpdateSalary()
    {
        return View();
    }
}
```
In the preceding example any identity which fulfills the EmployeeOnly policy can access the Payslip action as that policy is enforced on the controller. However in order to call the UpdateSalary action the identity must fulfill both the EmployeeOnly policy and the HumanResources policy.

