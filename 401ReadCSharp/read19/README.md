# Roles, Claims and JWT Tokens

# Table of contents


|Read No. | Name of chapter|
|:---------: |:--------------:|
|19|[Claims-Based auth](Claims-Based-auth.md)|
|19|[Intro-to-Claims](Intro-to-Claims.md)|
|19|[JWT Authentication](JWT-Authentication.md)|


# Introduction to Authentication with ASP.NET Core

## The difference between Authentication and Authorisation

First of all, we should clarify the difference between these two dependent facets of security. The simple answer is that **Authentication is the process of determining who you are**, while **Authorisation revolves around what you are allowed to do, i.e. permissions**. Obviously before you can determine what a user is allowed to do, you need to know who they are, so when authorisation is required, you must also first authenticate the user in some way.

## Authentication in ASP.NET Core
he fundamental properties associated with identity have not really changed in ASP.NET Core - although they are different, they should be familiar to ASP.NET developers in general. For example, in ASP.NET 4.x, there is a property called User on HttpContext, which is of type IPrincipal, which represents the current user for a request. In ASP.NET Core there is a similar property named User, the difference being that this property is of type ClaimsPrincipal, which implements IPrincipal.

The move to use ClaimsPrincipal highlights a fundamental shift in the way authentication works in ASP.NET Core compared to ASP.NET 4.x. Previously, authorisation was typically Role-based, so a user may belong to one or more roles, and different sections of your app may require a user to have a particular role in order to access it. In ASP.NET Core this kind of role-based authorisation can still be used, but that is primarily for backward compatibility reasons. The route they really want you to take is claims-based authentication.

## Claims-based authentication

The concept of claims-based authentication can be a little confusing when you first come to it, but in practice it is probably very similar to approaches you are already using. You can think of claims as being a statement about, or a property of, a particular identity. That statement consists of a name and a value. For example you could have a DateOfBirth claim, FirstName claim, EmailAddress claim or IsVIP claim. Note that these statements are about what or who the identity is, not what they can do.

The identity itself represents a single declaration that may have many claims associated with it. For example, consider a driving license. This is a single identity which contains a number of claims - FirstName, LastName, DateOfBirth, Address and which vehicles you are allowed to drive. Your passport would be a different identity with a different set of claims.

So lets take a look at that in the context of ASP.NET Core. Identities in ASP.NET Core are a ClaimsIdentity. A simplified version of the class might look like this (the actual class is a lot bigger!):

```csharp
public class ClaimsIdentity: IIdentity
{
    public string AuthenticationType { get; }
    public bool IsAuthenticated { get; }
    public IEnumerable<Claim> Claims { get; }

    public Claim FindFirst(string type) { /*...*/ }
    public Claim HasClaim(string type, string value) { /*...*/ }
}
```

I have shown the main properties in this outline, including Claims which consists of all the claims associated with an identity. There are a number of utility methods for working with the Claims, two of which I have shown here. These are useful when you come to authorisation, and you are trying to determine whether a particular Identity has a given Claim you are interested in.

The AuthenticationType property is fairly self-explanatory. In our practical example previously, this might be the string Passport or DriversLicense, but in ASP.NET it is more likely to be Cookies, Bearer, or Google etc. It's simply the method that was used to authenticate the user, and to determine the claims associated with an identity.

Finally, the property IsAuthenticated indicates whether an identity is authenticated or not. This might seem redundant - how could you have an identity with claims when it is not authenticated? One scenario may be where you allow guest users on your site, e.g. on a shopping cart. You still have an identity associated with the user, and that identity may still have claims associated with it, but they will not be authenticated. This is an important distinction to bear in mind.

As an adjunct to that, in ASP.NET Core if you create a ClaimsIdentity and provide an AuthenticationType in the constructor, IsAuthenticated will always be true. So an authenticated user must always have an AuthenticationType, and, conversely, you cannot have an unauthenticated user which has an AuthenticationType.

## Multiple Identities
Hopefully at this point you have a conceptual handle on claims and how they relate to an Identity. I said at the beginning of this section that the User property on HttpContext is a ClaimsPrincipal, not a ClaimsIdentity, so lets take a look at a simplified version of it:

```csharp
public class ClaimsPrincipal :IPrincipal
{
    public IIdentity Identity { get; }
    public IEnumerable<ClaimsIdentity> Identities { get; }
    public IEnumerable<Claim> Claims { get; }

    public bool IsInRole(string role) { /*...*/ }
    public Claim FindFirst(string type) { /*...*/ }
    public Claim HasClaim(string type, string value) { /*...*/ }
}
```

The important point to take from this class is that there is an `Identities` property which returns `IEnumerable<ClaimsIdentity>`. So a single `ClaimsPrincipal` can consist of multiple `Identities`. There is also an `Identity` property that is there in order to implement the `IPrincipal` interface - in .NET Core it just selects the first identity in `Identities`.

Going back to our previous example of the passport and driving license, multiple identities actually makes sense - those documents are both forms of identity, each of which contain a number of claims. In this case you are the principal, and you have two forms of identity. When you have those two pieces of identity in your possession, you as the principal inherit all the claims from all your identities.

