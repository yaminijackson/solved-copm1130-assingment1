Download Link: https://assignmentchef.com/product/solved-copm1130-assingment1
<br>
<strong>Introduction </strong>

It is an interactive program designed for drawing a variety of shapes. They include straight lines, polygons, rectangles, circles, ellipses and sectors. Users can use it by manipulating keyboards and mouses, for instance, pressing, releasing and dragging.

To enable extra functions, certain events are added. Pressing “H” or “J” would trigger specific cleaning functions. Besides, another tool for drawing called FreehandTool is included. They will be

illustrated in detail later.




<h1>Documentation</h1>

First of all, I will introduce some simple functions in this program and what they do.

In View.hs:

<ul>

 <li><strong>toolToLabel</strong>: show the current Tool and how to use it l <strong>colourShapeToPicture</strong>: turn single ColourShape into a coloured Picture</li>

 <li><strong>colourShapesToPicture</strong>: use recursion and colourShapeToPicture to turn a list of</li>

</ul>

ColourShapes into the list of coloured Pictures l <strong>colourNameToColour</strong><strong>: </strong>match the ColourNames with the

<h2>Colours in CodeWorld</h2>

<ul>

 <li><strong>shapeToPicture</strong><strong>:</strong> turn cases of Shapes into the corresponding Pictures</li>

</ul>

In Controller.hs:

<ul>

 <li><strong>nextColour</strong><strong>:</strong> change the ColourName to the next one in the given sequence l <strong>nextTool</strong><strong>: </strong>change the Tool to the next one, if it is being used, then stay unchanged</li>

 <li><strong>colourD</strong><strong>:</strong> use recursion to delete all ColourShapes whose</li>

</ul>

Colour are the same l <strong>shapeD</strong><strong>: </strong>use recursion to delete all ColourShapes whose

Shape are the same

<h2>How functions are pieced together</h2>

Next, I will illustrate how these functions are pieced together. There is a function called handleEvent. It is in the form of (Model ss t c fhd). The ss is the list of ColourShape. t and c are the current using Tool and ColourName. fhd is a Bool used for starting or finishing FreehandTool. When a certain Event happens, it triggers a change from the input Model to the output one. Below shows its functions.

<ul>

 <li><strong>Press “Esc”</strong>: initialize the program l <strong>Press “D”</strong>: print the Model in terminal l <strong>Press “M”</strong>: display the mystery image l <strong>Press “Backspace” or “Delete”</strong>: delete the most recent Picture drawn l <strong>Press “Space“</strong>: draw a Polygon with vertices stored l <strong>Press “T”</strong>: change to next Tool (trigger nextTool) l <strong>Press “C”</strong>: change to next Colour (trigger nextColour)</li>

 <li><strong>Press “H”</strong>: use colourD to delete Pictures with the same Colour</li>

 <li><strong>Press “J”</strong>: use shapeD to delete Pictures with the same Shape</li>

 <li><strong>Press the mouse</strong>: store Point in the Tool in use</li>

</ul>

<ol start="2">

 <li>change fhd to True, and store the first Point in</li>

</ol>

Polyline when using FreehandTool l <strong>Release the mouse</strong>: 1. store the second Point and draw the Picture of Line, Rectangle, Circle, Ellipse and Sector 2. change fhd to False, and finish drawing when using FreehandTool

<ul>

 <li><strong>Move the mouse</strong>: when fhd is True, store Points and draw lines according to the moving track of the mouse, otherwise, stop drawing</li>

</ul>

Variables in Model will be used in function modelToPicture to display the Picture. Firstly, it shows the Tool and

<h3>ColourName in use. Secondly, use colourShapesToPicture</h3>

for converting ss to a list of coloured Picture. Thirdly, it displays the coordinate plane.

<em>         </em><strong><em> </em></strong>

To design this program, helper functions are also used. For example, the function radius for sectors. Since cases for Sectors in shapeToPicture is extremely long. So, I decided to use helper functions to shorten the width of my code.

