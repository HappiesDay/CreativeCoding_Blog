---
title: Week 5 Glitch
published_at: 2024-3
snippet: Week 5
disable_html_sanitization: true

---

Hello, world

# Comments on the Glitch code
This code focus more on the conditions of the glitch and it works quite linearly on calculating the glitch chunk, prepare a set of glitched image, setting up the glitch probability, and displaying the glitch images.

```
   const cnv = document.getElementById (`glitch_self_portrait`) 
   cnv.width = cnv.parentNode.scrollWidth
   cnv.height = cnv.width * 9 / 16 
   cnv.style.backgroundColor = `red`
   const ctx = cnv.getContext (`2d`) 
```

Default set up


```
   let img_data
   const draw = i => ctx.drawImage (i, 0, 0, cnv.width, cnv.height) 
   const img = new Image () 
   img.onload = () => { 
      cnv.height = cnv.width * (img.height / img.width) 
      draw (img) 
      img_data = cnv.toDataURL ("image/jpeg") 
      add_glitch () 
   }
   img.src = `/240405/pfp_glasses.jpg`
```
When load the image, it call the function to start the glitch effects calculations.

```
   const rand_int = max => Math.floor (Math.random () * max) 
   const glitchify = (data, chunk_max, repeats) => {
      const chunk_size = rand_int (chunk_max / 4) * 4
      const i = rand_int (data.length - 24 - chunk_size) + 24
      const front = data.slice (0, i)
      const back = data.slice (i + chunk_size, data.length)
      const result = front + back
      return repeats == 0 ? result : glitchify (result, chunk_max, repeats - 1)
   }
```

This part is mainly about setting up the condition. Here it splits the string into 2 part and later reunite the string. When conditioning, it calculates the glitch size, since the image is now view as string of character and conditions it to ensure the inside glitch chunk smaller than the maximum glitch chunk and only glitch from the pixel line 24th onwards then reunite the string. It glitch a few times then stop.


```
   const glitch_arr = []

   const add_glitch = () => 
   
      {
      const i = new Image ()
      i.onload = () => {

         glitch_arr.push (i)
         if (glitch_arr.length < 12) add_glitch ()

         else draw_frame ()
      }
      i.src = glitchify (img_data, 96, 6)
   }

```

This part apply the chunk calculation from above, load a new image ready to be glitched, calculating the chunk size of the glitch equals to 96 character of the string , and repeat this 6 times then push these new glitched images to an array ready to be used.



```
   let is_glitching = false
   let glitch_i = 0

   const draw_frame = () => {
      if (is_glitching) draw (glitch_arr[glitch_i])
      else draw (img)

      const prob = is_glitching ? 0.05 : 0.02
      //If the glitch is active, set the prop number value to 5%
      //If the glitch is not active, set the value to 2%

      if (Math.random () < prob) {
         glitch_i = rand_int (glitch_arr.length)
         is_glitching = !is_glitching
      }
  

      requestAnimationFrame (draw_frame)
   }

```      

This part calculate the probability of the glitch, if it happens to glitch, draw the randomly selected glitched image from the array, if not, draw the original image.




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
We then put them to an array with all the brightness data and create a new glitched image version, this time the data will be sorted by the quick sort script. We then deliver the unsort data to the quick sort and the quick sort will deliver the sorted data, which brings us to the Module script that will utilize this new data and animate on it.

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

TLDR: We first calculate the position of the pixel within the column, we then extract 4 rgba value out of it and create a fifth value called br (stand brightness). We then compare the brightness and sort them from left to right then use this new data to draw a new, manipulated image.

<br>

# Self-portrait in the style of glitch

<canvas id="glitch_self_portrait"></canvas>

<script type="module">

   const cnv = document.getElementById (`glitch_self_portrait`)
   cnv.width = cnv.parentNode.scrollWidth
   cnv.height = cnv.width * 9 / 16
   cnv.style.backgroundColor = `deeppink`

   const ctx = cnv.getContext (`2d`)

   let img_data

   const draw = i => ctx.drawImage (i, 0, 0, cnv.width, cnv.height)

   const img = new Image ()
   img.onload = () => {
      cnv.height = cnv.width * (img.height / img.width)
      draw (img)
      img_data = cnv.toDataURL ("image/jpeg")
      add_glitch ()
   }
   img.src = `/images/creepy.jpg`

   const rand_int = max => Math.floor (Math.random () * max)

   const glitchify = (data, chunk_max, repeats) => {
      const chunk_size = rand_int (chunk_max / 4) * 4
      const i = rand_int (data.length - 24 - chunk_size) + 24
      const front = data.slice (0, i)
      const back = data.slice (i + chunk_size, data.length)
      const result = front + back
      return repeats == 0 ? result : glitchify (result, chunk_max, repeats - 1)
   }

   const glitch_arr = []

   const add_glitch = () => {
      const i = new Image ()
      i.onload = () => {
         glitch_arr.push (i)
         if (glitch_arr.length < 12) add_glitch ()
         else draw_frame ()
      }
      i.src = glitchify (img_data, 96, 6)
   }

   let is_glitching = false
   let glitch_i = 0

   const draw_frame = () => {
      if (is_glitching) draw (glitch_arr[glitch_i])
      else draw (img)

      const prob = is_glitching ? 0.05 : 0.02
      if (Math.random () < prob) {
         glitch_i = rand_int (glitch_arr.length)
         is_glitching = !is_glitching
      }

      requestAnimationFrame (draw_frame)
   }

</script>

<br>

## Which of Ngai's aesthetic categories does your self-portrait (and glitch more generally) belong to, and why?
Glitch naturally fits the zanny aesthetic since glitch introduce 3 main parts that reinforce the chaos: Un-welcome behavior, instability and visual disruption. Ngai put zanny fundemental as performative labor, reflect in our precariousness and intensity of contemporary work life. Technology is a big assiciation with our work life. However when technology breaks down, unwelcome and unpredictable actions such as bugging or glitching emerge, leading to feelings of apprehensiveness and distress. This aligns with Ngai's description of the zany as "anxious and excessive." Nick Briz, a new media artist, suggests a basic formula: take a familiar piece of technology and do something unfamiliar with it. This also concurs with Ngai's understanding of the zany as involving imitation and mimicry, almost as if trying to copy in an unstable and forced manner.

<br>

## Does glitch increase or decrease effective complexity, and why?
Glitch effects decrease the coherent flow of the image and introduce new variations that lean more toward a computational aesthetic. A glitched image requires more cognitive effort to interpret. The increase in detail, such as more layers and more textural material, makes the visuals more complicated and consequently disrupts the composition. By altering the readability of the image, potentially it's canvas frame, the complexity goes beyond its effective range and into the realm of digital corruptions, which invites us to a deeper engagement with the relationship between technology and visual expression.

<br>

<br>