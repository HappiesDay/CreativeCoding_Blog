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
<iframe width="560" height="315" src="https://www.youtube.com/embed/RCPof5TC-Gs?si=TPQMZ8EUzrcSwuC0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Therefore in my code, I change the loop part to become:

```
function draw() 
{
  const t = frameCount / 25
  const total_squares = 10
    const totalColumns = innerWidth / total_squares 
    
    const totalRows = innerHeight/ total_squares //My attempt to balance the size 

  background(`turquoise`);
  fill (`deeppink`)
 
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
}
```
<iframe width="100%" height=800px src="https://editor.p5js.org/HappiesDay/full/mfwKcft72"></iframe>

## Second idea: Change the size of square

### Third idea: Add a way to create more square for every square on the horizon line

<iframe width="100%" height=800px src="https://editor.p5js.org/HappiesDay/full/LpYEK21eS"></iframe>


