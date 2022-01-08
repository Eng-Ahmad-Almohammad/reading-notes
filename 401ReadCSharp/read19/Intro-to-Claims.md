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