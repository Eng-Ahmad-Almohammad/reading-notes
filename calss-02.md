# Table of content
 |Read No. | Name of chapter|
 |:---------: |:--------------:|
 |2|[Text](https://eng-ahmad-almohammad.github.io/text/)|
 |2|[Introducing CSS](https://eng-ahmad-almohammad.github.io/Introducing-css/)|
 |2|[Basic JavaScrit instructions](https://eng-ahmad-almohammad.github.io/Basic-JavaScript-Instructions/)|
 |2|[Decisions and loops](https://eng-ahmad-almohammad.github.io/Decisions-and-Loops/)|
 
 
 
 # text
## Headings
### HTML has six "levels" of headings:
#### 1-< h1 > is used for main headings.
#### 2-< h2 > is used for subheadings.
#### 3- If there are further sections under the subheadings then the < h3 > element is used, and so on...
![heading](https://user-images.githubusercontent.com/70091044/92333937-fe901100-f091-11ea-80d6-635ba80da519.PNG)
## Paragraphs
## < p >
### To create a paragraph, surround the words that make up the paragraph with an opening < p > tag and closing < /p > tag.
## Bold & Italic
## < b >
### By enclosing words in the tags < b > and < /b > we can make characters appear bold.
## < i >
### By enclosing words in the tags < i > and < /i > we can make characters appear italic.
## Superscript & Subscrip
## < sup >
### The < sup > element is used to contain characters that should be superscript such as the suffixes of dates or mathematical concepts like raising a number to a power.
## < sub >
### The < sub > element is used to contain characters that should be subscript. It is commonly used with foot notes or chemical formulas such.
![sub and sup](https://user-images.githubusercontent.com/70091044/92334176-47e16000-f094-11ea-9c30-001c8712d432.PNG)
## White Space
### In order to make code easier to read, web page authors often add extra spaces or start some elements on new lines.
### When the browser comes across two or more spaces next to each other, it only displays one space. Similarly if it comes across a line break, it treats that as a single space too. This is known as white space collapsing.
## Line Breaks & Horizontal Rules
## < br />
### As you have already seen, the browser will automatically show each new paragraph or heading on a new line. But if you wanted to add a line break inside the middle of a paragraph you can use the line break tag < br />.
## < hr />
### To create a break between themes — such as a change of topic in a book or a new scene in a play — you can add a horizontal rule between sections using the < hr /> tag.


# Introducing CSS
### CSS works by associating rules with HTML elements. These rules govern how the content of specified elements should be displayed. A CSS rule contains two parts: a selector and a declaration.
### CSS declarations sit inside curly brackets and each is made up of two\ parts: a property and a value, separated by a colon. You can specify several properties in one declaration, each separated by a semi-colon.
## Using External CSS
## < link >
### The <link> element can be used in an HTML document to tell the browser where to find the CSS file used to style the page. It is an empty element (meaning it does not need a closing tag), and it lives inside the < head > element. It should use three attributes:
### 1- href: This specifies the path to the CSS file (which is often placed in a folder called css or styles). 
### 2- type: This attribute specifies the type of document being linked to. The value should be text/css.
### 3- rel: This specifies the relationship between the HTML page and the file it is linked to. The value should be stylesheet when linking to a CSS file.
## Using Internal CSS
## < style >
### You can also include CSS rules within an HTML page by placing them inside a < style > element, which usually sits inside the < head > element of the page. 
![internal css](https://user-images.githubusercontent.com/70091044/92334528-757bd880-f097-11ea-9bb3-5dccc00771fc.PNG)
## CSS Selectors
### There are many different types of CSS selector that allow you to target rules to specific elements in an HTML document. 
![selectors](https://user-images.githubusercontent.com/70091044/92334546-c1c71880-f097-11ea-8ea3-b0b87e8c8222.PNG)