Consider another practical example - you are taking a flight. First you will be asked at the booking desk to prove the claims you make about your `FirstName` and `LastName` etc. Luckily, you remembered your passport, which is an identity that verifies those claims, so you receive your boarding pass and you're on your way to the next step.

At security you are asked to prove the claim that you are booked on to a flight. This time you need the other form of identity you are carrying, the boarding pass, which has the `FlightNumber` claim, so you are allowed to continue on your way.

Finally, once you are through security, you make your way to the VIP lounge, and are asked to prove your VIP status with the VIP Number claim. This could be in the form of a VIP card, which would be another form of identity and would verify the claim requested. If you did not have a card, you could not present the requested claim, you would be denied access, and so would be asked to leave and stop making a scene.

Again, the key points here are that a principal can have multiple identities, these identities can have multiple claims, and the `ClaimsPrincipal` inherits all the claims of its `Identities`.

As mentioned previously, the role based authorisation is mostly around for backwards compatibility reasons, so the method `IsInRole` will be generally unneeded if you adhere to the claims-based authentication emphasised in ASP.NET Core. Under the hood, this is also just implemented using claims, where the claim type defaults to `RoleClaimType`, or `ClaimType.Role`.

## Creating a new principal
So now we've seen how principals work in ASP.NET Core, how would we go about actually creating one? A simple example, such as you might see in a normal web page login might contain code similar to the following

```csharp
public async Task<IActionResult> Login(string returnUrl = null)
{
    const string Issuer = "https://gov.uk";

    var claims = new List<Claim> {
        new Claim(ClaimTypes.Name, "Andrew", ClaimValueTypes.String, Issuer),
        new Claim(ClaimTypes.Surname, "Lock", ClaimValueTypes.String, Issuer),
        new Claim(ClaimTypes.Country, "UK", ClaimValueTypes.String, Issuer),
        new Claim("ChildhoodHero", "Ronnie James Dio", ClaimValueTypes.String)
    };

    var userIdentity = new ClaimsIdentity(claims, "Passport");

    var userPrincipal = new ClaimsPrincipal(userIdentity);

    await HttpContext.Authentication.SignInAsync("Cookie", userPrincipal,
        new AuthenticationProperties
        {
            ExpiresUtc = DateTime.UtcNow.AddMinutes(20),
            IsPersistent = false,
            AllowRefresh = false
        });

    return RedirectToLocal(returnUrl);
}
```

This method currently hard-codes the claims in, but obviously you would obtain the claim values from a database or some other source. The first thing we do is build up a list of claims, populating each with a string for its name, a string for its value, and optional Issuer and ClaimValueType fields. The ClaimType class is a helper which exposes a number of common claim types. Each of these is a url for example http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name, but you do not have to use a url, as shown in the last claim added.

Once you have built up your claims you can create a new ClaimsIdentity, passing in your claim list, and specifying the AuthenticationType (to ensure that your identity has IsAuthenticated=true). Finally you can create a new ClaimsPrincipal using your identity and sign the user in. In this case we are telling the AuthenticationManager to use the "Cookie" authentication handler, which we must have configured as part of our middleware pipeline.



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



# JWT Authentication

## What is JWT?

JSON Web Token (JWT) is a means of representing claims to be transferred between two parties. The claims in a JWT are encoded as a JSON object that is digitally signed using JSON Web Signature (JWS) and/or encrypted using JSON Web Encryption (JWE).

In simple terms, it is just another way of encoding JSON object and use that encoded object as access tokens for authentication from the server.

## Let’s break JWT

There are generally three parts in JWTs as shown in the above picture.
1st part is HEADER:
```json
{
 "alg": "HS256",
 "typ": "JWT"
}
```

**alg:** We have two main algorithms(HS256/RS256) to sign our JWT 3rd part (Signature) which we mention in the headers so that the producer and consumer(you will understand this soon in the next section) both should use the same algorithm to verify the token on each end. HS256 indicates that this token is signed using HMAC-SHA256.
**typ:** Define the type of the token which is JWT obviously in our case.

When we base64UrlEncode the above header data we will get eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9 the first part of our JWT token.

## 2nd part is PAYLOAD:
It mostly contains the claims (custom data) and some standard claims as well. We can use standard claims to identify a lot of things i.e exp: the expiry of the token,iat: time at which token issued etc.
```json
{
 "email": "John Doe",
 "xyz": "abc"
}
```
When we base64UrlEncode the above payload data we will get eyJuYW1lIjoiSm9obiBEb2UiLCJhbW91bnQiOjUwMCwieHl6IjoiYWJjIn0 the second part of our JWT token.

## 3rd part is SIGNATURE:

It is calculated by base64url encoding of header and payload and concatenating them with a period as a separator. Then encrypt it with HMAC-SHA256 along with the secret key and the result of the first step.
```
key           = 'secretkey';
unsignedToken = encodeBase64Url(header) + '.' + encodeBase64Url(payload);
signature     = HMAC-SHA256(key, unsignedToken) // As mentioned in header section.
```
When we perform the above steps we will get 54W-Y-Xz6xKgSnbQ7Se7tK5hcbXIvjsZ47u6CnQxjag the third part of our JWT token


