---
title: Week 2 Basic JavaScript concept
published_at: 2024-3
snippet: Week 2
disable_html_sanitization: true


---

Hello, homework

# Refactor
<iframe src="https://editor.p5js.org/HappiesDay/full/b39uwtomr"></iframe>

# Response to Only Suddenly
## Make the border for the circle
First to make the frame which was quite easy since you only need four rectangle position correctly
<iframe src="https://editor.p5js.org/HappiesDay/full/b_fEas7Yk"></iframe>


## Add velocity to a ball in the middle
Simply change the ball X and Y position to make it move
<br>
More X means moving to the right
<br>
More Y means moving to the bottom
<br>
The hard part is to calculate the ball position for it to collide with the box. 
I was very confuse on why the ball keep going outside of the border until I realise the Y count from top to bottom, not from bottom to top like how a graph would. The higher the Y the lower the position. When I realise this, calculating the collision line was rather easy.
When collide, to make the ball goes the opposite way, change the ball X from positive to negative will make the ball left -> right become ball right -> left, vice versa with ball Y
<iframe width="100%" height=800px src="https://editor.p5js.org/HappiesDay/full/D3E8CWSfO"></iframe>



