---
title: Week 5 Glitch
published_at: 2024-4
snippet: Week 5
disable_html_sanitization: true

---

Hello, world

# Comments on the Glitch code

<canvas id="glitch_self_portrait"></canvas> 

<script type="module">

   const cnv = document.getElementById (`glitch_self_portrait`) //get the canvas width and height
   cnv.width = cnv.parentNode.scrollWidth //Including width that is not visible by overflow
   cnv.height = cnv.width * 9 / 16 //Calculate canvas height
   cnv.style.backgroundColor = `red`

   const ctx = cnv.getContext (`2d`) //Create a 2D object based on the canvas size

   let img_data

   const draw = i => ctx.drawImage (i, 0, 0, cnv.width, cnv.height) 
   //drawImage(image, dx, dy, dWidth, dHeight) 
   //in this case, i is the glitched image (layered on top), the image is located at top left, canvas width and height)
   const img = new Image () //Create a new image
   img.onload = () => { //this image have the glitch
      cnv.height = cnv.width * (img.height / img.width) //make the canvas width/ canvas height same ratio as image width/ image height
      draw (img) 
      img_data = cnv.toDataURL ("image/jpeg") //make the image into a string of data
      add_glitch () //call function to add glitch
   }
   img.src = `/240405/pfp_glasses.jpg`

   const rand_int = max => Math.floor (Math.random () * max) 
   //Create a random whole number, max as a placeholder
   //
   const glitchify = (data, chunk_max, repeats) => {
   // Calculate the glitch size, since the image is now view as string of character
      const chunk_size = rand_int (chunk_max / 4) * 4
      // ensure the inside glitch chunk smaller than the maximum glitch chunk
      const i = rand_int (data.length - 24 - chunk_size) + 24
      //only glitch from the pixel line 24th onwards
      const front = data.slice (0, i)
      //slice (start, end), for this one, take a random data from start to a random character
      const back = data.slice (i + chunk_size, data.length)

      //slice (start, end)
      //i + chunk size so the glitch have visible seperated parts
      //data length the condition to make the glitch chunk take out character count does not go over
      //the final character from the data string

      //tldr making sure the glitch is chunky and there is enough characters for the bottom of the image to be glitched
      const result = front + back
      //reunite the data string

      return repeats == 0 ? result : glitchify (result, chunk_max, repeats - 1)
      //if repeat attempts >0, continue to glitch
      //if repeat reach 0, stop
   }

   const glitch_arr = []

   const add_glitch = () => 
   
      {
      //Applying the glitch calculation from above
      const i = new Image ()
      //Create an untouched image
      i.onload = () => {
      //When the image loaded, create an array of the glitch images

         glitch_arr.push (i)
         //this array collects the glitch image
         if (glitch_arr.length < 12) add_glitch ()

         else draw_frame ()
         //is enough glitch image,
      }
      i.src = glitchify (img_data, 96, 6)
      //glitchify = (data, chunk_max, repeats)
      //set the max glitch chunk to 96 character of the string and repeat the glitch 6 times
   }

   let is_glitching = false
   let glitch_i = 0

   const draw_frame = () => {
      if (is_glitching) draw (glitch_arr[glitch_i])
      else draw (img)
      //if glitch, draw the glitched miage, if not, draw the original image

      const prob = is_glitching ? 0.05 : 0.02
      //If the glitch is active, set the prop number value to 5%
      //If the glitch is not active, set the value to 2%

      if (Math.random () < prob) {
         glitch_i = rand_int (glitch_arr.length)
         //select the random glitch image from the glitch array
         is_glitching = !is_glitching
         //turn on and off the glitching
      }
  

      requestAnimationFrame (draw_frame)
      //for every frame, check the condition again
   }
//TLDR, this script only do the probability, calculating the glitch chunk and displaying it


</script>





## Which catergory does my self-portrait belong to?







# AT1 concept
## What is cute as an catergory?
Cute is easy to understand since it is very intuitively easy to acknowledge via its look, its sensory feeling, or its lack of other quality. It can be defined as the spare time for empathy via its vulnerability and commodity.<br>
Firstly, vision serves as a primary sense, as we, as humans, are hard-wired to assess potential threats swiftly. If an entity does not pose imminent danger, then we are to judge it as weird or cute depending on if we are able to attach human-like qualities to it. For example, a lion tripped and fell into the water video would be cute if it stays a video. We can empathize with the lion since we are not there with the lion. Similarly, if it lacks a self-defense mechanism and approachability is available, a power dynamic is formed. <br>
Baby-like, disproportionally small, defenseless, or completed ownership give us a quality of being superior. The urge to buy, to possess and to get close is a commodity aesthetic (Ngai 2020). For example, Hello Kitty is very popular due to its pink pastel and innocent appeal that also makes it a widely sold and lovable product. Accessibility is important for power dynamics. This also tightly intertwined with consumer culture. We want to get close to it first, fixate our curiosity and violently consume it. On one side we like it enough to protect it and on the other side, we are hypnotized to do so willingly.<br>
 "Cute" aesthetic, it often makes us feel a special way, sparking emotions like warmth and love. But how we react to cuteness can be influenced by our culture and society. Sometimes, what's considered cute can bring out tender feelings, and other times, it might lead us to view things in a less serious, more playful light. While art does not always share all the cute definitions, art comes from a place of narrative or abstract, making it qualifies for empathy and vulnerability, and expression, the quality of touchable.


