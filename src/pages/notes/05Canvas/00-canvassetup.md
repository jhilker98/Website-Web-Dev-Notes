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

`<canvas>` 

**Required Attributes**

`id`

`width`

`height`

**Content**

`var ctx = canvas.getContext('2d');` 2d

`var ctx = canvas.getContext('webgl');` 3d

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
