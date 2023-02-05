---
layout: ../../../layouts/NotesLayout.astro
section: 'Canvas'
title: 'Styles'
description: 'Style canvas elements.'
author: 'Research Scientist'
tags: ["canvas","style"]
---

# Styles

`ctx.fillStyle = ''` background , color pattern or gradient

`ctx.strokeStyle = ''` outline , color pattern or gradient

`ctx.lineWidth = ''` sets line width of stroke , does not apply to fill

`ctx.lineCap = ''` butt (default) , round , square

`ctx.lineJoin = ''` miter (default) , round , bevel

`ctx.font = ''` set some font such as bold 18pt AdventPro

# Colour Gradients

`ctx.createLinearGradient(x0,y0,x1,y1);` x,y give direction of gradient

`ctx.createRadialGradient();` cx1,cy1,radius1,cx2,cy2,radius2 (inner circle,outer circle)

`someGradient.addColorStop()` 1st param from 0 to 1 represents % , 2nd param is colour

**Linear**

```javascript
aCanvas = document.querySelector("#awesomeCanvas");
ctx = aCanvas.getContext('2d');

softBox = ctx.createLinearGradient(0,0,300,0);
softBox.addColorStop(0,'rgb(100,100,100)');
softBox.addColorStop(0.5,'rgb(200,200,200)');
softBox.addColorStop(1,'rgb(100,100,100)');
ctx.fillStyle = softBox;
ctx.fillRect(0,0,300,150);
ctx.strokeStyle = softBox;
ctx.lineWidth = 10;
ctx.strokeRect(40,170,310,200);
```

**Radial**

```javascript
aCanvas = document.querySelector("#awesomeCanvas");
ctx = aCanvas.getContext('2d');

softCircle = ctx.createRadialGradient(100,100,25,100,100,75);
softCircle.addColorStop(0,'rgb(100,100,100)');
softCircle.addColorStop(0.5,'rgb(200,200,200)');
softCircle.addColorStop(1,'rgb(100,100,100)');
ctx.fillStyle = softCircle;
ctx.beginPath();
ctx.arc(100,100,100,0,2*Math.PI);
ctx.fill();
```

# Shadows

`setShadow()`

`shadowColor`

`shadowBlur`

`shadowOffsetX`

`shadowOffsetY`

```javascript
aCanvas = document.querySelector("#awesomeCanvas");
ctx = aCanvas.getContext('2d');

function setShadow() {
    ctx.shadowColor = 'grey';
    ctx.shadowBlur = '20';
    ctx.shadowOffsetX = 5;
    ctx.shadowOffsetY = 5;
}

ctx.beginPath();
ctx.arc(200,250,50,0,2*Math.PI,false);
ctx.save(); // comment out for inset shadow
ctx.fillStyle = 'orange';
setShadow();
ctx.fill();
ctx.restore(); // comment out for inset shadow
```
