---
layout: ../../../layouts/NotesLayout.astro
section: 'Canvas'
title: 'Shapes & Paths'
description: 'Declaring shapes and paths in the canvas.'
author: 'Research Scientist'
tags: ["canvas","shapes","paths"]
---

# Shapes

`rect()` parameters x,y,width,height

`ctx.fillRect()` fills rectangular area x,y,width,height

`ctx.clearRect()` clears fill applied to area specified x,y,width,height

# Paths

`ctx.moveTo(x,y)` moves pen without drawing

`ctx.lineTo(x,y)` draws from current position to given position 

`ctx.beginPath()` clears the buffer , useful between different paths

`ctx.closePath()` closes path , draws from last point to the first point

`ctx.strokeStyle = ''`

`ctx.fillStyle = ''`

`ctx.stroke()` draws the buffer content

`ctx.fill()` draws the buffer content

`ctx.arc()` cx,cy,radius,startAngle,endAngle,drawInverse (circle center radius radians clockwise false)

`ctx.arcTo()` x0,y0,x1,y1,radius useful for drawing curved boxes

`ctx.quadraticCurveTo()` controlX,controlY,endX,endY useful for controlling curved lines

`ctx.bezierCurveTo()` controlX1,controlY1,controlX2,controlY2,endX,endY

**A Bezier Curve**

```javascript
function drawBezierCurve() {
    ctx.beginPath();
    ctx.moveTo(100,20);
    ctx.bezierCurveTo(290,-40,200,200,400,100)
    ctx.lineWidth = 5;
    ctx.strokeStyle = 'orange';
    ctx.stroke();
}

aCanvas = document.querySelector("#awesomeCanvas");
ctx = aCanvas.getContext('2d');
drawBezierCurve();
```

**Curved Box**

```javascript
function drawCurvedBox(ctx,x,y,width,height,radius,fill,stroke) {
ctx.moveTo(x+radius, y);
ctx.arcTo(x+width, y,x+width, y+height, radius);
ctx.arcTo(x+width, y+height, x, y+height, radius); 
ctx.arcTo(x, y+height, x, y,radius);
ctx.arcTo(x, y, x+width, y,radius);
    if(fill) {
        ctx.fill();
    }
    if(stroke) {
        ctx.stroke();
    }
}

aCanvas = document.querySelector("#awesomeCanvas");
ctx = aCanvas.getContext('2d');
ctx.fillStyle = 'pink';
ctx.strokeStyle = 'red';
ctx.lineWidth = 10;
drawCurvedBox(ctx,15,15,160,120,20,true,true);
```


**Curved Arrow**

From example, probably nicer ways to implement this.

```javascript
function drawCurvedArrow(startPointX, startPointY,
                         endPointX, endPointY,
                         quadPointX, quadPointY,
                         lineWidth,
                         arrowWidth,
                         color) {
    // BEST PRACTICE: the function changes color and lineWidth -> save context!
    ctx.save();
    ctx.strokeStyle = color;
    ctx.lineWidth = lineWidth;
 
    // angle of the end tangeant, useful for drawing the arrow head
    var arrowAngle = Math.atan2(quadPointX - endPointX, quadPointY - endPointY) + Math.PI;
 
    // start a new path
    ctx.beginPath();
    // Body of the arrow
    ctx.moveTo(startPointX, startPointY);
    ctx.quadraticCurveTo(quadPointX, quadPointY, endPointX, endPointY);
    // Head of the arrow
    ctx.moveTo(endPointX - (arrowWidth * Math.sin(arrowAngle - Math.PI / 6)),
               endPointY - (arrowWidth * Math.cos(arrowAngle - Math.PI / 6)));
 
    ctx.lineTo(endPointX, endPointY);
 
    ctx.lineTo(endPointX - (arrowWidth * Math.sin(arrowAngle + Math.PI / 6)),
               endPointY - (arrowWidth * Math.cos(arrowAngle + Math.PI / 6)));
 
    ctx.stroke();
    ctx.closePath();
    // BEST PRACTICE -> restore the context as we saved it at the beginning
    // of the function
    ctx.restore();
}

aCanvas = document.querySelector("#awesomeCanvas");
ctx = aCanvas.getContext('2d');
drawCurvedArrow(10,10,200,200,150,250,10,10,'red');
```

# Text

**Methods**

`ctx.strokeText()` parameters text,x,y,[max width]

`ctx.fillText()` parameters text,x,y,[max width]

**Properties**

`ctx.font = ''` passed values are style,weight,size,face

`ctx.lineWidth = `

`textBaseline`

`textAlign` center start left end right , aligns to given x value in `fillText` or `strokeText`

`direction`

# Images

**Methods**

`ctx.drawImage()` image or video ,x,y or image,x,y,newSizeX,newSizeY or img,sx,xy,sw,sh,dx,dy,dw,dh
s is source & d is destination

For images not already on the page use a callback to use them.

```javascript
window.onload = function startImg() {
    canvas = document.querySelector("someCanvas");
    ctx = canvas.getContext('2d');
    imageObj = document.querySelector('#theImageId');
    drawImages();
}

function drawImages() {
    console.log("Image loaded.");
    ctx.drawImage(imageObj,0,0,100,100);
}
```

Video.

```html
<!--html-->
<video id="sourcevideo" autoplay="true" loop="true"><source src="somevid.mp4" type="video/mp4" /></video>
<canvas id="myCanvas" width="620" height="360"></canvas>
```

```js
   var video;
   var canvas, ctx;
   var angle = 0;
 
 function init() {
   video = document.getElementById('sourcevid');
   canvas = document.getElementById('myCanvas');
   ctx = canvas.getContext('2d');
 
   setInterval("processFrame()", 25); // call processFrame each 25ms
 }
 
 function processFrame() {
    ctx.drawImage(video, 0, 0, 320, 180); // can use video from webcam stream 

    drawRotatingVideo(480, 90);

    ctx.drawImage(video, 0, 180, 320, 180);
    ctx.drawImage(video, 320, 180, 320, 180);
 }
 
 function drawRotatingVideo(x, y) {
     // Clear the zone at the top right quarter of the canvas
    ctx.clearRect(320, 0, 320, 180);
 
    // We are going to change the coordinate system, save the context!
    ctx.save();
    // translate, rotate and recenter the image at its "real" center,
    //not the top left corner
    ctx.translate(x, y);
    ctx.rotate(angle += 0.01); // rotate and increment the current angle
    ctx.translate(-80, -45);
 
    ctx.drawImage(video, 0, 0, 160, 90);
 
    // restore the context
    ctx.restore();
 }
```



