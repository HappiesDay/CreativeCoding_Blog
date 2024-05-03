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





