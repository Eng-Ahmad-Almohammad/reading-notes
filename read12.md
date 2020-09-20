# Table of content
 |Read No. | Name of chapter|
 |:---------: |:--------------:|
 |12|[Charts](https://eng-ahmad-almohammad.github.io/charts/)|
 |12|[Canvas element](https://eng-ahmad-almohammad.github.io/Basic-usage-of-canvas/)|
 |12|[Drawing shapes with canvas](https://eng-ahmad-almohammad.github.io/Drawing-shapes-with-canvas/)|
 |12|[Applying styles and colors](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Applying_styles_and_colors)|
 |12|[Drawing text](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Drawing_text)|














 # charts

### Charts are far better for displaying data visually than tables and have the added benefit that no one is ever going to press-gang them into use as a layout tool. They’re easier to look at and convey data quickly, but they’re not always easy to create.
## Drawing line chart

1- Creat HTML body and [download Chart.js](https://github.com/nnnick/Chart.js),Copy the Chart.min.js out of the unzipped folder and into the directory you’ll be working in

2- Include a canvas element inside the HTML Which will include the chart.

3- Write the fllowing script in the foot of the body:
![script](https://user-images.githubusercontent.com/70091044/93720680-44210380-fb93-11ea-95e7-e89799ecaecf.PNG)

4- Add some information you need inside the script and Chart.js will draw the chart.

## Drawing a pie chart

1- Creat HTML body and [download Chart.js](https://github.com/nnnick/Chart.js),Copy the Chart.min.js out of the unzipped folder and into the directory you’ll be working in

2- Include a canvas element inside the HTML Which will include the chart.

3- Write the fllowing script in the foot of the body:
![pie script](https://user-images.githubusercontent.com/70091044/93720787-eccf6300-fb93-11ea-9643-90b7f266227e.PNG)

4- Add some information you need inside the script and styling them then Chart.js will draw the chart.

### Same thing for bar chart 








# Basic usage of canvas

## The < canvas > element

### At first sight a < canvas > looks like the <img> element, with the only clear difference being that it doesn't have the src and alt attributes. Indeed, the < canvas > element has only two attributes, width and height. These are both optional and can also be set using DOM properties. When no width and height attributes are specified, the canvas will initially be 300 pixels wide and 150 pixels high. The element can be sized arbitrarily by CSS, but during rendering the image is scaled to fit its layout size: if the CSS sizing doesn't respect the ratio of the initial canvas, it will appear distorted.


## Fallback content
### The < canvas > element differs from an < img > tag in that, like for < video >, < audio >, or < picture > elements, it is easy to define some fallback content, to be displayed in older browsers not supporting it, like versions of Internet Explorer earlier than version 9 or textual browsers. You should always provide fallback content to be displayed by those browsers.

### Providing fallback content is very straightforward: just insert the alternate content inside the < canvas > element. Browsers that don't support < canvas > will ignore the container and render the fallback content inside it. Browsers that do support < canvas > will ignore the content inside the container, and just render the canvas normally.

![canvas](https://user-images.githubusercontent.com/70091044/93721137-9152a480-fb96-11ea-8134-4f7c41074474.PNG)

## The rendering context
### The < canvas > element creates a fixed-size drawing surface that exposes one or more rendering contexts, which are used to create and manipulate the content shown. 

### The canvas is initially blank. To display something, a script first needs to access the rendering context and draw on it. The < canvas > element has a method called *getContext()*, used to obtain the rendering context and its drawing functions. *getContext()* takes one parameter, the type of context. For 2D graphics, you specify "2d" to get a *CanvasRenderingContext2D*.








# Drawing shapes with canvas
## The grid

### The origin of this grid is positioned in the top left corner at coordinate (0,0). All elements are placed relative to this origin. So the position of the top left corner of the blue square becomes x pixels from the left and y pixels from the top, at coordinate (x,y).

## Drawing rectangles
### There are three functions that draw rectangles on the canvas:

1- fillRect(x, y, width, height) Draws a filled rectangle.

2- strokeRect(x, y, width, height) Draws a rectangular outline.

3- clearRect(x, y, width, height) Clears the specified rectangular area, making it fully transparent.

### Each of these three functions takes the same parameters. x and y specify the position on the canvas (relative to the origin) of the top-left corner of the rectangle. width and height provide the rectangle's size.


## Drawing paths
### A path is a list of points, connected by segments of lines that can be of different shapes, curved or not, of different width and of different color. A path, or even a subpath, can be closed. To make shapes using paths, we take some extra steps:

1- First, you create the path.

2- Then you use drawing commands to draw into the path.

3-Once the path has been created, you can stroke or fill the path to render it.

### Here are the functions used to perform these steps:

* beginPath(): Creates a new path. Once created, future drawing commands are directed into the path and used to build the path up.

* Path methods: Methods to set different paths for objects.

* closePath(): Adds a straight line to the path, going to the start of the current sub-path.

* stroke(): Draws the shape by stroking its outline.

* fill(): Draws a solid shape by filling the path's content area.