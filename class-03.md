# Table of content
 |Read No. | Name of chapter|
 |:---------: |:--------------:|
 |3|[Lists](https://eng-ahmad-almohammad.github.io/lists/)|
 |3|[Boxes](https://eng-ahmad-almohammad.github.io/Boxes/)|
 |3|[Basic JavaScrit instructions](https://eng-ahmad-almohammad.github.io/Basic-JavaScript-Instructions/)|
 |3|[Decisions and loops](https://eng-ahmad-almohammad.github.io/Decisions-and-Loops/)|




# Lists
## Ordered Lists
## < ol >
### The ordered list is created withthe < ol > element.
## < li >
### Each item in the list is placed between an opening < li > tag and a closing < /li > tag. (The li stands for list item.)
![ordered list](https://user-images.githubusercontent.com/70091044/92357904-4a25d780-f0f1-11ea-9327-cbd8c6dc7fd4.PNG)
## Unordered Lists
## < ul >
### The unordered list is created with the < ul > element.
## < li >
### Each item in the list is placed between an opening < li > tag and a closing < /li > tag. (The li stands for list item.)
![unordered list](https://user-images.githubusercontent.com/70091044/92372872-3a64be00-f106-11ea-9985-40d77f990a4c.PNG)
## Definition Lists
## < dl >
### The definition list is created with the < dl > element and usually consists of a series of terms and their definitions. Inside the < dl> element you will usually see pairs of < dt > and < dd > elements.
## < dt >
### This is used to contain the term being defined (the definition term).
## < dd >
### This is used to contain the definition
![definition list](https://user-images.githubusercontent.com/70091044/92373402-eefedf80-f106-11ea-89bf-6a86ff643005.PNG)
## *Nested Lists*
### You can put a second list inside an < li > element to create a sublist or nested list.
![nested list](https://user-images.githubusercontent.com/70091044/92373661-53ba3a00-f107-11ea-9488-1ee0bc1f62f4.PNG)



# Boxes
## Box Dimensions( width, height)
### By default a box is sized just big enough to hold its contents. To set your own dimensions for a box you can use the height and width properties.
### The most popular ways to specify the size of a box are to use pixels, percentages, or ems. Traditionally, pixels have been the most popular method because they allow designers to accurately control their size.
### When you use percentages, the size of the box is relative to the size of the browser window or, if the box is encased within another box, it is a percentage of the size of the containing box.
### When you use ems, the size of the box is based on the size of text within it. Designers have recently started to use percentages and ems more for measurements as they try to create designs that are flexible across devices which have different-sized screens.
![Box dimensions](https://user-images.githubusercontent.com/70091044/92375340-a72d8780-f109-11ea-89ab-e685ea3803fe.PNG)
## Limiting Width (min-width, max-width)
### Some page designs expand and shrink to fit the size of the user's screen. In such designs, the min-width property specifies the smallest size a box can be displayed at when the browser window is narrow, and the max-width property indicates the maximum width a box can stretch to when the browser window is wide.
## Limitig Height (min-height, max-height)
### In the same way that you might want to limit the width of a box on a page, you may also want to limit the height of it. This is achieved using the min-height and max-height properties.
## Overflowing Content
## overflow
### The overflow property tells the browser what to do if the content contained within a box is larger than the box itself. It can have one of two values:
### *hidden*: This property simply hides any extra content that does not fit in the box.
### *scroll*: This property adds a scrollbar to the box so that users can scroll to see the missing content.
![overflow](https://user-images.githubusercontent.com/70091044/92376169-da244b00-f10a-11ea-873d-a1e87440dfd2.PNG)
## Border, Margin & Padding
### Every box has three available properties that can be adjusted to control its appearance:
![border](https://user-images.githubusercontent.com/70091044/92376401-32f3e380-f10b-11ea-8fa0-29a0357a6c14.PNG)
## Border Width (border-width)
### The border-width property is used to control the width of a border. The value of this property can either be given in pixels or using one of the following values:

- [x] thin

- [x] medium

- [x] thick

####(You cannot use percentages with this property.)
### You can control the individual size of borders using four separate properties:

- [x] border-top-width

- [x] border-right-width

- [x] border-bottom-width

- [x] border-left-width

### You can also specify different widths for the four border values in one property, like so:
### border-width: 2px 1px 1px 2px;
#### The values here appear in clockwise order: top, right, bottom, left.
![border width](https://user-images.githubusercontent.com/70091044/92377499-e7dad000-f10c-11ea-9285-b2ca84c48e68.PNG)
## Border Style (border-style)
### You can control the style of a border using the border-style property. This property can take the following values:

- [x] solid a single solid line 

-[x] dotted a series of square dots (if your border is 2px wide, then the dots are 2px squared with a 2px gap between each dot)

- [x] dashed a series of short lines

- [x] double two solid lines (the value of the border-width property creates the sum of the two lines)

- [x] groove appears to be carved into the page

- [x] ridge appears to stick out from the page

- [x] inset appears embedded into the page

-[x] outset looks like it is coming out of the screen

-[x] hidden / none no border is shown

### You can individually change the styles of different borders using: border-top-style, border-left-style, border-right-style, border-bottom-style
![border style](https://user-images.githubusercontent.com/70091044/92378680-dc88a400-f10e-11ea-96fc-9d7ca5c1892b.PNG)
## Border Color (border-color)
### You can specify the color of a border using either RGB values, hex codes or CSS color names.
### It is possible to individually control the colors of the borders on different sides of a box using: border-top-color, border-right-color, border-bottom-color, border-left-color
![border color](https://user-images.githubusercontent.com/70091044/92379039-6e90ac80-f10f-11ea-8ed1-daeb176382d2.PNG)
### The border property allows you to specify the width, style and color of a border in one property (and the values should be coded in that specific order).
![border short](https://user-images.githubusercontent.com/70091044/92379193-b9aabf80-f10f-11ea-82d9-6691563185e0.PNG)
## padding
### The padding property allows you to specify how much space should appear between the content of an element and its border.
### The value of this property is most often specified in pixels (although it is also possible to use percentages or ems).
### You can specify different values for each side of a box using: padding-top, padding-right, padding-bottom, padding-left
![Padding](https://user-images.githubusercontent.com/70091044/92379543-52413f80-f110-11ea-8912-fb2bc1feb0f5.PNG)
## Margin
### The margin property controls the gap between boxes. Its value is commonly given in pixels, although you may also use percentages or ems.
