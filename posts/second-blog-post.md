---
title: Week 2 Basic JavaScript concept
published_at: 2024-3
snippet: Week 2
disable_html_sanitization: true


---

Hello, homework

# Refactor
<iframe src="https://editor.p5js.org/HappiesDay/full/b39uwtomr"></iframe>

# Sketch for Fatal of the flesh then later change to Fill this up
## Draw a line when mouse pressed is register (Old concept form the work fatal o the Flesh)
Using Mouse X and Mouse Y as coordinate, I can make a line using the current mouse position and the after 0.2 second mouse position
<br>
The original work doesn't have a countinuos cut, therefore I make a timer whenever the mouse press but it didnt work out in this sketch
<iframe src="https://editor.p5js.org/HappiesDay/full/Tm_A2P_P7"></iframe>


## Change to mouseDragged
Instead of using mouseclick, I change to drag for easier management. The code is also cleaner and more compact
```
function mouseDragged() {
  pressTime = setTimeout(startDragging, 400); //When press start timer
  isDragging = true //reset if the dragging is true
}

function startDragging() {
  isDragging = false;
}
```
The end result is this which is similiar to a basic painting programme.
<iframe src="https://editor.p5js.org/HappiesDay/full/aHv9ZxG0s"></iframe>

## Generate a new shape

<iframe width="560" height="315" src="https://www.youtube.com/embed/cgk2BOM7KZk?si=MTIEZ4fpLmToxPfS&amp;start=4199" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
I use a new sketch to simplify my steps. Since the shape is randomized along with the new concept called vertex the lecturer show in the falling falling I think it is best use with circle since circle or eclipse shape can morph into other shape. In this sketch I tried to follow this youtube tutorial to make a shape every new frame
<iframe src="https://editor.p5js.org/HappiesDay/full/RxTIvkUaL"></iframe>
### Combining the two
<iframe width="100%" height=800px src="https://editor.p5js.org/HappiesDay/full/4kvHIq4zw"></iframe>


