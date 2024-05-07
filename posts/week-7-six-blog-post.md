---
title: Week 7 
published_at: 2024-5
snippet: Week 7
disable_html_sanitization: true

---

Hello, world

# Asci cam combine with week 5 glitch

<canvas id="glitch_self_portrait"></canvas>
<script src="/scripts/glitch.js"></script>

# LOL
<div id="ascii_div"></div>

<script type="module">

   // make canvas html element for ASCII art
   const cnv = document.createElement (`canvas`);
   cnv.width = 64; 
   const sourceCanvas = document.getElementById('glitch_self_portrait');
   cnv.height = cnv.width * sourceCanvas.height / sourceCanvas.width; // maintain aspect ratio

   // grab the ascii div from DOM
   const div = document.getElementById(`ascii_div`);
   div.style.fontFamily = `monospace`; // set font to be monospace
   div.style.textAlign = `center`; // center aligned

   // get canvas context for ASCII art
   const ctx = cnv.getContext(`2d`);

   // string of characters from dark - bright
   const chars = "¶Ñ@%&∆∑∫#Wß¥$£√?!†§ºªµ¢çø∂æåπ*™≤≥≈∞~,.…_¬“‘˚`˙";

   const draw_frame = async () => {
      // draw image from source canvas onto ASCII art canvas
      ctx.drawImage(sourceCanvas, 0, 0, cnv.width, cnv.height);

      // get pixel data
      const pixels = await ctx.getImageData(0, 0, cnv.width, cnv.height).data;
      let ascii_img = ``; // start empty ascii string

      for (let y = 0; y < cnv.height; y += 2) {
         for (let x = 0; x < cnv.width; x+= 2) {
            const i = (y * cnv.width + x) * 4; // get pixel position
            const r = pixels[i], g = pixels[i+1], b = pixels[i+2]; // get rgb values
            const br = (r * g * b / 16581376) ** 0.1; // calculate brightness
            const char_i = Math.floor(br * chars.length); // use brightness to select character
            ascii_img += chars[char_i]; // add character to ascii string
         }
         ascii_img += `\n`; // new line
      }

      div.innerText = ascii_img; // add ascii string to innerText of div
      requestAnimationFrame(draw_frame); // wait and then call next frame
   }

   draw_frame(); // start recursive animation
</script>



## Why does combining ideas / libraries seem to make things more aesthetically chaotic?  
Combining ideas and or libraries will increase the nonlinearity directions of the work. In effective complexity, even though it consists of randomness, there are typically some limits to keep things from getting too chaotic and ensure the non-random components remain visible. However when combining ideas and libraries, the limit factor does not proportionally expand to keep up with the new variations. Furthermore, when presented with multiple ideas simultaneously, especially if they are complex or unfamiliar, the cognitive load increases therefore make the visual having more weight and harder to handle, therefore maximizing the discord in communicating the idea effiecently. This complexity can also make it tougher to communicate clearly, which might lead to misunderstandings or confusion, adding to the overall sense of chaos.