## Producer and Consumer concept of API’s

There are two parties involved, one party who gives a service, and the other party who uses the service.
- **Producer** is the one who gives a service. It will be the provider(Server) of the API(s) which are JWT protected.
- **Consumer** is the one who uses it. It will be the customer(Server/Mobile App/ Web App/ Client) who will be providing the valid JWT token to consume the API(s) being provided by the Producer.


1. Share the SECRET: This is the responsibility of the Producer side to share the mutual secret. This secret will be required to verify the token at the Producer end and the same secret will be used to create the token at the respective consumer side.
2. Prepare the PAYLOAD: Consumer should encode all the data (body or query or params) in the payload of the JWT token (you can choose specific fields that need to be present in the payload of JWT but I would suggest to wrap all the data). We will exact this at producer end to verify that the data is the same in the token payload and the request API.
i.e: GET call to `/v1/api/getdetails?email=rachitgulati26@gmail.com` should have JWT payloadand the request.query is also the same as above.

3. GET the TOKEN: The token should be present in the header with name jwt-token (you can choose your custom name or send it in authorization header after all it’s custom contract).

4. Idenitify the CONSUMER: We just need one last thing and that is to identify our consumer. This we can do it in either way by setting iss: CONSUMER_NAME standard claim in the payload or by sending another header jwt-consumer: CONSUMER_NAME. We will be using the latter one.

## CONSUMER’S JOBS:
```javascript
import axios from 'axios'; // npm install axios
const jwt = require('jsonwebtoken'); // npm install jsonwebtoken
const PRODUCER_URL = 'https://<BASE_URL>/v1/api/getdetails';
/************KEEP IT SAFE ******************/
// Keep it in ENV and get it like process.env.(secret|clientName) ;
const secret = 'hello-reader';
const clientName = 'consumer-1-erx97812'
/**************END****************/
const getUserDetails = (email) => {
  const params = {
     email
   };
  // Sign everything here for be body(POST, PUT etc) or params(GET, POST, etc).
  /***************TOKEN CREATION ***************/
   const token = jwt.sign({...params}, secret);
   // BODY as well: ex: jwt.sign({...params, ...body }, secret);
  /****************END**************/
  const options = {
   params,
   headers: {
     'jwt-token': token, // Setting token in header
     'jwt-consumer': clientName, // Consumer identity
   },
  };
  // Anyway you like to call external API. I prefer axios.
  const response =  axios.get(PRODUCER_URL, options);
  return response.data;
}
```
## PRODUCER’S JOBS:
```javascript
import _ from 'lodash'; // npm install lodash
const router = express.Router();
const jwt = require('jsonwebtoken'); // npm install jsonwebtoken
export const API_HEADERS = {
  JWT_TOKEN: 'jwt-token',
  JWT_CONSUMER: ' jwt-consumer'
};
const MESSAGES = {
 NOT_FOUND: 'Valid headers not present ',
 TOKEN_EXPIRES: 'Download token expired',
 USER_NOT_FOUND: 'User with given email doesn\'t exist',
 NOT_VALID_CLIENT: 'Not a valid client',
};
/***************SECRETS***************/
// I would prefer to keep in database if it is more than > 5. Else // keep it in environment.
const SECRETS = {
  'consumer-1-erx97812': 'secret1',
  'consumer-2-i32eecx2': 'secret2',
}
/***************END***************/
// Middleware for JWT Verifier
export const JWTVerifier = async (req, res, next) => {
  const jwtToken = req.headers[API_HEADERS.JWT_TOKEN];
  const jwtConsumer = req.headers[API_HEADERS.JWT_CONSUMER];
  const payload = {};
  if (!jwtToken || !jwtConsumer) {
    return res.status(400).json({ message: MESSAGES.NOT_FOUND });
  }
try {
    const secret = SECRETS[jwtConsumer];
    if (!secret) {
      return res.status(403).json({ message: MESSAGES.NOT_VALID_CLIENT });
    }
    _.merge(payload, req.query, req.body);
    try {
      jwt.verify(jwtToken, secret);// Verify only token not data.
      const decoded = jwt.decode(jwtToken, { complete: true });
      // Verifying the data sent inside the token should be same as payload.
      if (!_.isEqual(decoded.payload, payload)) { 
        return res.status(403).json({ message: MESSAGES.NOT_VALID_PAYLOAD });
      }
      return next();
    } catch (err) {
      return res.status(403).json({ message: MESSAGES.NOT_FOUND });
    }
  } catch (error) {
    return next(error);
  }
};
router.get('/v1/api/getdetails', JWTVerifier, (req, res, next) {
  var customData = {
    'abc@gmail.com': {
      name: 'rachit',
      dob: '26/07/1993'
    },
    'xzy@gmail.com': {
      name: 'suchit',
      dob: '09/09/1996'
    }
  }
  const user = customData[req.query.email];
  if(user) res.json({ user });
  res.json({ message: MESSAGES.USER_NOT_FOUND})
})
```