# Table of content
 |Read No. | Name of chapter|
 |:---------: |:--------------:|
 |4|[Links](https://eng-ahmad-almohammad.github.io/links/)|
 |4|[Latout](https://eng-ahmad-almohammad.github.io/Layout/)|
 |4|[ Functions](https://eng-ahmad-almohammad.github.io/Functions/)
 |4|[6 Reasons for Pair Programming](https://eng-ahmad-almohammad.github.io/6-Reasons-for-Pair-Programming/)





 # Links
## Writing Links
### Links are created using the < a > element. Users can click on anything between the opening < a > tag and the closing < /a > tag. You specify which page you want to link to using the href attribute.
![a comands](https://user-images.githubusercontent.com/70091044/92458940-bb878800-f1ce-11ea-9cb7-bb17ab1e55b4.PNG)
## Email Links
### (mailto:): To create a link that starts up the user's email program and addresses an email to a specified email address, you use the < a > element. However, this time the value of the href attribute starts with mailto: and is followed by the email address you want the email to be sent to.
![link email](https://user-images.githubusercontent.com/70091044/92459815-d1e21380-f1cf-11ea-8308-8773c917ac83.PNG)
## Opening Links in a New Window
### target: If you want a link to open in a new window, you can use the target attribute on the opening < a> tag. The value of this attribute should be *_blank*.
## Linking to a Specific Part of the Same Page
### At the top of a long page you might want to add a list of contents that links to the corresponding sections lower down. Or you might want to add a link from part way down the page back to the top of it to save users from having to scroll back to the top.
### To link to an element that uses an id attribute you use the < a > element again, but the value of the href attribute starts with the # symbol, followed by the value of the id attribute of the element you want to link to. In this example, < a href="#top" > links to the < h1> element at the top of the page whose id attribute has a value of top.
![link in same page](https://user-images.githubusercontent.com/70091044/92461272-c1329d00-f1d1-11ea-9585-90c77edae3e5.PNG)
## Linking to a Specific Part of Another Page
### If you want to link to a specific part of a different page (whether on your own site or a different website) you can use a similar technique. As long as the page you are linking to has id attributes that identify specific parts of the page, you can simply add the same syntax to the end of the link for that page.
### For example, to link to the bottom of the homepage of the website that accompanies this book, you would write:
### < a href="http:/www.htmlandcssbookcom/#bottom">


# Layout
## Building Blocks
### CSS treats each HTML element as if it is in its own box. This box will either be a block-level box or an inline box.
![building block](https://user-images.githubusercontent.com/70091044/92462751-8b8eb380-f1d3-11ea-9fb6-9d0664d95635.PNG)
## Controlling the Position of Elements
### CSS has the following positioning schemes that allow you to control the layout of a page: normal flow, relative positioning, and absolute positioning. You specify the positioning scheme using the position property in CSS. You can also float elements using the float property.
- [ ] *Normal flow* (position:static)
### In normal flow, each block-level element sits on top of the next one. Since this is the default way in which browsers treat HTML elements, you do not need a CSS property to indicate that elements should appear in normal flow.
- [ ] *Relative Positioning* (position:relative)
### Relative positioning moves an element in relation to where it would have been in normal flow.
- [ ] *Absolute Positioning* (position:absolute)
### When the position property is given a value of absolute, the box is taken out of normal flow and no longer affects the position of other elements on the page. (They act like it is not there.) 
- [ ] *Fixed Positioning* (position:fixed)
### Fixed positioning is a type of absolute positioning that requires the position property to have a value of fixed. It positions the element in relation to the browser window. Therefore, when a user scrolls down the page, it stays in the exact same place. 
## Overlapping Elements (z-index)
### When you use relative, fixed, or absolute positioning, boxes can overlap. If boxes do overlap, the elements that appear later in the HTML code sit on top of those that are earlier in the page. If you want to control which element sits on top, you can use the z-index property. Its value is a number, and the higher the number the closer that element is to the front.
![Z-index](https://user-images.githubusercontent.com/70091044/92497820-7ed58400-f202-11ea-8f41-9a18fd10011b.PNG)
## Floating Elements (float)
### The float property allows you to take an element in normal flow and place it as far to the left or right of the containing element as possible. Anything else that sits inside the containing element will flow around the element that is floated.






# Functions, Methods, and Objects
## WHAT IS A FUNCTION? 
### Functions let you group a series of statements together to perform a specific task. If different parts of a script repeat the same task, you can reuse the function (rather than repeating the same set of statements). 
## Declaring a function
### To creat a function, you give it a name and then write the statements neesed to achieve its task inside the curly braces.
![function](https://user-images.githubusercontent.com/70091044/92518912-cfa8a500-f221-11ea-8f56-f7603a679c01.PNG)
## Calling a function
### Having declared the function, you can then execute all of the satements between its curly braces with just one line of code.
![calling function](https://user-images.githubusercontent.com/70091044/92519456-a6d4df80-f222-11ea-8117-bd28443ce2ac.PNG)
## Declaring functions that need information
### Sometimes a function needs specific information to perform its task. In such cases, when you declare the function you give it *parameters*. Inside the function, the parameters act like variables
![function info](https://user-images.githubusercontent.com/70091044/92520103-c1f41f00-f223-11ea-887b-e2380eda44e0.PNG)






# 6 Reasons for Pair Programming
## How does pair programming work?
### pair programming commonly involves two roles: 
### 1-the Driver: is the programmer who is typing and the only one whose hands are on the keyboard.
### 2-the Navigator: The Navigator uses their words to guide the Driver but does not provide any direct input to the computer. The Navigator thinks about the big picture, what comes next, how an algorithm might be converted in to code, while scanning for typos or bugs.
## Why pair program?
### While learning to code, developers likely study several programming languages. Similar to a foreign language class, there are four fundamental skills that help anyone learn a new language:
### 1- *Listening*: hearing and interpreting the vocabulary
### 2- *Speaking*: using the correct words to communicate an idea
### 3- *Reading*: understanding what written language intends to convey
### 4- *Writing*: producing from scratch a meaningful
### The abilities you foster will serve you well in completing assignments, in your own communication and learning, in interviews, and in readiness for a job at a company that utilizes this agile practice.
### 1- Greater efficiency
#### It is a common misconception that pair programming takes a lot longer and is less efficient. In reality, when two people focus on the same code base, it is easier to catch mistakes in the making. Research indicates that pair programing takes slightly longer, but produces higher-quality code that doesn’t require later effort in troubleshooting and debugging (let alone exposing users to a broken product).
### 2- Engaged collaboration
#### When two programmers focus on the same code, the experience is more engaging and both programmers are more focused than if they were working alone. It is harder to procrastinate or get off track when someone else is relying on you to complete the work.
### 3- Learning from fellow students
#### Everyone has a different approach to problem solving; working with a teammate can expose developers to techniques they otherwise would not have thought of. If one developer has a unique approach to a specific problem, pair programming exposes the other developer to a new solution.
### 4- Social skills
####  Pair programming not only improves programming skills, but can also help programmers develop their interpersonal skills. When just grabbing the keyboard and taking over isn’t an option, getting good at finding the right words is a skill unto itself.
### 5- Job interview readiness
#### A common step in many interview processes involves pair programming between a current employee and an applicant, either in person or through a shared screen. They will carry out exercises together, such as code challenges.
### 6- Work environment readiness
#### Many companies that utilize pair programing expect to train fresh hires from CS-degree programs on how they operate to actually deliver a product. Code Fellows graduates who are already familiar with how pairing works can hit the ground running at a new job, with one less hurdle to overcome.
