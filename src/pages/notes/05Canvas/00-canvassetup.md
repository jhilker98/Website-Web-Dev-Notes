---
layout: ../../../layouts/NotesLayout.astro
section: 'Canvas'
title: 'Set Up'
description: 'Set up the canvas element'
author: 'Research Scientist'
tags: ["canvas"]
---

# Canvas Set Up

**Element**

`<canvas></canvas>`

**Required Attributes**

`id`

`width`

`height`

`<canvas id="canvas" width="100" height="100"></canvas>`

Default size is 300px x 150px.

**Content**

`const canvas = document.getElementById("canvas");`

`const ctx = canvas.getContext('2d');` 2d

`const ctx = canvas.getContext('webgl');` 3d

# Example Template

Wait unitl the page finishes loading before beginning to draw the canvas.

```javascript
window.onload = () => {
    draw();
};
```

The draw function.

```javascript
function draw() {
    const canvas = document.getElementById("canvas");
    if (canvas.getContext) {
        const ctx = canvas.getContext('2d');
    }
    // else {
    //     some code to inform that canvas is not supported
    // }
}
```

**Timing**

These two methods are similar to `console.log`.

`console.time("someName")` begins timer

`console.timeEnd("someName")` ends timer

Placing a function or loop between them allows for the length of time that it took for the function or loop to run to be displayed in the console.

```javascript
console.time("timeywimey");
function someFunction() {
    // someCodeBlock
}
console.timeEnd("timeywimey");
```
