---
layout: ../../../layouts/NotesLayout.astro
section: 'SVG'
title: 'Basics'
description: 'SVG element and attributes.'
author: 'Research Scientist'
tags: ["SVG","element"]
---

# SVG Element

```html
<svg width="100px" height="100px" viewbox="0 0 100 100" version="1.1" xmlns="...">
<circle class="circle" cx="50" cy="50" r="50" fill="rgb(100,250,100)"></circle>
</svg>
```

# SVG Attributes

`width="100px"` `height="100px"` size of the svg , if not entered then svg expands to fill viewport , if entered in css `svg {width:10px,height10x;}` width and height can be controlled via JS

`viewbox="x y width height"` size of the camera

# ViewBox

`preserveAspectRatio="alignX alignY viewbox "` alignment of viewbox within the viewport

`xMin` left edge of viewbox

`xMid` middle edge of viewbox

`xMax` right edge of viewbox

`yMin` top edge of viewbox

`yMid` middle edge of viewbox

`yMax` bottom edge of viewbox

`meet` viewbox smaller than viewport , full shape is visible

`slice`  viewbox larger than viewport , part of shape is cut off

`none` shape expands to fill viewport , shape distorted

# Shapes

`<rect x="n" y="n" width="n" height="n"/>` rectangle or square

`<circle cx="n" cy="n" r="n"/>` circle , `cx cy` define center of circle `r` defines radius

`<ellipse/>` ellipse

`<polygon points="n1 n2 n3 n4 n5 n6"/>` polygon , first n defines x second n defines y , last point auto connects to first point


`<line x1="n" y1="n" x2="n" y2="n">` line , straight from `x1 y1` to `x2 y2`

`<polyline points="n,n n,n n,n n,n"/>` polyline , straight lines between points `x,y`

# Paths

`<path d="Mn n n n n nz"/>` path curved , d is drawing , M is move to , z indicates last point and connects to first point , if no z then not a closed path instead path remains open

# Path Data

Use capital letter for absolute and lower letter for relative.

**Lines**

`Mm` move to , start of a new path

`Ll` line to , straight line

`Hh` horizontal line , from current position

`Vv` vertical line , from current position

`Zz` end path , joins this point with first point

**Curves**

`Cc` cubic bezier , two control points

`Ss` reflecting cubic bezier , same as cubic bezier but makes another curve and reflects it

`Qq` quadratic bezier , both sides share same control point

`Tt` same same as quadratic bezier but makes another curve and reflects it

`Aa` elliptical arc

# Groups

`<g></g>` Items within tags are grouped.

# Elements

`<defs>` defines elements for later use

`<text>` makes text inside SVG that can be selected

# Accessibility

Use presentation for role so screen reader does not read every shape.

```html
<svg aria-labelledby="title" id="svg" role="presentation">
<title id="title" lang="en">Some Title</title>
```

# Optimize

On objects do the following with illustration tool:

- reduce number of path points to the most minimum needed
- reduce SVG path
- png drop shadows are heave instead use SVG filter

Use svgomg.
Do not minify the file if you want to animate it.

# Add SVG to DOM

**Via SVG Tag**

Best method for accessibility and animation.

```html
<svg width="100px" height="100px" viewbox="0 0 100 100" version="1.1" xmlns="...">
<circle class="circle" cx="50" cy="50" r="50" fill="rgb(100,250,100)"></circle>
</svg>
```

**Via IMG Tag**

This allows for screen reader access. But SVG is not editable.

`<img src="someSvg.svg" alt="svg thing"`

**Via Background Image Property**

```css
div {
    background-image: url('something.png');
    background-image: url('something.svg');
}
```