This program is divided into three separated parts. The first one is functionality functions, like nextTool and nextColour. They are used in the other two parts of the program. The second part is the Model part. This part is designed for interaction between users and machines. If any defined Event happens, change on Model will occur. For instance, when t is RectangleTool with c being Red, click, drag and release the mouse will store a ColourShape in ss. The third part is modelToPicture. It helps transform from the Model to visible pictures.




<h1>Reflection</h1>

I encountered a conceptual problem about shapeToPicture function in Task 2. Inputs for Shape are different from those for

Picture. So, I became confused about how to use the input points. For example, I only have two opposite coordinates of the bounding box for Ellipse. However, there is no function for drawing an ellipse in CodeWorld. Then I started to sketch many ellipses. Accidentally, I found ellipses turn to circles when their long axes were equal to short axes. Therefore, it indicated we could consider ellipses as the scaled circles. That is, firstly, draw a Circle with a radius of the half short axis. Secondly, scale it in the vertical direction by the length-width ratio of the bounding box. Thirdly, translate the ellipse to the required position.

Another conceptual problem happened when I tried to draw a Polygon with only two vertices. Nothing could be observed on the coordinate plane. When I pressed “Backspace”, no picture was deleted. To test what had happened, I pressed “D” and examine the ss in Model. I think it could be considered as an invisible picture drawn. Because there is no Polygon with only two vertices. So, I changed the code for KeyPress “Space”. Unless there are at least three Points stored in PolygonTool, pressing “Space” will not draw the Polygon out.

There was a technical issue in Task 4.2. I was wondering how to use one event to trigger the other one. Specifically, how to trigger

PointerMovement by PointerPress. It seems impossible for two Events to exist simultaneously. Then I discussed with Qianhui Wang(u7070170) on WeChat. Suddenly, I came up with the idea of creating a new field and pressing mouse leads to change in this field.

PointerMovement will start to work if the field is changed.

Otherwise, it stops to store points. This method works effectively.

There was another technical issue. I had tried to optimize my delete function. The problem was if two or more Polylines were drawn consecutively, they would be deleted together. It was caused by using recursion. I discussed this problem with Yiran Wang

(u7079256) on Piazza and WeChat. He introduced the idea of “start point”. I tried to create a new field to include a list of

“start points”. But I failed when rewriting delete function.

Whatever I wrote would cause errors. Then, I discussed with Runpeng Luo on Piazza(question @423). He gave me the advice of rearranging the “list” part inside PointerMovement. I realized that each curve should be considered as one Polyline. Thus, I rewrote it. The edited PointerMovement adds new Points to the Shape of the first element in ss. The curve drawn now is one Shape, not many Shapes. So, curves drawn by FreehandTool

could be deleted separately.

<h2>Something I will do differently next time</h2>

I will improve the code quality for shapeD and colourD. I wrote almost seventy lines for those functions. I want to shorten them by minimizing the number of cases since they share similarities. But I don’t have any idea so far.




<h2>Testing</h2>

Firstly, I have to make sure the program could run successfully. So, I

<h3>used cabal v2-repl comp1100-assignment1 to run the</h3>

code in GHCI. If there is any error or warning, it would be printed out in the terminal. Therefore, it is easy for me to identify and fix problems with my code.

<em>         </em>

<h3>For functionalities of the program</h3>

Then, I need to ensure that the functions work as expected. So, I ran the whole program by typing cabal v2-run shapes and tested

it in two aspects.

The first one was about drawing functions. I drew each shape in all directions and made sure that they worked well. For example, when testing SectorTool, I attempted it in four quadrants and checked it with my expectation. Then, I focused on edge cases. For sectors, I set up one with radius 0 and no crash happened.

The other one was about functionality functions like nextTool and nextColour. All of them worked perfectly. I ran the program and pressed “T”, and the tool could be changed. Also, pressing “C” altered the current ColourName. Two examples for edge cases testing could be when the Tool was in use, pressing “T” becoming ineffective. Pressing “Backspace” with nothing drawn would not cause program crash.

<h2>Conclusion</h2>

Generally, the program integrates multiple tasks. A variety of tests has been run and all of them passed. The program can accomplish most of the drawing tasks.