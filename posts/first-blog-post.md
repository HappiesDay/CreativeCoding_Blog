---
title: Week 1 Intro to ps5
published_at: 2024-3
snippet: Week 1
disable_html_sanitization: true

---

Hello, world


# Square Grid homework
## Initial idea: Create instance for total columns and rows
My idea is to create another instance to generate square in the row for every i loop.
The concept is called "Nested loop", which I learn from this tutorial
<iframe width="100%" height="315" src="https://www.youtube.com/embed/RCPof5TC-Gs?si=TPQMZ8EUzrcSwuC0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Therefore in my code, I change the loop part to become:

```
  const totalColumns = innerWidth / total_squares 
    
  const totalRows = innerHeight/ total_squares //My attempt to balance the size 

  const size = width / total_squares *0.90
  for (let i = 0; i < totalColumns; i++) 
  {
    for (let j = 0; j < totalRows; j++)   //My attempt to add another row 
    {
      const x = width * (i + 0.5) / totalColumns
      const y = height * (j + 0.5) / totalRows

      square (x, y, t * ((i + j)+1) % size)
    }
  }
```
<iframe src="https://editor.p5js.org/HappiesDay/full/mfwKcft72"></iframe>

## Second idea: Change the size of square
I find that by automating the size to match the columns and rows is quite unnecessary so I change the size to depend only on the total squares
```
  const total_squares = 10; // Number of squares in both dimensions
  const size = (width / total_squares)*0.8; // Size of each square

  for (let i = 0; i < total_squares; i++) { // Create a horizontal line of square
    for (let j = 0; j < total_squares; j++) { //for every square on the horizon line, create a verticle line of square
      const x = width * (i + 0.5) / total_squares;  
      const y = height * (j + 0.5) / total_squares;
      square(x, y, t * ((i + j) + 1) % size)/2;

```

### Final sketch:

<iframe width="100%" height=800px src="https://editor.p5js.org/HappiesDay/full/LpYEK21eS"></iframe>


# Rafaël Rozendaal sketch (Almost calm work)
## How did Rafaël achieve these effects? 
This is an interactive web, and the circle and color respond to the mouse, therefore he might have use 
-mouse X and mouse Y: for when the color in circle rotate clockwise when mouse move
-rotate: since the color in the circle rotate only clockwise and the background only rotate counter clockwise
-lerp: since the color is gradient

## Test for the use of mouse X and mouse Y in color changing
<iframe width="100%" height="315" src="https://www.youtube.com/embed/nicMAoW6u1g?si=FQDd7eDzEOLOaXSs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
