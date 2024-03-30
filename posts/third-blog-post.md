---
title: Week 3 Effective Complexity and the Cute
published_at: 2024-3
snippet: Week 3
disable_html_sanitization: true

---

Hello, world


# AT1 concept
## What is cute
At first to make 


## Second idea: Change the size of square

### Third idea: Add a way to create more square for every square on the horizon line


# Response to Only Suddenly
## Make the border for the circle
First to make the frame which was quite easy since you only need four rectangle position correctly
<iframe src="https://editor.p5js.org/HappiesDay/full/b_fEas7Yk"></iframe>


## Add velocity to a ball in the middle
Simply change the ball X and Y position to make it move
More X means moving to the right
More Y means moving to the bottom
The hard part is to calculate the ball position for it to collide with the box
I was very confuse on why the ball keep going outside of the border until I realise the Y count from top to bottom, not from bottom to top like how a graph would. The higher the Y the lower the position. When I realise this, calculating the collision line was rather easy.
When collide, to make the ball goes the opposite way, change the ball X from positive to negative will make the ball left -> right become ball right -> left, vice versa with ball Y
<iframe src="https://editor.p5js.org/HappiesDay/full/D3E8CWSfO"></iframe>
