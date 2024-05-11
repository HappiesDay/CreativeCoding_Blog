---
title: Week 8 A2 submission
published_at: 2024-3
snippet: Week 7
disable_html_sanitization: true

---

Hello, world

# Responded work
## Glitch artist reference
I want to create an interactive work, and after seeing [Rosa Menkman work here](https://rosa-menkman.blogspot.com/) I was inspired to have the canvas to be interactive In Rosa's work, the text frame is not defined to 1 font nor color nor rotation, and the frame for the videos and images open weird links. This is the foundation for my chaotic aethestic where the text and the art is vurnerable to our mouse.

## Generative artist reference
Firstly to create something interesting on screen to interact, I comes to [this tutorial](https://www.youtube.com/watch?v=O7cUOPYducc) by Frank Laboratory channel, where I heavily reference the art and the code to generate the base image I will be working on. The relentless lines and path appearing is really messy and randomized which fits my goal. However I condition the effect to have big shape as time goes on since only line and path would prove difficult to fill the whole canvas and be as chaotic as possible. Overall the color remains the same since it was already saturated to the way I want.

## Interactive reference
To make the canvas interactive, I make the art switch between 2 state: generating the lines and shattering. By shattering, the effect is particle physics by [this tutorial]https://youtu.be/vAJEHf92tV0?si=I8fb9xAvrP52uy1l&t=4529) also by Frank Laboratory channel. Here I reference mostly the math to calculate the mouse / pointer influence on the particle velocity. As for the sections to freeze the canvas and turn them into particle, it shares a lot of similiarity with the asci cam in the lecture where we turn the image to dataURL and converting that string to something else. I ran into trouble with decoded image data storage. I also want to make the first particle wave not be cleared by the click. The final aesthetic is extremely messy and everytime we are interacting with something new which reinforce the zanny.

## Audio reference
The audio sections is mostly the synthesis explained in class. To make it more obnoxious I pump up the audio to make it loud and annoying. 

<br>

<br>

# A2
For me, this work is best to interact with a smaller width and longer height, similiar to a phone screen

<iframe width="100%" height=1200px src="https://happiesday-a2-chaos-ne-22.deno.dev/"></iframe>