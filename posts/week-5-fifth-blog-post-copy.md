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







# Pixel Sort code comment
This code sort the brightness of the pixel vertically, rendering the brightess pixel to be at the top and the darkest at the bottom. It has 2 part: Pixel sort js and Module
Firstly, I will focus on the pixel sort since the Module import the Pixel sort script

```
const quicksort = a => {
   if (a.length <= 1) return a

   let pivot = a[0]
   let left = []
   let right = []

   for (let i = 1; i < a.length; i++) {
      if (a[i].br < pivot.br) left.push (a[i])
      else right.push (a[i])
   }

   const sorted = [ ...quicksort (left), pivot, ...quicksort (right) ]

   return sorted
}
```
Here we create 3 empty arrays: pivot, left and right. Pivot will contain the brightness of the first pixel of the vertical line of the image as the primary comparasion and push the other pixel to the left and right catergory then sum it up in an array call sorted.

```

export class PixelSorter {
   constructor (ctx) {
      this.ctx = ctx
   }

   init () {
      this.width = this.ctx.canvas.width
      this.height = this.ctx.canvas.height
      this.img_data = this.ctx.getImageData (0, 0, this.width, this.height).data
   }

 ```
Firstly, we retrieve its width and height data and create a new image object 

```

   glitch (pos, dim) {
      const find_i = c => ((c.y * this.ctx.canvas.width) + c.x) * 4 
```
Here when finding the brightness data, we skip 4 value in the array as further down below, we will have 5 value for each pixel (red, green, blue, alpha and brightness) and we only focus on the brightness.

```
      for (let x_off = 0; x_off < dim.x; x_off++) {
         const positions = []

         for (let y_pos = pos.y; y_pos < pos.y + dim.y; y_pos++) {
            positions.push (find_i ({ x: pos.x + x_off, y: y_pos }))
         }

         const unsorted = []
```
We calculate the position of x positions of the pixel one column at a time and push it to unsorted array.
```
         positions.forEach (p => {
            const r = this.img_data[p]
            const g = this.img_data[p + 1]
            const b = this.img_data[p + 2]
            const a = this.img_data[p + 3]
            const br = r * g * b
            unsorted.push ({ r, g, b, a, br })
         })
```
For each pixel, it will retrieve 4 value and create a new value called br (brightness)
```
         const sorted = quicksort (unsorted).reverse ()

         let rgba = []

         sorted.forEach (e => {
            rgba.push (e.r)
            rgba.push (e.g)
            rgba.push (e.b)
            rgba.push (e.a)
         })

         rgba = new Uint8ClampedArray (rgba)

         const new_data = this.ctx.createImageData (1, dim.y)
         
         new_data.data.set (rgba)

         this.ctx.putImageData (new_data, pos.x + x_off, pos.y)
      }
   }
```
We then put them to an array with all the brightness data and create a new image version, this time the data will be sorted by the quick sort script. We then deliver the unsort data to the quick sort and the quick sort will deliver the sorted data, which brings us to the Module script.

```
<script type="module">
   import { PixelSorter } from "/scripts/pixel_sort.js"

   const cnv  = document.getElementById (`pixel_sort`)
   cnv.width  = cnv.parentNode.scrollWidth
   cnv.height = cnv.width * 9 / 16   

   const ctx = cnv.getContext (`2d`)
   const sorter = new PixelSorter (ctx)

   const img = new Image ()

   img.onload = () => {
      cnv.height = cnv.width * (img.height / img.width)
      ctx.drawImage (img, 0, 0, cnv.width, cnv.height)
      sorter.init ()
      draw_frame ()
   }

   img.src = `/240408/kornerpark.jpg`

   let frame_count = 0
   const draw_frame = () => {

      ctx.drawImage (img, 0, 0, cnv.width, cnv.height)

      let sig = Math.cos (frame_count * 2 * Math.PI / 500)

      const mid = {
         x: cnv.width / 2,
         y: cnv.height / 2
      }

      const dim = {
         x: Math.floor ((sig + 3) * (cnv.width / 6)) + 1,
         y: Math.floor ((sig + 1) * (cnv.height / 6)) + 1
      }

      const pos = {
         x: Math.floor (mid.x - (dim.x / 2)),
         y: Math.floor (mid.y - (dim.y / 2))
      }

      sorter.glitch (pos, dim)

      frame_count++
      requestAnimationFrame (draw_frame)
   }

</script>
```
The final render will be for each collumn, the brightess pixel will be at the top and the darkess at the bottom. We then come to the Module script which is responsible for loading the original image, then replacing some of it with the glitch version via draw frame.