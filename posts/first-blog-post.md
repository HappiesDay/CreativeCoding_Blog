---
title: Week 1
published_at: 2024-3
snippet: Week 1
disable_html_sanitization: true

---

Hello, world


# Grid
## Initial idea: Create instance for total columns and rows
At first to make 
```
function draw() 
{
  const t = frameCount / 25
  const total_squares = 10
    const totalColumns = innerWidth / total_squares 
    
    const totalRows = innerHeight/ total_squares 

  background(`turquoise`);
  fill (`deeppink`)
 
  const size = width / total_squares *0.90
  for (let i = 0; i < totalColumns; i++) 
  {
    for (let j = 0; j < totalRows; j++)
    {
      const x = width * (i + 0.5) / totalColumns
      const y = height * (j + 0.5) / totalRows

      square (x, y, t * ((i + j)+1) % size)
    }
  }
}
```

## Second idea: Change the size of square

### Third idea: Add a way to create more square for every square on the horizon line

<iframe width="100%" height=(width/10)*15 src="https://editor.p5js.org/HappiesDay/full/LpYEK21eS"></iframe>