<br>

## Effective Complexity?

Effective Complexity explores the structural balance between making sense and unpredictable variety. Too much would represent chaos and too little would be rigid rules. Murray and Seth agrees that "Effective complexity can be high only a region intermediate between total
order and complete disorder." Which steam from the idea that the polarized extreme side of absolute random and eternal uniformity are simple and lack engagements.
<br>
In cute aesthetic, it is about enough simplicity and complexity dwell within to make certain entity interesting. Take the example of the Ape NFT. The Ape has a simple, adorable design, big eyes. However, his expressive facial reactions and accessory open up the complicated naughty personality inside which adds depth to initial façade innocence outlook. A cute look reinforced by contrasting behavior pushes the sweet spot of making sense of what we're seeing, but also enough unpredictability or variety to keep things challenging.
<br>
With coherent aesthetic frame, we can bypass some originality novelty, refrains its unexpectability to certain mood and style. This approach effective gives it an inherent foundation and composition that can be built upon. The redundancy is not just tolerated but is a key feature of the aesthetic, contributing to the overall experience in a soothing and comforting respond. 


<br>

# AT1L: Journey: The way to Fill this up 
<br>

## What about the work makes it belong to the aesthetic category of "cute"?
For me, the charm of cuteness is found in two main aspects: the ability to shape and create, and the use of color.<br>
Controling this color-jitter-like brush empower me, making me wanting master it and it is enticing to try. I can also define the composition however I want, but in the end I feel the compusle to fill the entire screen, essential indicate that its vulnerbility demand me to cover it up and protecting it. <br>
The color is soft pastel, gradients that blends with the white background which makes the overall mood and style gentle, calming. Yet on the other hand, in this case on the other mouse button, brings about the ability to erase and start anew. Adding layer of white to the underlying color make it seems like an earaser, but in reality, we are adding depth to the fleeing moments of the artwork. <br>
All together, this art make it self feel cute.



## How does the artist employ effective complexity in the work to achieve its aesthetic result?
The unpredictability of the shape but is always less than 6 n-gons make it not so dramtic, the shape generally don't appear sharp and stay true to it lovable, easy looking style. Additionally, the colors are chosen at random but stay within a range of soft pastels. No one color is too bright or too saturated, which makes everything easy on the eyes and nicely smooth out the edges of the shapes. The ability to add white shape or eraser give us control and essentially forfeit its absolute randomness. Vice versa, the ability to control where the brush goes make it predictable and rigid, but is compensated by other feature meantion above.

<br> 

# Fill this up (and a bit of fatal of the flesh)
## Rozendaal's work quality that I retain
The javascript that I experimented with to support my design composition is the variables to make the location date easier to manage, utilizing variables to manage location data more effectively, incorporating randomness for added excitement, implementing mouse interaction variables such as mouseX and mouseY, and utilizing state variables like 'dragged' and 'pressed'. Additionally, I employed the draw pattern function to transition between two phases of the composition. 
For the design composition of the second phase, the randomness of the bombarding lines contributes to the sensation of 'itchiness'. The red hot color palette, pink, and purple, adds a playful yet dynamic opposite to the singular tracing line in the first phase. They also look like donut sprinkles at times.



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
<iframe width="100%" height=400px src="https://editor.p5js.org/HappiesDay/full/4kvHIq4zw"></iframe>



## Change idea
At this point, I drop the shape generator and change the line to become a animated line that follows the cursor arround. Additional, I add a second chaotic phase when the mouse is pressed, toggling a new dimension.
```
function draw() {
  if (patternState === 0) {
    background(255); // Set a white background to contrast with the pattern

    shapes.forEach(shape => {
      shape.update(mouseX, mouseY); // Update each shape's position based on the mouse
      shape.display(); // Display each shape
    });
  } else {
    drawPatternTwo();
  }

```
Through this change of state, it opens my work to a second phase where thing can get more experimental.
 Although it start out black and white, I really like this variant because 
without the color, the work seems to have the clearest narrative. But without color, it does not provoke the sense of fuzziness and uncomfortable I'm looking for in the cute framework.
<iframe width="100%" height=400px src="https://editor.p5js.org/HappiesDay/full/dle8YjHER"></iframe>

# Final
To make this feel more complete, I add minute things such as color jitter when the mouse moving franticly arround the screen. Moreover I add slight increase to the line weight but it is not as noticable. I also add variety if you decide to click the mouse a bunch more time.
<iframe  width="100%" height=800px src="https://editor.p5js.org/HappiesDay/full/iSoRr4Flx"></iframe>