# Don’t Overthink It Grids

## Context
### A block level element is as wide as the parent it’s inside (width: auto;). We can think of it as 100% wide. The wrapper for a grid probably don’t have much to do with semantics, it’s just a generic wrapper, so a div is fine.

## Columns
### Let’s start with a practical and common need: a main content area being 2/3 the width and a sidebar being 1/3 the width. We just make two column divs with appropriate class names. To make them next to each other, we just need to float them and apply widths.


## Clearing Context
### The parent element will collapse to zero height since it has only floated children. Let’s fix that by clearing it.

