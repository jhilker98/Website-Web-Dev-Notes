---
layout: ../../../layouts/NotesLayout.astro
section: 'SVG'
title: 'Animation'
description: 'Animating an SVG element.'
author: 'Research Scientist'
tags: ["SVG","animation"]
---

# Performance

**Layout Changes & Repaints**

Avoid animating properties that cause layout changes or repaints.

*No Layout Change & No Repaint*

Ok to animate these

`opacity:`

`transform:`

These are the only 2 properties that do not cause either so it's ok to animate them.

*No Layout Change*

`color:`

`background-color:`

`box-shadow:`

These 3 only cause repaint they do not cause layout changes.

*Movement*

`transform: translate();`

Do not animate margins. Use `transform: translate();` instead.

**Hardware Acceleration**

```css
/* this turns on hardware acceleration */
.element {
  transform: translateZ(0);
  backface-visibility: hidden;
  perspective: 1000px;
}
```

# Sprites

**Step Animation**

Animation jumps from one frame onto the next.

`animation: name 2s steps(24) infinite`

Make one sprite for each step.
24 FPS is the minimum to give the illusion of smooth movement.
Can purposely use fewer sprites and FPS to give a more basic movement.

**Responsive**

*Visual Detail*

Give different level of detail for sprites that appear on different devices.

Large screens

- many visual elements
- fine details

Small screens

- few visual elements
- no fine details

*Size*

Uses % but can instead use display flexbox for sizing the svg.
```css
svg {
  width: 50%;
}
```

# Animation

**Axis of Rotation**

`transform-origin: 50% 50%;` places axis on center of object

`transform-origin: 0% 0%;` places axis on top left of object

# Elemental Motion

Considerations

- Farther objects have less definition , more blurry , grayish
- Parallax effects are where farther away objects move slower than near objects
- Does the air , water or environment affect the movements

# Animate Stroke

Self drawing animation.

- shape or path has a stroke
- stroke is dashed
- obtain full length of shape with JS `.getTotalLength()`
- dasharray the whole length of the shape
- animate `dashoffset` with `@keyframes`

```css
@keyframes dash {
  50% {stroke-dashoffset: 0;}
  100% {stroke-dashoffset: -250;}
}
```

# DOM or Canvas

|DOM|Canvas|
|--|--|
|+ UI animation|+ 3d animation|
|- < 200 objects|+ 1000s of objects|
|+ resolution independent|- not resolution independent|
|+ accessible|- not accessible|
