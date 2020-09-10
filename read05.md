# Table of content
 |Read No. | Name of chapter|
 |:---------: |:--------------:|
 |5|[Images](https://eng-ahmad-almohammad.github.io/Images/)|
 |5|[Color](https://eng-ahmad-almohammad.github.io/Color/)
 |5|[Text](https://eng-ahmad-almohammad.github.io/Text-201/)|









 # Images
## Adding Images
## < img >
### To add an image into the page you need to use an < img > element. This is an empty element (which means there is no closing tag). It must carry the following two attributes.
## src
### This tells the browser where it can find the image file. This will usually be a relative URL pointing to an image on your own site. (Here you can see that the images are in a child folder called *images*
## alt
### This provides a text description of the image which describes the image if you cannot see it.
## Height & Width of Images
- [x] height: This specifies the height of the image in pixels.

- [x] width: This specifies the width of the image in pixels.

![img](https://user-images.githubusercontent.com/70091044/92654246-3e583200-f2f8-11ea-9161-f34468ce9e86.PNG)
## Three Rules for Creating Images
### There are three rules to remember when you are creating images for your website which are summarized below. 
### 1- Save images in the right format
### 2-Save images at the right size
### 3- Use the correct resolution
##  Figure and Figure Caption < figure > < figcaption >
### Images often come with captions. HTML5 has introduced a new < figure > element to contain images and their caption so that the two are associated. You can have more than one image inside the < figure> element as long as they all share the same caption.
### The < figcaption> element has been added to HTML5 in order to allow web page authors to add a caption to an image. Before these elements were created there was no way to associate an < img> element with its caption.
![figcaption](https://user-images.githubusercontent.com/70091044/92701706-fae1e000-f358-11ea-83bc-e06d989c7190.PNG)








# Color
## Foreground Color color
### The color property allows you to specify the color of text inside an element. You can specify any color in CSS in one of three ways:
#### 1. *RGB values*: These express colors in terms of how much red, green and blue are used to make it up. For example: rgb(100,100,90).
#### 2. * hex codes*: These are six-digit codes that represent the amount of red, green and blue in a color, preceded by a pound or hash # sign. For example: #ee3e80
#### 3. *color names*: There are 147 predefined color names that are recognized by browsers. For example: DarkCyan.
![color](https://user-images.githubusercontent.com/70091044/92714069-641b2080-f364-11ea-8dd9-33d79d529705.PNG)


## Background Color
### CSS treats each HTML element as if it appears in a box, and the background-color property sets the color of the background for that box.
### You can specify your choice of background color in the same three ways you can specify foreground colors: RGB values, hex codes, and color names. 
![background color](https://user-images.githubusercontent.com/70091044/92714176-8f057480-f364-11ea-981b-ba377f00ba2d.PNG)


## CSS3: Opacity
## opacity, rgba
### CSS3 introduces the opacity property which allows you to specify the opacity of an element and any of its child elements. The value is a number between 0.0 and 1.0 (so a value of 0.5 is 50% opacity and 0.15 is 15% opacity).

### The CSS3 rgba property allows you to specify a color, just like you would with an RGB value, but adds a fourth value to indicate opacity. This value is known as an alpha value and is a number between 0.0 and 1.0 (so a value of 0.5 is 50% opacity and 0.15 is 15% opacity). The rgba value will only affect the element on which it is applied (not child elements).
![opacity](https://user-images.githubusercontent.com/70091044/92714372-cb38d500-f364-11ea-8de3-989cd57099ae.PNG)











# Text
## Specifying Typefaces (font-family)
### The font-family property allows you to specify the typeface that should be used for any text inside the element(s) to which a CSS rule applies. The value of this property is the name of the typeface you want to use. 
## Size of Type (font-size)
### The font-size property enables you to specify a size for the font. There are several ways to specify the size of a font. The most common are:
### 1-*pixels*: are commonly used because they allow web designers very precise control over how much space their text takes up. The number of pixels is followed by the letters px.

### 2-*percentages*: The default size of text in browsers is 16px. So a size of 75% would be the equivalent of 12px, and 200% would be 32px.

### 3- *Ems*: An em is equivalent to the width of a letter m.
![font size](https://user-images.githubusercontent.com/70091044/92716360-60d56400-f367-11ea-96f4-68857ee6db29.PNG)
## More Font Choice (@font-face)
### @font-face allows you to use a font, even if it is not installed on the computer of the person browsing, by allowing you to specify a path to a copy of the font, which will be downloaded if it is not on the user's machine.
![@font-family](https://user-images.githubusercontent.com/70091044/92716679-cfb2bd00-f367-11ea-964c-806f6368c6d9.PNG)
## Bold (font-weight)
### The font-weight property allows you to create bold text. There are two values that this property commonly takes:
- [x] normal: This causes text to appear at a normal weight.

- [x] bold: This causes text to appear bold.

## Italic (font-style)
### If you want to create italic text, you can use the font-style property. There are three values this property can take:
### 1-normal: This causes text to appear in a normal style (as opposed to italic or oblique)

### 2- italic: This causes text to appear italic.

### 3- oblique: This causes text to appear oblique.

## Alignment (text-align)
### The text-align property allows you to control the alignment of text. The property can take one of four values:
### 1- left: This indicates that the text should be left-aligned.

### 2-right: This indicates that the text should be right-aligned.

### 3- center: This allows you to center text.

### 4- justify: This indicates that every line in a paragraph, except the last line, should be set to take up the full width of the containing box.
