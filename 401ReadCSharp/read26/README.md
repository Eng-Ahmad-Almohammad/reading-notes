# Intro to MVC

# Table of contents

|Read No. | Name of chapter|
|:---------: |:--------------:|
|20|[MVC Basics](MVC-Basics.md)|





# MVC-Basics.md

**MVC** is a design pattern or architecture which helps in developing the web application in a most efficient way when compared with the traditional ASP.NET Web Application.

## The differences between ASP.NET Web Application Framework and ASP.NET MVC Application Framework.

- In traditional ASP.NET web application approach, the user action and view (UI) are combined, i.e., the web page, say, Sample.aspx and code behind Sample.aspx.cs which has the action logic are both tightly coupled, whereas in MVC, the View only deals with UI of the page and the user actions are defined in Controller.

- In any web based application, a user initiates the requests which are nothing but actions. So, for action based requirement, ASP.NET Web Application follows the View based architecture which is not so efficient. MVC is action-based architecture. Based on the action, an appropriate View is displayed. The organization of the code inside MVC is very clean and organized.

- In ASP.NET, View State is used to maintain the state of the web page. Maintaining the state means maintaining the data between post backs for a user. This makes the web page heavy which, in turn, makes the trips to server inefficient. In MVC, we don’t have View State to store the state information.

- Unlike in ASP.NET where entire Page Life cycle is undergone for each request, the response time of the web page is very high which is not user friendly. In MVC, we don’t have the concept of page life cycle. When a request is made, the request hits the Controller which, in turn, hits the appropriate action. Then, the controller collects the required data from model and it is rendered in the appropriate View to user. So the response time is very low.

- Testing is as important as development. A code which is not tested properly may break in few scenarios which degrades the quality of the software. In ASP.NET, testing is tedious task as both View (UI) and Business logic (code behind) are tightly coupled. We cannot test code-behind separately. In MVC, it enhances the test-driven development by making the UI and action logic loosely coupled. As Models, Controllers and Views are all separate layers, they can be tested easily.



Basically, MVC makes the design of the application into three layers namely Model, View, and Controller. Each of these components are built to handle different aspects of the application.

**Model** layer represent the objects in our Application. Model is also a class which has all the objects and its properties and methods defined in it.

**View** Layer has all the html controls which define the UI of the application. Here in MVC, we don’t have drag and drop option for controls as we don’t use server controls. Instead we use Razor Engine available with Visual Studio by default which helps in rendering the View.

Views are files with .cshtml extensions. .cshtml contain both html and server code.

And also, using ‘@’, we can access C# code so that in our page which can access server side dynamic data.

**Controller** basically handles the request from user. It is the heart of the MVC application as everyone say. It is responsible to handle the request and return a response to user by loading appropriate View with data from Model.

Controller is nothing but a class with a group of methods called actions. And Every action method returns view. A View can be anything like it can be xml or html or JSON etc.

Controller maps the incoming user requests to appropriate Controller actions with the help of process called Routing.

Routing process internally creates a table called ‘Route Table’ which describes which action to be taken for each request from user. The route table is created during the Application Start event. Routes are URL patterns created dynamically based on incoming request.

Generally, Data Access Layer is again a separate layer along with MVC Layers, like as we have in asp.net web application. DAL can contact Database and return result to Model.

Another important point to remember is, MVC is not totally new framework. It is built on top of asp.net, so all the features available in asp.net can be used in MVC as well. So it is called as Asp.net MVC.

Using MVC, once the application is developed, we can use the same logic for either asp.net MVC Application or phone app just by changing the View Layer of the application. So MVC also enhances reusability.

We can say MVC follows Front Controller approach because here it is that Controller which handles all requests whereas ASP.net Web Application follows Page Controller approach. i.e It is Page level at which incoming request is handled and act accordingly.