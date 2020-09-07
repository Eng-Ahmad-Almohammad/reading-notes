# Table of contents
|Read No. | Name of chapter|
|:---------: |:--------------:|
|1|[HTML Introduction](https://eng-ahmad-almohammad.github.io/Introduction/)|
|1|[Structure](https://eng-ahmad-almohammad.github.io/structure/)|
|1|[Extra Markup](https://eng-ahmad-almohammad.github.io/Extra-Markup/)|
|1|[HTML5 Layout](https://eng-ahmad-almohammad.github.io/HTML5-layout/)|
|1|[Process and Design](https://eng-ahmad-almohammad.github.io/process-design/)|
|1|[JS Introduction](https://eng-ahmad-almohammad.github.io/js-introduction/)|
|1|[The ABC of programming](https://eng-ahmad-almohammad.github.io/the-ABC-of-programming/)|


# Introduction
## How the Web Works
#### When you visit a website, the web server hosting that site could be anywhere in the world. In order for you to find the location of the web server, your browser will first connect to a Domain Name System (DNS) server.
### For example:
#### when a web user in England wants to view the website of the Louvre art gallery in France which is located at www.1- louvre.fr. Firstly, the browser in Cambridge contacts a DNS server in London. The DNS server then tells the browser the location of the web server hosting the site in Paris.

1- When you connect to the web, you do so via an Internet Service Provider (ISP). You type a domain name or web address into your browser to visit a site; for example: google.com, bbc.co.uk, microsoft.com.

2-Your computer contacts a network of servers called Domain Name System (DNS) servers. These act like phone books; they tell your computer the IP address associated with the requested domain name. An IP address is a number of up to 12 digits separated by periods / full stops. Every device connected to the web has a unique IP address; it is like the phone number for that computer.

3-The unique number that the DNS server returns to your computer allows your browser to contact the web server that hosts the website you requested. A web server is a computer that is constantly connected to the web, and is set up especially to send web pages to users.

4-The web server then sends the page you requested back to your web browser.

# Structure
## Let's look at the following code. There are several different elements. Each element has an opening tag and a closing tag.
## code
![html structure](https://user-images.githubusercontent.com/70091044/92247895-8a5a3f80-eed0-11ea-85b1-34caed9c2dd9.PNG)
![html structure 1](https://user-images.githubusercontent.com/70091044/92262350-a6b3a780-eee3-11ea-8ac8-61889679e71f.PNG)


## *head*
### Before the *body* element you will often see a *head* element. This contains information about the page (rather than information that is shown withinthe main part of the browser window that is highlighted in blue on the opposite page). You will usually find a *title* element inside the *head* element.
## *title*
### The contents of the *title* element are either shown in the top of the browser, above where you usually type in the URL of the page you want to visit, or on the tab for that page (if your browser uses tabs to allow you to view multiple pages at the same time).
  
  
## _Attributes_ :
### Attributes provide additional information about the contents of an element. They appear on the opening tag of the element and are made up of two parts: a name and a value, separated by an equals sign.
![attributes](https://user-images.githubusercontent.com/70091044/92261830-d1e9c700-eee2-11ea-867b-932b137a05eb.PNG)

# Extra-Markup
## DOCTYPES
### Because there have been several versions of HTML, each web page should begin with a DOCTYPE declaration to tell a browser which version of HTML the page is using (although browsers usually display the page even if it is not included). We will therefore be including one in each example for the rest of the book.
### As you will see when we come to look at CSS and its box model onpage 316, the use of a DOCTYPE can also help the browser to render a page correctly.
### Because XHTML was written in XML, you will sometimes see pages that use the XHTML strict DOCTYPE start with the optional XML declaration. Where this is used, it should be the first thing in a document. There must be nothing before it, not even a space.
![Doctypes](https://user-images.githubusercontent.com/70091044/92270215-4f670480-eeee-11ea-8fb7-41117b05b9cc.PNG)
## Comments in HTML
### < !-- --> (without space)
### If you want to add a comment to your code that will not be visible in the user's browser, you can add the text between these characters:
### < !-- comment goes here --> (without space)
![Coment code](https://user-images.githubusercontent.com/70091044/92270916-8853a900-eeef-11ea-92f1-a570c97aa45f.PNG)
![Cmment result](https://user-images.githubusercontent.com/70091044/92270922-8c7fc680-eeef-11ea-9c91-d6e8371c27f1.PNG)

## ID Attribute
### Every HTML element can carry the id attribute. It is used to uniquely identify that element from other elements on the page. Its value should start with a letter or an underscore (not a number or any other character). It is important that no two elements on the same page have the same value for their id attributes (otherwise the value is no longer unique).
![Id](https://user-images.githubusercontent.com/70091044/92271293-365f5300-eef0-11ea-821a-17d8f0969366.PNG)
## Class Attribute
### Every HTML element can also carry a class attribute. Sometimes, rather than uniquely identifying one element within a document, you will want a way to identify several elements as being different from the other elements on the page. For example, you might have some paragraphs of text that contain information that is more important than others and want to distinguish these elements, to do this you can use the class attribute. 
![class](https://user-images.githubusercontent.com/70091044/92271814-1e3c0380-eef1-11ea-9e5a-ea363bfce2c6.PNG)
## Block Elements
### Some elements will always appear to start on a new line in the browser window. These are known as *block level* elements. 
### Examples of block elements are < h1 >, < p >, < ul >, and < li >.
![block](https://user-images.githubusercontent.com/70091044/92272238-da95c980-eef1-11ea-8705-339b10c835f7.PNG)
## Inline Elements
### Some elements will always appear to continue on the same line as their neighbouring elements. These are known as *inline* elements.
### Examples of inline elements are < a >, < b >, < em >, and < img >.
![inline](https://user-images.githubusercontent.com/70091044/92274408-db305f00-eef5-11ea-848c-04daffb61936.PNG)
## Grouping Text & Elements In a Block
## < div > 
### The < div > element allows you to group a set of elements together in one block-level box. For example, you might create a < div > element to contain all of the elements for the header of your site (the logo and the navigation), or you might create a  < div > element to contain comments from visitors.
![div](https://user-images.githubusercontent.com/70091044/92274886-b983a780-eef6-11ea-83ec-a909dd49eb05.PNG)
## Grouping Text & Elements Inline
## < span > 
### The < span > element acts like an inline equivalent of the < div > element. It is used to either:
1. Contain a section of text where there is no other suitable element to differentiate it from its surrounding text.
2. Contain a number of inline elements.
### The most common reason why people use < span > elements is so that they can control the appearance of the content of these elements using CSS.
![span](https://user-images.githubusercontent.com/70091044/92275309-90afe200-eef7-11ea-8438-37993423ad79.PNG)
## IFrames
## < iframe >
### An iframe is like a little window that has been cut into your page — and in that window you can see another page. The term iframe is an abbreviation of inline frame.
### One common use of iframes (that you may have seen on various websites) is to embed a Google Map into a page. The content of the iframe can be any html page (either located on the same server or anywhere else on the web).
### An iframe is created using the < iframe > element. There are a few attributes that you will need to know to use it:
## src
### The src attribute specifies the URL of the page to show in the frame.
## height
### The height attribute specifies the height of the iframe in pixels.
## width
### The width attribute specifies the width of the iframe in pixels.
## scrolling
### The scrolling attribute will not be supported in HTML5. In HTML 4 and XHTML, it indicates whether the iframe should have scrollbars or not. This is important if the page inside the iframe is larger than the space you have allowed for it (using the height and width attributes). Scrollbars allow the user to move around the frame to see more content. It can take one of three values: yes (to show scrollbars), no (to hide scrollbars) and auto (to show them only if needed).
## frameborder
### The frameborder attribute will not be supported in HTML5. In HTML 4 and XHTML, it indicates whether the frame should have a border or not. A value of 0 indicates that no border should be shown. A value of 1 indicates that a border should be shown.
## seamless
### In HTML5, a new attribute called seamless can be applied to an iframe where scrollbars are not desired. The seamless attribute (like some other new HTML5 attributes) does not need a value, but you will often see authors give it a value of seamless. Older browsers do not support the seamless attribute.
![iframe](https://user-images.githubusercontent.com/70091044/92276618-061cb200-eefa-11ea-90eb-14380087dbab.PNG)
## Information About Your Pages
## < meta >
### The < meta > element lives inside the < head > element and contains information about that web page. 
### It is not visible to users but fulfills a number of purposes such as telling search engines about your page, who created it, and whether or not it is time sensitive. (If the page is time sensitive, it can be set to expire.)
### The < meta > element is an empty element so it does not have a closing tag. It uses attributes to carry the information. 
### The most common attributes are the name and content attributes, which tend to be used together. These attributes specify properties of the entire page. The value of the name attribute is the property you are setting, and the value of the content attribute is the value that you want to give to this property.
### The value of the name attribute can be anything you want it to be. Some defined values for this attribute that are commonly used are:
## description
### This contains a description of the page. This description is commonly used by search engines to understand what the page is about and should be a maximum of 155 characters. Sometimes it is also displayed in search engine results.
## keywords
### This contains a list of commaseparated words that a user might search on to find the page. In practice, this no longer has any noticeable effect on how search engines index your site.
## robots
### This indicates whether search engines should add this page to their search results or not. A value of noindex can be used if this page should not be added. A value of nofollow can be used if search engines should add this page in their results but not any pages that it links to.
### The <meta> element also uses the http-equiv and content attributes in pairs. In our example, you can see three instances of the http-equiv attribute. Each one has a different purpose:
## author
### This defines the author of the web page.
## pragma
### This prevents the browser from caching the page. (That is, storing it locally to save time downloading it on subsequent visits.)
## expires
### Because browsers often cache the content of a page, the expires option can be used to indicate when the page should expire (and no longer be cached). Note that the date must be specified in the format shown.
![meta](https://user-images.githubusercontent.com/70091044/92277966-de7b1900-eefc-11ea-962d-110902e0075a.PNG)
## Escape Characters
### There are some characters that are used in and reserved by HTML code. (For example, the left and right angled brackets.)
![esPNG](https://user-images.githubusercontent.com/70091044/92278382-c5bf3300-eefd-11ea-8ebb-cd881b2d11a9.PNG)


# HTML5-layout
## Headers & Footers
## < header > < footer >
### The < header > and < footer > elements can be used for:
● The main header or footer that appears at the top or bottom of every page on the site.

● A header or footer for an individual < article > or < section > within the page.
### In this example, the < header > element used to contain the site name and the main navigation. The < footer > element contains copyright information, along with links to the privacy policy and terms and conditions. Each individual < article > and < section > element can also have its own < header > and < footer > elements to hold the header or footer information for that section within the page.
![header and footer](https://user-images.githubusercontent.com/70091044/92302622-415cc680-ef76-11ea-8c93-ad170f4f84c9.PNG)
## Navigation
## < nav >
### The < nav > element is used to contain the major navigational blocks on the site such as the primary site navigation.
![Nav](https://user-images.githubusercontent.com/70091044/92302702-d3fd6580-ef76-11ea-95f0-4d929b283175.PNG)
## Articles
## < article >
### The < article > element acts as a container for any section of a page that could stand alone and potentially be syndicated.
### This could be an individual article or blog entry, a comment or forum post, or any other independent piece of content.
![artical](https://user-images.githubusercontent.com/70091044/92302891-a4e7f380-ef78-11ea-89ea-eda56f770a63.PNG)
## Asides
## < aside >
### The < aside > element has two purposes, depending on whether it is inside an < article > element or not.
### 1-When the < aside > element is used inside an < article > element, it should contain information that is related to the article but not essential to its overall meaning. For example, a pullquote or glossary might be considered as an aside to the article it relates to.
### 2-When the < aside > element is used outside of an < article > element, it acts as a container for content that is related to the entire page. For example, it might contain links to other sections of the site, a list of recent posts, a search box, or recent tweets by the author.
![aside](https://user-images.githubusercontent.com/70091044/92302993-abc33600-ef79-11ea-8c5d-d06848525655.PNG)
## Sections
## < section >
### The < section > element groups related content together, and typically each section would have its own heading.
### For example, on a homepage there may be several < section > elements to contain different sections of the page, such as latest news, top products, and newsletter signup.
### Alternatively, if you have a page with a long article, the < section > element can be used to split the article up into separate sections.
![section](https://user-images.githubusercontent.com/70091044/92303103-82ef7080-ef7a-11ea-85fc-9df87207337e.PNG)
## Heading Groups
## < hgroup >
### The purpose of the < hgroup > element is to group together a set of one or more < h1 > through < h6 > elements so that they are treated as one single heading.
### For example, the < hgroup > element could be used to contain both a title inside an < h2 > element and a subtitle within an < h3 > element.
![hgroup](https://user-images.githubusercontent.com/70091044/92303201-52f49d00-ef7b-11ea-947a-d2b147ed3422.PNG)
## Figures
## < figure > < figcaption >
###  It can be used to contain any content that is referenced from the main flow of an article (not just images).
### It is important to note that the article should still make sense if the content of the < figure > element were moved (to another part of the page, or even to a different page altogether). For this reason, it should only be used when the content simply references the element (and not for something that is absolutely integral to the flow of a page).
### Examples of usage include:
● Images

● Videos

● Graphs

● Diagrams

● Code samples
 
● Text that supports the main
body of an article
### The < figure > element should also contain a < figcaption > element which provides a text decription for the content of the < figure > element. 
![figure](https://user-images.githubusercontent.com/70091044/92303318-52a8d180-ef7c-11ea-936b-1ee5c0b6137e.PNG)


# Process & Design
## Who is the Site For?
### Every website should be designed for the target audience—not just for yourself or the site owner. It is therefore very important to understand who your target audience is.
## Target Audience: individuals
* What is the age range of your target audience?
* Will your site appeal to more women or men? What is the mix?
* Which country do your visitors live in?
### and many others points

## Target Audience: Companies
* What is the size of the company or relevant department?
* What is the position of people in the company who visit your site?
* Will visitors be using the site for themselves or for someone else?
*  How large is the budget they control?

## Why People Visit YOUR Website
### Now that you know who your visitors are, you need to consider *why* they are coming. While some people will simply chance across your website, most will visit for a specific reason.
### for that you must have some of:
#### 1. Key Motivations.
#### 2. Specific Goals.
## What Your Visitors are Trying to Achieve
#### It is unlikely that you will be able to list every reason why someone visits your site but you are looking for key tasks and motivations. This information can help guide your site designs.
## What Information Your Visitors Need
### You know who is coming to your site and why they are coming, so now you need to work out what information they need in order to achieve their goals quickly and effectively.
## How Often People Will Visit Your Site
### Some sites benefit from being updated more frequently than others. Some information (such as news) may be constantly changing, while other content remains relatively static.
## Site Maps
### Now that you know what needs to appear on your site, you can start to organize the information into sections or pages.
## WireFrames
### A wireframe is a simple sketch of the key information that needs to go on each page of a site. It shows the hierarchy of the information and how much space it might require.
## Getting your message across using design
### The primary aim of any kind of visual design is to communicate. Organizing and prioritizing information on a page helps users understand its importance and what order to read it in.
## Visual hierarchy
### Most web users do not read entire pages. Rather, they skim to find information. You can use contrast to create a visual hierarchy that gets across your key message and helps users find what they are looking for.
## grouping and Similarity
### When making sense of a design, we tend to organize visual elements into groups. Grouping related pieces of information together can make a design easier to comprehend. Here are some ways this can be achieved.
## Designing Navigation
### Site navigation not only helps people find where they want to go, but also helps them understand what your site is about and how it is organized. Good navigation tends to follow these principles...


# Introduction
## how JavaScript makes WEB pages more interactive
### JavaScript allows you to make web pages more interactive by accessing and modifying the content and markup used in a web page while it is being viewed in the browser.
#### 1- ACCESS CONTENT: You can use JavaScript to select any element, attribute, or text from an HTML page.
#### 2- MODIFY CONTENT: You can use JavaScript to add elements, attributes, and text to the page, or remove them.
#### 3- PROGRAM RULES You can specify a set of steps for the browser to follow (like a recipe), which allows it to access or change the content of a page.
#### 4- REACT TO EVENTS You can specify that a script should run when a specific event has occurred. 

